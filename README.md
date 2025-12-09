# 🐾 PetHub

**PetHub** is a simple Java web application built with **Java**, **JDBC**, **Servlets**, and **MySQL**. It demonstrates a small CRUD-style app to manage pets (add, list, update, delete) and is suitable for learning server-side Java web development.

---

## 🔧 Technologies

* Java (8+)
* Servlets (Java EE / Jakarta Servlets)
* JDBC (MySQL Connector/J)
* MySQL (or MariaDB)
* Web server / servlet container (Apache Tomcat recommended)
* Build: optional (Eclipse/IntelliJ or Maven/Gradle)

---

## 🚀 Features

* Add new pets (name, type, age, owner contact)
* List all pets
* Update and delete pet records
* Simple HTML forms + server-side validation

---

## 📦 Prerequisites

1. Java JDK 8 or higher installed. Verify with:

```bash
java -version
javac -version
```

2. MySQL server running and accessible.
3. A servlet container like Apache Tomcat (9+) or an IDE that can run servlets.
4. MySQL JDBC Driver (Connector/J) in your project's `WEB-INF/lib` or added as a dependency.

---

## 🛠️ Step-by-step setup

### 1. Clone the repo

```bash
git clone https://github.com/Vishalnimbal/PetHub.git
cd PetHub
```

### 2. Create the database and table (MySQL)

Open your MySQL client and run:

```sql
CREATE DATABASE pethub_db;
USE pethub_db;

CREATE TABLE pets (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  type VARCHAR(50) NOT NULL,
  age INT,
  owner_contact VARCHAR(150),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 3. Configure database connection

Edit the file where your DB credentials are stored (commonly a `config.properties`, `db.properties`, or inside a servlet):

```properties
db.url=jdbc:mysql://localhost:3306/pethub_db
db.username=YOUR_DB_USER
db.password=YOUR_DB_PASSWORD
```

> 💡 If you use Tomcat, you can also create a JNDI DataSource in `context.xml` and reference it from your servlets.

### 4. Add MySQL Connector/J

Download the MySQL JDBC driver and put the JAR into `WEB-INF/lib/` (if using raw WAR structure), or add as a dependency in Maven/Gradle.

**Maven example** (in `pom.xml`):

```xml
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
  <version>8.0.34</version>
</dependency>
```

### 5. Build and deploy

**If using an IDE:** import the project (Eclipse/IntelliJ), make sure project facets include "Dynamic Web Module", then run on Tomcat.

**If using a WAR file:** package your app and drop the WAR into Tomcat's `webapps/` directory.

```bash
# if using Maven
mvn clean package
# then copy target/PetHub.war -> $TOMCAT_HOME/webapps/
```

### 6. Start Tomcat and open the app

Start your servlet container and open in a browser:

```
http://localhost:8080/PetHub
```

---

## 🧭 Common endpoints (example)

* `GET /pets` - list pets
* `GET /pets/new` - form to create a pet
* `POST /pets` - create a pet
* `GET /pets/edit?id=...` - form to edit a pet
* `POST /pets/update` - update a pet
* `POST /pets/delete` - delete a pet

(Adjust based on your servlet mappings / `web.xml`.)

---

## 🐛 Troubleshooting

* **`ClassNotFoundException: com.mysql.cj.jdbc.Driver`** — make sure the MySQL connector JAR is on the classpath (`WEB-INF/lib` or server lib).
* **Cannot connect to DB** — check `db.url`, username/password, and that MySQL listens on the expected port (usually 3306). Also check firewall.
* **404 on servlet URL** — verify `web.xml` mappings or servlet annotations and ensure the app name used in the URL matches the WAR context.
* **Port conflicts** — Tomcat default is 8080; change `conf/server.xml` if needed.

---

## ✅ Good-to-have improvements

* Use a connection pool (HikariCP, Tomcat JDBC) instead of raw `DriverManager`.
* Move DB credentials to environment variables or a secured properties file.
* Add input validation & better error handling.
* Add unit/integration tests.
* Use Maven/Gradle for dependency management.

---

## 📄 License

This project is provided as-is — add a license file (e.g., MIT) if you want to open source it.

---

## ✨ Contributing

Contributions welcome! Fork the repo, create a branch, submit a pull request.

---

Made with ❤️ and lots of 🐶🐱
