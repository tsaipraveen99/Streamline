- Establish SSH connection with the master node

  ```bash
  ssh streamline-spark
  ```

- Clone the repository and cd into Kafka folder

  ```bash
  git clone https://github.com/jsunecha/Streamline.git && \
  cd Streamline/spark-streaming
  ```

- Set the evironment variables -

  - External IP of the Kafka VM so that spark can connect to it

  - Name of your GCS bucket. (What you gave during the terraform setup)

    ```bash
    export KAFKA_ADDRESS=IP.ADD.RE.SS
    export GCP_GCS_BUCKET=bucket-name
    ```

     **Note**: You will have to setup these env vars every time you create a new shell session. Or if you stop/start your cluster

- Start reading messages

  ```bash
  spark-submit \
  --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.1.2 \
  stream_all_events.py
  ```

- If all went right, you should see new `parquet` files in your bucket! That is Spark writing a file every two minutes for each topic.

- Topics we are reading from

  - listen_events
  - page_view_events
  - auth_events