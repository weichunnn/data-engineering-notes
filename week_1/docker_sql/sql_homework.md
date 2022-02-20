```
/* ::date -> typecasting to date */
select count(1)
from yellow_taxi_trips
where tpep_pickup_datetime::date = '2021-01-15'
```

```select date_trunc('day', tpep_pickup_datetime) pickup_day,
max(tip_amount) max_tip
from yellow_taxi_trips
group by 1
order by max_tip desc
limit 1
```

```
/* coalesce used to map to argument 2 when argument1 is null */
select coalesce(dozones."Zone", 'Unknown'),
count(1)
from yellow_taxi_trips as taxi
inner join taxi_zones as puzones
on taxi."PULocationID" = puzones."LocationID"
left join taxi_zones as dozones
on taxi."DOLocationID" = dozones."LocationID"
where puzones."Zone" ilike '%central park%'
and tpep_pickup_datetime::date = '2021-01-14'
group by 1
order by 2 desc
```

```
select concat(coalesce(puzones."Zone", 'Unknown'), '/', coalesce(dozones."Zone", 'Unknown')),
avg(total_amount)
from yellow_taxi_trips as taxi
left join taxi_zones as puzones on taxi."PULocationID" = puzones."LocationID"
left join taxi_zones as dozones on taxi."DOLocationID" = puzones."LocationID"
group by 1
order by 2 desc
limit 1
```
