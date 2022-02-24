# Docker Airflow Setup Notes

- https://airflow.apache.org/docs/apache-airflow/stable/concepts/overview.html#:~:text=Airflow%20is%20a%20platform%20that,data%20flows%20taken%20into%20account
- https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html
- https://airflow.apache.org/docs/docker-stack/recipes.html

## What is Parquet

- file format for efficient data storage and retrieval
- efficient data compression and encoding schemes with enhanced performance to handle complex data in bulk
- Good -> Reduction in size, faster query run time, lesser data scanned, lower cost
- https://databricks.com/glossary/what-is-parquet

## Snipet

```
download and output the first 10 lines of file only
curl -sS https://s3data.com | head -n 10
```
