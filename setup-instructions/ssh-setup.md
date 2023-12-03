## SSH setup

- I recommend watching the first few minutes of [this video by Alexey](https://www.youtube.com/watch?v=ae-CV2KfoN0&list=PL3MmuxUbc_hJed7dXYoJw8DoCuVHhGEQb) for understanding how it's done. You can then follow the below steps.

- Create an ssh key in your local system in the `.ssh` folder - [Guide](https://cloud.google.com/compute/docs/connect/create-ssh-keys#linux-and-macos)

- Add the public key (`.pub`) to your VM instance - [Guide](https://cloud.google.com/compute/docs/connect/add-ssh-keys#expandable-2)

- Create a config file in your `.ssh` folder

  ```bash
  touch ~/.ssh/config
  ```

- Copy the following snippet and replace with External IP of the Kafka, Spark (Master Node), Airflow VMs. Username and path to the ssh private key

    ```bash
    Host streamline-kafka
        HostName 34.72.222.232
        User <username>
        IdentityFile <path/to/home/.ssh/keyfile>

    Host streamline-spark
        HostName 34.134.212.114
        User <username>
        IdentityFile <path/to/home/.ssh/keyfile>

    Host streamline-airflow
        HostName 104.155.164.198
        User <username>
        IdentityFile <path/to/home/.ssh/gcp>
    ```
- Once you are setup, you can simply SSH into the servers using the below commands in separate terminals. Do not forget to change the IP address of VM restarts.

    ```bash
    ssh streamline-kafka
    ```

    ```bash
    ssh streamline-spark
    ```

    ```bash
    ssh streamline-airflow
    ```

- You will have to forward ports from your VM to your local machine for you to be able to see Kafka, Airflow UI. The steps for which are given below:

## Port forwarding to local machine:

Using Visual Studio Code, install the Remote - SSH extension by searching in the extensions tab.

Click the button on the bottom-left of the screen

![Alt text](image-2.png)

Then click on the option "Connect to Host..."

![Alt text](image-1.png)

Next, click on the compute instance you want to connect to, say "streamline-kafka"

![Alt text](image-3.png)

Next, open a new terminal in VS Code and click on the "PORTS" tab.

![Alt text](image-4.png)

Here, you can enter the port number that you want to forward to your local machine so you can directly access airflow, kafka, or spark from your local machine.

For example, below, I have forwarded the port number 9021 from "streamify-kafka" so I can check kafka cluster status from my local machine in the browser at "http://localhost:9021/clusters".

![Alt text](image-7.png)

![Alt text](image-6.png)