# Application API POC

This wiki provides comprehensive documentation and guides for the Proof-of-Concept Attendance-API.

## Table of Contents

- [Introduction](#introduction)
- [Pre-requisites](#pre-requisites)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Contact](#contact)
- [Additional Resources](#additional-resources)

## Metadata

|      Author      | Created On | 
|------------------|------------|
| Priyanshu Yadav  | 11/11/2024 | 
## Introduction

This project is a proof-of-concept (POC) for an attendance API. It demonstrates the core functionality and design of the API, providing a foundation for further development and integration.

## Pre-requisites

- [Portgresql](https://www.postgresql.org/)
- [Redis](https://redis.io/)
- [Poetry](https://python-poetry.org/docs/)
- [Liquibase](https://www.liquibase.com/)


## Getting Started

To get started with the attendance API POC, follow these steps:

1. **Clone the Repository:**
    ```sh
    git clone https://github.com/OT-MICROSERVICES/attendance-api.git
    cd attendance-api
    ```
  <img width="773" alt="Screenshot 2024-11-11 at 12 41 23 PM" src="https://github.com/user-attachments/assets/7441f803-4b6f-4a45-8c88-803703b56081">


2. **Install Postgres:**
    ```sh
    sudo apt install postgresql
    ```
<img width="1128" alt="Screenshot 2024-11-11 at 12 42 14 PM" src="https://github.com/user-attachments/assets/8ccb845e-c41f-4cf8-8733-6a35faf33be6">


3. **Install Redis:**
    ```sh
    curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg

    echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list

    sudo apt-get update
    sudo apt-get install redis 
    ```
   <img width="1332" alt="Screenshot 2024-11-11 at 12 46 20 PM" src="https://github.com/user-attachments/assets/08401fb0-0cc8-4b18-b3ba-287e25d7b9c8">


4. **Install Poetry:**
    ```sh
    curl -sSL https://install.python-poetry.org | python3 -
    export PATH="$HOME/.local/bin:$PATH"
    source ~/.bashrc
    ```
   <img width="922" alt="Screenshot 2024-11-11 at 1 12 52 PM" src="https://github.com/user-attachments/assets/24e92200-bae1-4d24-8bcf-03eec45b9c3a">


5. **Install Liquibase:**
    ```sh
   sudo snap install liquibase

   liquibase --version

    ```
   <img width="797" alt="Screenshot 2024-11-11 at 1 18 47 PM" src="https://github.com/user-attachments/assets/d8a003b8-56ae-441c-bb6e-27728cb6c965">


6. **Install Run time Dependency:**
    ```sh
    sudo apt install -y python3.11
    ```
   <img width="1118" alt="Screenshot 2024-11-11 at 1 21 17 PM" src="https://github.com/user-attachments/assets/156f2eb0-aeed-4ab5-89e2-7882ba7483e9">



## Usage

Here are some examples of how to use the API:

1. Firstly, clone the repo locally onto your server.
2. Please update the configuration inside `config.yaml`. Replace the current IP address with your own server's IP. If you are running the service locally, substitute the IP with `localhost`.
<img width="923" alt="Screenshot 2024-11-11 at 1 23 21 PM" src="https://github.com/user-attachments/assets/f55dd713-2924-470a-af1f-210a18bb8d70">

3. Please update the properties inside `liquibase.properties`. Replace the existing IP address with your server's IP. If you are running the service on your local machine, change the IP address to `localhost`.
<img width="826" alt="Screenshot 2024-11-11 at 1 25 03 PM" src="https://github.com/user-attachments/assets/1836b18c-c52f-4879-80b4-0c0d7451b38f">

4. Create user and password with postgresql.
```sh
    sudo -i -u postgres
    psql
    ALTER USER postgres WITH PASSWORD 'password';
```
<img width="653" alt="Screenshot 2024-11-11 at 1 26 15 PM" src="https://github.com/user-attachments/assets/ab861294-4845-4cbf-b1dc-016ccc5c9ae4">


## Run Build

Install dependencies using `poetry install` command.
<img width="802" alt="Screenshot 2024-11-11 at 1 32 43 PM" src="https://github.com/user-attachments/assets/36f3d18f-f995-47d9-9eeb-ec98acc4196a">


For building the application, we can utilize the `make` command alongside our [Makefile](https://github.com/OT-MICROSERVICES/attendance-api/blob/main/Makefile). However, as the first and foremost step, we need to install all the dependencies and packages using Poetry. Fortunately, we can easily accomplish this with a single `make` command.

With Poetry simplifying the installation process, setting up the project becomes effortless. Just execute the `make` command, and witness Poetry seamlessly handle the installation of dependencies and packages. Once completed, you're all set to embark on your development journey with confidence and ease.

```sh
    make build
```


Now we need to run migrations in order to create databases, schema etc.

```sh
    make run-migrations
```
<img width="794" alt="Screenshot 2024-11-11 at 2 36 54 PM" src="https://github.com/user-attachments/assets/6c77e326-b48e-4b76-9372-58519ad12c99">


Once everything is set-up and ready to go. We run the application by:

```sh
    gunicorn app:app --log-config log.conf -b 0.0.0.0:8080
```
<img width="1053" alt="Screenshot 2024-11-11 at 2 37 11 PM" src="https://github.com/user-attachments/assets/67f23f0e-1ef6-4bfc-bb97-a790db82502d">

To check wether the api is working or not we can use below command , replace localhost with your ip address if you are running the api on cloud

```sh
     http://<your-public-ip>:8080/apidocs
```
<img width="995" alt="Screenshot 2024-11-11 at 2 38 25 PM" src="https://github.com/user-attachments/assets/ca5551ea-402d-42e0-a45a-5c4b138d1de9">


We can do health checks also by doing:

```sh
    http://<your-public-ip>:8080/api/v1/attendance/health/detail
```
<img width="1186" alt="Screenshot 2024-11-11 at 2 44 45 PM" src="https://github.com/user-attachments/assets/f0d3d5aa-c33e-406f-b8d7-119a3722b961">


## Contact

For questions or support, please contact:

|       Name       |            Email Address               |
|------------------|----------------------------------------|
| Priyanshu Yadav  | priyanshu.yadav.snaatak@mygurukulam.co |



## Additional Resources

- [Liquibase](https://www.liquibase.com/download)
- [Postgresql](https://www.postgresql.org/download/linux/ubuntu/)
- [Redis](https://redis.io/docs/latest/operate/oss_and_stack/install/install-redis/install-redis-on-linux/)
