## Local Instance of Postgres13

```
docker run -it \
  -e POSTGRES_USER='root' \
  -e POSTGRES_PASSWORD='root' \
  -e POSTGRES_DB='ny_taxi' \
  -v /Users/weichun/Desktop/data_engineering/week_1/ny_taxi_postgres:/var/lib/postgresql/data \
  -p 5432:5432 \
  postgres:13

docker run -it \
  -e PGADMIN_DEFAULT_EMAIL='admin@admin.com' \
  -e PGADMIN_DEFAULT_PASSWORD='root' \
  -p 8080:80 \
  dpage/pgadmin4
```

## Creating Network

```
docker network create pg-network

docker run -it \
  -e POSTGRES_USER='root' \
  -e POSTGRES_PASSWORD='root' \
  -e POSTGRES_DB='ny_taxi' \
  -v /Users/weichun/Desktop/data_engineering/week_1/ny_taxi_postgres:/var/lib/postgresql/data \
  --network=pg-network \
  --name pg-database \
  -p 5432:5432 \
  postgres:13

docker run -it \
  -e PGADMIN_DEFAULT_EMAIL='admin@admin.com' \
  -e PGADMIN_DEFAULT_PASSWORD='root' \
  --network=pg-network \
  --name pgadmin \
  -p 8080:80 \
  dpage/pgadmin4
```

## Ingesting taxi data

```
python ingest_data.py \
  --user=root \
  --password=root \
  --host=localhost \
  --port=5432 \
  --db=ny_taxi \
  --table_name=yellow_taxi_trips \
  --url="https://s3.amazonaws.com/nyc-tlc/trip+data/yellow_tripdata_2021-01.csv"

docker build -t taxi_ingest:v0001 .

docker run -it \
  --network=week_1_default \
  taxi_ingest:v0001 \
    --user=root \
    --password=root \
    --host=pgdatabase \
    --port=5432 \
    --db=ny_taxi \
    --table_name=yellow_taxi_trips \
    --url="https://s3.amazonaws.com/nyc-tlc/trip+data/yellow_tripdata_2021-01.csv"
```

## ingesting zones data

```
python ingest_data.py \
 --user=root \
 --password=root \
 --host=localhost \
 --port=5432 \
 --db=ny_taxi \
 --table_name=taxi_zones \
 --url="https://s3.amazonaws.com/nyc-tlc/misc/taxi+_zone_lookup.csv"
```
