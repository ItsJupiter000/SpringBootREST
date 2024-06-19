# Spring Boot User Registration and Fetching API

This is a simple Spring Boot project that demonstrates user registration and fetching user details using RESTful APIs. It uses MySQL for the database and implements basic security features.


## Prerequisites

- Java 11 or later
- Maven
- MySQL

## Setup

1. **Clone the repository:**

   ```sh
   git clone https://github.com/your-username/your-repository-name.git
   cd your-repository-name

2. **Configure the database:**

    Update `src/main/resources/application.properties` with your MySQL database credentials.
   
        spring.datasource.url=jdbc:mysql://localhost:3306/your-database-name
        spring.datasource.username=your-username
        spring.datasource.password=your-password
        spring.jpa.hibernate.ddl-auto=update
        spring.jpa.show-sql=true


4. **Create the database schema:**

   Run the SQL script provided in `src/main/resources/schema.sql` to create the necessary table(s).

        CREATE TABLE user (
          id BIGINT NOT NULL AUTO_INCREMENT,
          username VARCHAR(255) NOT NULL,
          email VARCHAR(255) NOT NULL,
          password VARCHAR(255) NOT NULL,
          PRIMARY KEY (id),
          UNIQUE (username)
        );


## Running the Application

1. **Build the project:**

        mvn clean install


2. **Run the project:**

        mvn spring-boot


The application will start on `http://localhost:8080`.

## Using the API

### Register User

- **URL:** `POST http://localhost:8080/api/user/register`

- **Request Body:**

  ```json
  {
    "username": "abc",
    "email": "abc@gmail.com",
    "password": "password123"
  }

- **Response:**
  
  ```json
  {
  "id": 1,
  "username": "abc",
  "email": "abc@gmail.com"
  }

### Fetch User Details

 - **URL:** `GET http://localhost:8080/api/user/fetch?username=abc`
  
 - **Response:**
   
   ```json
   {
    "id": 1,
    "username": "abc",
    "email": "abc@gmail.com"
   }

### Error Responses

#### User Already Exists (Registration):

- **Status Code:** `400 Bad Request`

- **Response Body:**

  ```json
  {
    "error": "User already exists"
  }

#### User Not Found (Fetching User Details):

- **Status Code:** `404 Not Found`

- **Response Body:**

  ```json
  {
    "error": "User not found"
  }
