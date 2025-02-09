# Set-up Apache Pyspark Cluster Locally using Docker

This repository provides a **Docker-based Apache Spark cluster** setup with:
- **Spark Master**
- **Multiple Spark Workers**
- **Spark History Server**

## 🚀 Setup & Running the Cluster

### 1️⃣ **Build the Spark Image**
```bash
docker-compose build
```

### 2️⃣ **Start the Spark Cluster**
```bash
docker-compose up -d
```
This starts:
- **Spark Master** (`spark://spark-master:7077`)
- **Spark Worker(s)**
- **Spark History Server**

### 3️⃣ **Check Running Containers**
```bash
docker ps
```

### 4️⃣ **Scale Up/Down Workers**
To start **3 worker nodes**:
```bash
docker-compose up -d --scale spark-worker=3
```
To scale dynamically:
```bash
docker-compose up -d --scale spark-worker=5  # Increase to 5 workers
docker-compose up -d --scale spark-worker=2  # Reduce to 2 workers
```

### 5️⃣ **Access Spark Web UI**
- **Spark Master UI** → [http://localhost:9090](http://localhost:9090)
- **Spark History Server UI** → [http://localhost:18080](http://localhost:18080)

### 6️⃣ **Submit an ETL Job**
To run an **ETL pipeline** (e.g., `main.py`):
```bash
docker exec -it da-spark-master spark-submit \
  --master spark://spark-master:7077 \
  --deploy-mode client \
  /path/to/main.py
```
To pass arguments:
```bash
docker exec -it da-spark-master spark-submit \
  --master spark://spark-master:7077 \
  --deploy-mode client \
  /path/to/main.py arg1 arg2
```

### 7️⃣ **Stop & Remove the Cluster**
To **stop** the cluster (without removing containers):
```bash
docker-compose stop
```
To **stop & remove** all containers:
```bash
docker-compose down
```
To **remove everything** (including volumes):
```bash
docker-compose down -v
```

## 📝 Note
- Ensure your ETL scripts (`spark_session.py`, `extract.py`, `transform.py`, `load.py`, `main.py`) are inside the container or mounted.
- Use `spark-submit` to run your jobs.
- Dynamically **scale workers** based on workload.

🚀 **Now you're ready to run your Apache Spark cluster with Docker!**