# Deployment in GCP

## 📌 Project Overview
This repository contains my assignment for Enterprise Cloud Architecture, demonstrating the deployment of a Spring Boot application with a MySQL database hosted on Google Cloud SQL.

## 🎥 Demo Video
Watch the project in action: [Click Here](https://drive.google.com/file/d/1iL6VxzlapYBDuoGFDCgkxTNTi2iMzUp7/view?usp=sharing)

## 📒 Google Cloud SQL (MySQL) Setup Guide

### Phase 1: Access Google Cloud Console
* Navigate to: https://console.cloud.google.com/sql
* Ensure the correct project is selected.

### Phase 2: Initialize Cloud SQL Instance
1. Select **Create Instance** → opt for **MySQL**.
2. Select **MySQL 8.0** (strongly recommended).
3. Assign an **Instance ID** (example: `mysqldb-instance`).
4. Configure the **root password** (example: `Mysql-ECA1!`).
5. Region selection: choose **us-central1** (or your nearest region).
6. Availability configuration: select **Single zone** for development purposes.

### Phase 3: Configure Public IP Access
1. Navigate to your instance → select **Connections** section.
2. Under **Public IP**, select **Add network**.
3. Provide name: `development-access`.
4. Set IP range to `0.0.0.0/0` (⚠️ **Development use only**).
5. Save configuration and copy the **Public IP** (example: `34.56.223.88`).

### Phase 4: Database Creation Within Instance
1. Launch Cloud Shell or local terminal and establish connection:

```bash
docker run -it --rm mysql:8 mysql -h <YOUR_PUBLIC_IP> -u root -p
```

Example connection:

```bash
docker run -it --rm mysql:8 mysql -h 34.56.223.88 -u root -p
```

Enter your configured password (`Mysql-ECA1!`).

2. Execute database creation command:

```sql
CREATE DATABASE mysqldb;
```

3. Verify successful creation:

```sql
SHOW DATABASES;
```

The `mysqldb` database should appear in the list.

### Phase 5: Spring Boot Application Integration
Configure your `application-gcp.properties` file:

```properties
spring.datasource.url=jdbc:mysql://<Public IP address>:3306/mysqldb?createDatabaseIfNotExist=true
spring.datasource.username=root
spring.datasource.password=#######
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

server.port=8081
```

Launch your Spring Boot application to establish connection with the Cloud SQL database.

## 🚀 Getting Started

1. Clone this repository:

```bash
git clone https://github.com/UchithmaSenevirathne/Cloud-Deployment.git
```

2. Modify `application-gcp.properties` with your specific database configuration.
3. Execute the Spring Boot application:

4. Open your browser and navigate to `http://localhost:8081`.

## 📄 License Information
This project is distributed under the [MIT License](LICENSE).. 