# **Go Admin Application**

## **Overview**

This project is a Go-based Admin Panel application built with the [GoAdmin framework](https://github.com/GoAdminGroup/go-admin). It provides a ready-to-use admin interface with integration for MySQL.

---

## **Features**

- Admin Panel with customizable themes (`sword` or `adminlte`).
- Database integration with MySQL.
- Dockerized setup for easy deployment.
- Migration script to initialize the database schema.

---

## **Prerequisites**

Before you begin, ensure you have the following installed on your machine:

- [Go](https://golang.org/doc/install) (version 1.22 or later)
- [MySQL](https://dev.mysql.com/downloads/mysql/)
- [Docker](https://www.docker.com/products/docker-desktop) (optional, for containerized setup)
- [Git](https://git-scm.com/)

---

## **Setup Instructions**

### **Step 1: Clone the Repository**

```bash
git clone https://github.com/GoAdminGroup/demo.go-admin.com.git
cd demo.go-admin.com
```

---

### **Step 2: Update Configuration**

1. Edit the `config.json` file in the root directory.
2. Ensure the `database` section matches your MySQL setup:
   ```json
   {
     "database": {
       "default": {
         "host": "127.0.0.1",
         "port": "3306",
         "user": "root",
         "pwd": "your_mysql_password",
         "name": "go_admin_demo",
         "driver": "mysql"
       }
     },
     "prefix": "admin",
     "store": {
       "path": "./uploads",
       "prefix": "uploads"
     },
     "language": "en",
     "index": "/",
     "debug": true,
     "bootstrap_file_path": "./bootstrap.go",
     "theme": "sword"
   }
   ```

---

### **Step 3: Prepare the Database**

1. Log in to MySQL:
   ```bash
   mysql -u root -p
   ```
2. Create the `go_admin_demo` database:
   ```sql
   CREATE DATABASE go_admin_demo;
   ```
3. Import the schema provided:
   ```bash
   mysql -u root -p go_admin_demo < admin.sql
   ```

---

### **Step 4: Run the Application**

1. Compile and run the application:
   ```bash
   go run main.go
   ```
2. Access the admin panel in your browser:
   ```
   http://localhost:9032/admin
   ```

---

## **Optional: Dockerized Setup**

### **Step 1: Build and Run with Docker**

1. Build the Docker image:
   ```bash
   docker build -t go-admin-app .
   ```
2. Run the application container:
   ```bash
   docker run -d -p 9032:9032 --name go-admin-app go-admin-app
   ```

### **Step 2: Using Docker Compose**

If you have a `docker-compose.yml` file, you can start the application and database together:

```bash
docker-compose up --build
```

---

## **Folder Structure**

```
demo.go-admin.com/
├── login/                  # Login module
├── pages/                  # Page definitions
├── tables/                 # Table generators
├── admin.sql               # SQL schema file
├── bootstrap.go            # Bootstrap file
├── config.json             # Configuration file
├── main.go                 # Main entry point
├── go.mod                  # Go module file
├── Makefile                # Build and deploy script
└── README.md               # Documentation
```

---

## **Environment Variables**

If needed, you can override configuration values using environment variables:

- `DB_HOST`: Hostname of the database.
- `DB_PORT`: Port of the database (default: `3306`).
- `DB_USER`: MySQL username.
- `DB_PASSWORD`: MySQL password.
- `DB_NAME`: Database name (default: `go_admin_demo`).

Example:

```bash
export DB_HOST=127.0.0.1
export DB_USER=root
export DB_PASSWORD=root
export DB_NAME=go_admin_demo
```

---

## **Contributing**

Contributions are welcome! Please fork the repository and create a pull request for any changes or improvements.

---

## **Troubleshooting**

1. **Database Connection Error**:
   - Ensure MySQL is running and the credentials in `config.json` are correct.
2. **Port Conflict**:
   - Check if port `9032` is already in use. Update the `main.go` file to use a different port if necessary:
     ```go
     srv := &http.Server{
         Addr: ":9040", // Change port here
         Handler: r,
     }
     ```

---

## **License**

This project is licensed under the MIT License. See the `LICENSE` file for more information.
