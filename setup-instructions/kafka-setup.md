We will setup Kafka and eventsim in two separate docker processes in a dedicated compute instance. Eventsim will communicate with port `9092` of the `broker` container of Kafka to send events.

- Establish SSH connection

  ```bash
  ssh streamline-kafka
  ```

- Clone git repo and cd into Kafka folder

  ```bash
  git clone https://github.com/jsunecha/Streamline.git
  ```

- Install anaconda, docker & docker-compose.

  ```bash
  bash ~/Streamline/scripts/vm_setup.sh && \
  exec newgrp docker
  ```

- Set the evironment variables -

  - External IP of the Kafka VM

    ```bash
    export KAFKA_ADDRESS=IP.ADD.RE.SS
    ```

     **Note**: You will have to setup these env vars every time you create a new shell session. Or if you stop/start your VM

- Start Kafka 

  ```bash
  cd ~/Streamline/kafka && \
  docker-compose build && \
  docker-compose up 
  ```

  **Note**: Sometimes the `broker` & `schema-registry` containers die during startup. You should just stop all the containers with `docker-compose down` and then rerun `docker-compose up`.

- The Kafka Control Center should be available on port `9021`. Open and check if everything is working fine.

- Open another terminal session for the Kafka VM and start sending messages to your Kafka broker with Eventsim

  ```bash
  bash ~/Streamline/scripts/eventsim_startup.sh
  ```

  This will start creating events for 1 Million users spread out from the current time to the next 24 hours. 
  The container will run in detached mode. Follow the logs to see the progress.

- To follow the logs

  ```bash
  docker logs --follow million_events
  ```

- The messages should start showing in a few minutes.
  
- You should see four topics -

  - listen_events
  - page_view_events
  - auth_events
  - status_change_events

