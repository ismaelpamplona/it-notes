# Basic Principles of REST APIs

## Introduction to REST

REST (Representational State Transfer) is an architectural style for designing networked applications. It relies on a stateless, client-server, cacheable communication protocol, usually HTTP. REST APIs are used to perform CRUD (Create, Read, Update, Delete) operations on resources.

## Core Principles of REST

1. **Statelessness**: Each request from a client to a server must contain all the information needed to understand and process the request. The server does not store any client context between requests.

2. **Client-Server Architecture**: The client and server are separate entities. The client is responsible for the user interface, and the server handles data storage and processing. This separation allows for greater flexibility and scalability.

3. **Uniform Interface**: REST APIs have a uniform interface that simplifies and decouples the architecture. This constraint is essential to the design of any RESTful system.

4. **Resource Identification through URI**: Each resource is identified by a unique URI (Uniform Resource Identifier). Resources are typically represented as JSON or XML.

5. **Manipulation of Resources through Representations**: Clients interact with resources by exchanging representations of these resources. For example, a client can get the JSON representation of a resource and update it by sending a new representation.

6. **Self-descriptive Messages**: Each message includes enough information to describe how to process the message. This includes metadata about the message content and how to process it.

7. **Hypermedia as the Engine of Application State (HATEOAS)**: Clients interact with applications entirely through hypermedia provided dynamically by application servers. Hypermedia links provide the possible actions that can be taken.

## HTTP Methods

REST APIs use standard HTTP methods to perform CRUD operations.

- **GET**: Retrieve a resource.

  ```http
  GET /users/1
  ```

- **POST**: Create a new resource.

  ```http
  POST /users
  {
    "name": "John Doe",
    "email": "john.doe@example.com"
  }
  ```

- **PUT**: Update an existing resource.

  ```http
  PUT /users/1
  {
    "name": "John Doe",
    "email": "john.doe@newdomain.com"
  }
  ```

- **DELETE**: Delete a resource.

  ```http
  DELETE /users/1
  ```

- **PATCH**: Partially update a resource.
  ```http
  PATCH /users/1
  {
    "email": "john.doe@newdomain.com"
  }
  ```

## HTTP Status Codes

REST APIs use standard HTTP status codes to indicate the result of an operation.

- **200 OK**: The request was successful.
- **201 Created**: A new resource was created successfully.
- **204 No Content**: The request was successful, but there is no representation to return (for DELETE operations).
- **400 Bad Request**: The request could not be understood or was missing required parameters.
- **401 Unauthorized**: Authentication failed or user does not have permissions for the desired action.
- **403 Forbidden**: Authentication succeeded, but authenticated user does not have access to the resource.
- **404 Not Found**: The requested resource could not be found.
- **500 Internal Server Error**: An error occurred on the server.

## RESTful Resource Naming Conventions

- Use nouns to represent resources, not verbs.

  ```http
  /users
  /orders
  /products
  ```

- Use plural nouns for collections.

  ```http
  /users
  /orders
  ```

- Use hierarchical relationships to represent resources.

  ```http
  /users/1/orders
  /categories/1/products
  ```

- Use query parameters for filtering, sorting, and pagination.
  ```http
  /products?category=electronics&sort=price&limit=10
  ```

## Example REST API

### Define the Resources

1. **User Resource**: GET /users: Retrieve a list of users.

   - GET /users/{id}: Retrieve a specific user.
   - POST /users: Create a new user.
   - PUT /users/{id}: Update a user.
   - DELETE /users/{id}: Delete a user.

2. **Order Resource**: GET /orders/{id}: Retrieve a specific order.
   - POST /orders: Create a new order.
   - PUT /orders/{id}: Update an order.
   - DELETE /orders/{id}: Delete an order.

### Example API Calls

1. **Retrieve a list of users**: `GET /users`

2. **Create a new user**:

   ```http
   POST /users
   Content-Type: application/json

   {
   "name": "John Doe",
   "email": "john.doe@example.com"
   }
   ```

3. **Update a user**:

   ```http
   PUT /users/1
   Content-Type: application/json

   {
   "name": "John Doe",
   "email": "john.doe@newdomain.com"
   }
   ```

4. **Delete a user**: `DELETE /users/1`

## Summary

- **Statelessness**: Each request from a client to a server must contain all the information needed to understand and process the request.
- **Client-Server Architecture**: Separates the user interface from data storage and processing.
- **Uniform Interface**: Simplifies and decouples the architecture.
- **Resource Identification through URI**: Each resource is identified by a unique URI.
- **Manipulation of Resources through Representations**: Clients interact with resources by exchanging representations of these resources.
- **Self-descriptive Messages**: Each message includes enough information to describe how to process the message.
- **Hypermedia as the Engine of Application State (HATEOAS)**: Clients interact with applications entirely through hypermedia provided dynamically by application servers.
