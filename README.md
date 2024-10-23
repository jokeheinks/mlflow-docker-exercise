# CAISO MLflow model

California ISO Model for load forecasting (CAISO): It predicts for the next
day by taking hourly averages of the three days with highest
average consumption value among a pool of ten previous days,
excluding weekends, holidays, and past DR event days

Tho model is packed as a MLflow Project. When run, it fetches the newest data, trains a CAISO model and saves it locally as an MLflow Model. 
Here's a starting point for running and deploying a CAISO model locally:

```
git clone https://github.itu.dk/bhei/mlflow-docker-exercise
cd caiso-mlflow
mlflow run .
mlflow models serve -m model
```

You can now query the model using curl, for example:
```
curl -X POST http://127.0.0.1:5000/invocations -H "Content-Type: application/json" -d '{
    "dataframe_split": {
        "columns": ["Time"],
        "data": [
            ["2024-10-20 14:00:00"],
        ]
    }
}'
```
