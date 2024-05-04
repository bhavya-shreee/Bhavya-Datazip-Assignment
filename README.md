Start Minikube with : minikube start --cpus=4 --memory=8192

Create a Helm chart for ClickHouse: helm create clickhouse-chart

Install ClickHouse using Helm: helm install clickhouse ./clickhouse-chart

Check the status of pods: kubectl get pods

Forward port 8123 for ClickHouse SQL interface: kubectl port-forward svc/clickhouse-service 8123:8123

Forward port 9000 for ClickHouse native protocol interface: kubectl port-forward svc/clickhouse-service 9000:9000

Access ClickHouse CLI on the primary container: kubectl exec -it clickhouse-0 -- clickhouse-client

Create a table named "dz_test" in ClickHouse: 

     CREATE TABLE dz_test
(
    B Int64,
    T String,
    D Date
)
ENGINE = MergeTree
PARTITION BY D
ORDER BY B;

Insert data into the "dz_test" table:  insert into dz_test select number, number, '2023-01-01' from numbers(1e6);

Query the first 10 rows from the "dz_test" table: SELECT * FROM dz_test LIMIT 10;
