import dask.dataframe as dd
import pandas as pd
import time
import plotly.express as px
import plotly.graph_objects as go
from plotly.subplots import make_subplots

file_path = "Air_Quality.csv"
df = dd.read_csv(file_path, dtype={'Geo Join ID': 'float64'})
print("Dataset Loaded Successfully!\nColumns:", df.columns)
df["Data Value"] = dd.to_numeric(df["Data Value"], errors='coerce')
df = df.dropna(subset=["Data Value"])

if 'Data Value' in df.columns:
    print("\n🔹 Data Value Statistics:")
    print(df["Data Value"].describe().compute())
fig = make_subplots(rows=3, cols=1, subplot_titles=["Data Value Trend Over Years", "Average Data Value by Measure", "Average Data Value by Geo Place Name"],
specs=[[{"type": "xy"}], [{"type": "pie"}], [{"type": "xy"}]])
if {'Start_Date', 'Data Value'}.issubset(df.columns):
    df["Start_Date"] = dd.to_datetime(df["Start_Date"], errors='coerce')
    trend_data = df.groupby(df["Start_Date"].dt.year)["Data Value"].mean().compute()
    if not trend_data.empty:
        print("\n📈 Data Value Trend Over Years:")
        print(trend_data)
        fig.add_trace(go.Scatter(x=trend_data.index, y=trend_data.values, mode='lines', name="Trend"), row=1, col=1)
    else:
        print("\n⚠ No data available for Data Value Trend.")

if {'Measure', 'Data Value'}.issubset(df.columns):
    avg_measure_value = df.groupby("Measure")["Data Value"].mean().compute()
    if not avg_measure_value.empty:
        print("\n🔹 Average Data Value by Measure:")
        print(avg_measure_value)
        fig.add_trace(go.Pie(labels=avg_measure_value.index, values=avg_measure_value.values, name="Measure"), row=2, col=1)
    else:
        print("\n⚠ No data available for Average Data Value by Measure.")
if {'Geo Place Name', 'Data Value'}.issubset(df.columns):
    avg_data_value = df.groupby("Geo Place Name")["Data Value"].mean().compute()
    if not avg_data_value.empty:
        print("\n🔹 Average Data Value by Geo Place Name:")
        print(avg_data_value)
        worst_air_quality = avg_data_value.idxmax()
        worst_air_value = avg_data_value.max()
        print(f"\n🔥 Worst Air Quality: {worst_air_quality} ({worst_air_value})")
        fig.add_trace(go.Bar(x=avg_data_value.index, y=avg_data_value.values, name="Geo Place Name"), row=3, col=1)
    else:
        print("\n⚠ No data available for Average Data Value by Geo Place Name.")
fig.update_layout(height=900, title_text="Air Quality Data Analysis")
fig.show()

print("\n⏳ Comparing Dask vs Pandas Performance...")
start_time = time.time()
pandas_avg = pd.read_csv(file_path).groupby("Geo Place Name")["Data Value"].mean()
print("✅ Pandas Time:", time.time() - start_time, "s")
start_time = time.time()
dask_avg = df.groupby("Geo Place Name")["Data Value"].mean().compute()
print("✅ Dask Time:", time.time() - start_time, "s")
