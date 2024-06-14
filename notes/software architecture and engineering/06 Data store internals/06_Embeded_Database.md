# 6. Embedded Database

An embedded database is a database system that is integrated directly into an application. It runs within the application’s process, providing a lightweight and fast data storage solution without the need for a separate database server.

## Embedded vs Remote Database

### Embedded Database

**Characteristics:**

- **Integration:** The database runs within the application process.
- **Deployment:** Distributed as part of the application package.
- **Performance:** Typically faster for local operations due to in-process execution.
- **Maintenance:** Less administrative overhead; the application handles database management.
- **Use Case:** Ideal for applications requiring local storage with low latency, such as desktop applications, mobile apps, and IoT devices.

**Examples:**

- SQLite
- H2 (Java)
- Berkeley DB

### Remote Database

**Characteristics:**

- **Integration:** The database runs on a separate server, accessible over a network.
- **Deployment:** Requires separate installation and configuration.
- **Performance:** Network latency can affect performance; suitable for distributed systems.
- **Maintenance:** Requires regular administrative tasks such as backups, scaling, and security management.
- **Use Case:** Suitable for applications requiring centralized data storage and access by multiple clients, such as web applications, enterprise systems, and cloud services.

**Examples:**

- PostgreSQL
- MySQL
- MongoDB

### Key Differences

| **Characteristic** | **Embedded Database**                                                 | **Remote Database**                                                              |
| ------------------ | --------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| **Location**       | Runs within the same process as the application                       | Runs on a separate server and accessed over a network                            |
| **Performance**    | Faster local access due to in-process execution                       | May incur network latency; suitable for distributed access                       |
| **Maintenance**    | Minimal maintenance; managed by the application                       | Requires dedicated administrative tasks                                          |
| **Scalability**    | Limited by the resources of the host machine                          | Can be scaled horizontally or vertically by adding more servers or resources     |
| **Use Cases**      | Desktop applications, mobile apps, local data storage for IoT devices | Web applications, enterprise systems, applications requiring multi-client access |

### Example of an Embedded Database (SQLite)

SQLite is a popular embedded database widely used in mobile applications and local data storage.

**Setting up SQLite in Rust:**

First, add the `rusqlite` dependency to your `Cargo.toml` file:

```toml
[dependencies]
rusqlite = "0.25.3"
```

Then, use the following code to create and interact with an SQLite database:

```rust
use rusqlite::{params, Connection, Result};

fn main() -> Result<()> {
    // Connect to the SQLite database (creates a database file if it doesn't exist)
    let conn = Connection::open("example.db")?;

    // Create a table
    conn.execute(
        "CREATE TABLE users (
                  id              INTEGER PRIMARY KEY,
                  name            TEXT NOT NULL,
                  email           TEXT NOT NULL
                  )",
        [],
    )?;

    // Insert a record
    conn.execute(
        "INSERT INTO users (name, email) VALUES (?1, ?2)",
        params!["Alice", "alice@example.com"],
    )?;

    // Query the database
    let mut stmt = conn.prepare("SELECT id, name, email FROM users")?;
    let user_iter = stmt.query_map([], |row| {
        Ok(User {
            id: row.get(0)?,
            name: row.get(1)?,
            email: row.get(2)?,
        })
    })?;

    // Print the query results
    for user in user_iter {
        println!("Found user {:?}", user.unwrap());
    }

    Ok(())
}

#[derive(Debug)]
struct User {
    id: i32,
    name: String,
    email: String,
}
```

### Example of a Remote Database (PostgreSQL)

PostgreSQL is a powerful remote database used in many web applications and enterprise systems.

**Setting up PostgreSQL in Rust:**

First, add the `tokio-postgres` and `tokio` dependencies to your `Cargo.toml` file:

```toml
[dependencies]
tokio = { version = "1", features = ["full"] }
tokio-postgres = "0.7"
```

Then, use the following code to create and interact with a PostgreSQL database:

```rust
use tokio_postgres::{NoTls, Error};

#[tokio::main]
async fn main() -> Result<(), Error> {
    // Connect to the PostgreSQL database
    let (client, connection) =
        tokio_postgres::connect("host=localhost user=dbuser password=dbpassword dbname=exampledb", NoTls).await?;

    // The connection object performs the actual communication with the database,
    // so spawn it off to run on its own.
    tokio::spawn(async move {
        if let Err(e) = connection.await {
            eprintln!("connection error: {}", e);
        }
    });

    // Create a table
    client.batch_execute("
        CREATE TABLE users (
            id      SERIAL PRIMARY KEY,
            name    VARCHAR(100),
            email   VARCHAR(100)
        )
    ").await?;

    // Insert a record
    client.execute(
        "INSERT INTO users (name, email) VALUES ($1, $2)",
        &[&"Alice", &"alice@example.com"],
    ).await?;

    // Query the database
    for row in client.query("SELECT id, name, email FROM users", &[]).await? {
        let id: i32 = row.get(0);
        let name: &str = row.get(1);
        let email: &str = row.get(2);

        println!("Found user: {} - {} ({})", id, name, email);
    }

    Ok(())
}
```

## Summary

An embedded database is integrated directly into the application, providing fast and lightweight local data storage, ideal for single-user or local scenarios. In contrast, a remote database runs on a separate server, accessible over a network, suitable for multi-user, centralized, and distributed applications. Each type has its advantages and is chosen based on the specific requirements of the application.
