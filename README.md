# Auth Service Task
## User Sign Up, User Login, Role and Permission module.

The diagram shows the database design of the module.

![Database Diagram](databasediagram.png)
## Dependency
 MySQL:
```xml
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
  <scope>runtime</scope>
</dependency>
```
## Configure Spring Datasource, JPA, App properties
Open `src/main/resources/application.properties`
```
spring.datasource.url= jdbc:mysql://xxxxxxxxxxxxx
spring.datasource.username= xxxxx
spring.datasource.password= xxxx
spring.jpa.properties.hibernate.dialect= org.hibernate.dialect.MySQL5InnoDBDialect
spring.jpa.hibernate.ddl-auto= update
airasia.app.jwtSecret= airasiaSecretKey
airasia.app.jwtExpirationMs= 86400000
```
## Run Spring Boot application
```
mvn spring-boot:run
```

## API Request Reponse Documentation

 Roles

```
Get Roles
Request:
GET /api/roles HTTP/1.1
Host: localhost:5000
Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJha3NoYXkiLCJpYXQiOjE2MTE1NTk3NTYsImV4cCI6MTYxMTY0NjE1Nn0.bPnNjq51IGwSCSOmQN06RwUfJglYJGsMUiBmMIr_5Is0Jl4AE_cQ8LKkyfQ4y9ryVDJ16uypc1sAIyYC6l_mmA

Response:
[{"id":1,"name":"Admin","permissions":[{"id":1,"name":"add"}]}]
```

Create Roles:
```
Request:
POST /api/roles HTTP/1.1
Host: localhost:5000
Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJha3NoYXkiLCJpYXQiOjE2MTE1NTk3NTYsImV4cCI6MTYxMTY0NjE1Nn0.bPnNjq51IGwSCSOmQN06RwUfJglYJGsMUiBmMIr_5Is0Jl4AE_cQ8LKkyfQ4y9ryVDJ16uypc1sAIyYC6l_mmA
Content-Type: application/json
Content-Length: 51

{
    "role":"user",
    "permission":["view"]
}
Response:
{
    "message": "Role Created Successfully",
    "unassignedPermissions": []
}
```

Permissions:
```
Get Permissions
Request:
GET /api/permissions HTTP/1.1
Host: localhost:5000Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJha3NoYXkiLCJpYXQiOjE2MTE1NTk3NTYsImV4cCI6MTYxMTY0NjE1Nn0.bPnNjq51IGwSCSOmQN06RwUfJglYJGsMUiBmMIr_5Is0Jl4AE_cQ8LKkyfQ4y9ryVDJ16uypc1sAIyYC6l_mmA

Response:
[
    {
        "id": 1,
        "name": "add"
    }
]
```
Create Permissions
```
Request:
POST /api/permissions HTTP/1.1
Host: localhost:5000
Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJha3NoYXkiLCJpYXQiOjE2MTE1NTk3NTYsImV4cCI6MTYxMTY0NjE1Nn0.bPnNjq51IGwSCSOmQN06RwUfJglYJGsMUiBmMIr_5Is0Jl4AE_cQ8LKkyfQ4y9ryVDJ16uypc1sAIyYC6l_mmA
Content-Type: application/json
Content-Length: 23

{
    "name":"view"
}
Response:
{
    "message": "Permission successfully!"
}
```

Login
```
Request:

POST /api/auth/login HTTP/1.1
Host: localhost:5000
Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJha3NoYXkiLCJpYXQiOjE2MTE1NTk3NTYsImV4cCI6MTYxMTY0NjE1Nn0.bPnNjq51IGwSCSOmQN06RwUfJglYJGsMUiBmMIr_5Is0Jl4AE_cQ8LKkyfQ4y9ryVDJ16uypc1sAIyYC6l_mmA
Content-Type: application/json
Content-Length: 55

{
    "username":"akshay",
    "password":"akshay"
}

Response:
{
    "id": 1,
    "username": "akshay",
    "email": "akshay13091992@gmail.com",
    "roles": [
        "Admin"
    ],
    "accessToken": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJha3NoYXkiLCJpYXQiOjE2MTE1NTk1ODQsImV4cCI6MTYxMTY0NTk4NH0.Zi7dRq2Kn30RijV34l6XC5QlLgEU9iVMrVRP2ssQjGI8rXhuHaC-P0hZ5VZXiKKR6Vz_aCrfXDxvPt6RPxzuCg",
    "tokenType": "Bearer"
}
```

Signup
```
Request:
POST /api/auth/signup HTTP/1.1
Host: localhost:5000
Content-Type: application/json
Content-Length: 88

{
    "username":"aditya",
    "password":"aditya",
    "email":"aditya@gmail.com"
}

Response:
{
    "message": "User registered successfully!"
}
```

Get Available Roles:
```
Request:

GET /api/users/1/roles HTTP/1.1
Host: localhost:5000
Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJha3NoYXkiLCJpYXQiOjE2MTE1NTk3NTYsImV4cCI6MTYxMTY0NjE1Nn0.bPnNjq51IGwSCSOmQN06RwUfJglYJGsMUiBmMIr_5Is0Jl4AE_cQ8LKkyfQ4y9ryVDJ16uypc1sAIyYC6l_mmA


Response:
[
    {
        "id": 1,
        "name": "Admin",
        "permissions": [
            {
                "id": 1,
                "name": "add"
            }
        ]
    }
]
```

Add Roles to User
```
Request :
POST /api/users/2/roles HTTP/1.1
Host: localhost:5000
Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJha3NoYXkiLCJpYXQiOjE2MTE1NTk3NTYsImV4cCI6MTYxMTY0NjE1Nn0.bPnNjq51IGwSCSOmQN06RwUfJglYJGsMUiBmMIr_5Is0Jl4AE_cQ8LKkyfQ4y9ryVDJ16uypc1sAIyYC6l_mmA
Content-Type: application/json
Content-Length: 34

{
    "roles":["user","admin"]
}

Response:
{
    "message": "Role Added Successfully",
    "unassignedRoles": []
}
```

Get Permissions of User:
```
Request:
GET /api/users/2/permissions HTTP/1.1
Host: localhost:5000
Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJha3NoYXkiLCJpYXQiOjE2MTE1NTk3NTYsImV4cCI6MTYxMTY0NjE1Nn0.bPnNjq51IGwSCSOmQN06RwUfJglYJGsMUiBmMIr_5Is0Jl4AE_cQ8LKkyfQ4y9ryVDJ16uypc1sAIyYC6l_mmA
Content-Type: application/json
Content-Length: 37

{
    "permissionIds":[1,2,3,4,5]
}
Response:
{
    "notAllowedPermissions": [
        3,
        4,
        5
    ],
    "allowedPermissions": [
        1,
        2
    ]
}
```
