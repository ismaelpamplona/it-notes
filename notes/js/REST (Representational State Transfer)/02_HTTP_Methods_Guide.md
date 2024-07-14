
# HTTP Methods

## 1. GET

### Introduction
The GET method is used to retrieve data from a server at the specified resource. Requests using GET should only retrieve data and should have no other effect on the data.

### Characteristics
- **Safe**: It doesn't alter the state of the resource.
- **Idempotent**: Multiple identical requests should have the same effect as a single request.
- **Cacheable**: Responses can be cached by clients and intermediate caches.

### Usage Example
```http
GET /users/1 HTTP/1.1
Host: example.com
```

### JavaScript Example
```javascript
fetch('https://example.com/users/1')
  .then(response => response.json())
  .then(data => console.log(data));
```

## 2. POST

### Introduction
The POST method is used to send data to the server to create a new resource. The server processes the data and returns a response indicating the result of the operation.

### Characteristics
- **Non-idempotent**: Multiple identical requests can have different effects.
- **Not safe**: It can alter the state of the resource.
- **Not cacheable**: Responses are not cacheable.

### Usage Example
```http
POST /users HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john.doe@example.com"
}
```

### JavaScript Example
```javascript
fetch('https://example.com/users', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    name: 'John Doe',
    email: 'john.doe@example.com'
  })
})
.then(response => response.json())
.then(data => console.log(data));
```

## 3. PUT

### Introduction
The PUT method is used to update an existing resource with the data provided. If the resource does not exist, it can create a new resource.

### Characteristics
- **Idempotent**: Multiple identical requests should have the same effect as a single request.
- **Not safe**: It can alter the state of the resource.
- **Not cacheable**: Responses are not cacheable.

### Usage Example
```http
PUT /users/1 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john.doe@newdomain.com"
}
```

### JavaScript Example
```javascript
fetch('https://example.com/users/1', {
  method: 'PUT',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    name: 'John Doe',
    email: 'john.doe@newdomain.com'
  })
})
.then(response => response.json())
.then(data => console.log(data));
```

## 4. DELETE

### Introduction
The DELETE method is used to delete a specified resource from the server.

### Characteristics
- **Idempotent**: Multiple identical requests should have the same effect as a single request.
- **Not safe**: It alters the state of the resource.
- **Not cacheable**: Responses are not cacheable.

### Usage Example
```http
DELETE /users/1 HTTP/1.1
Host: example.com
```

### JavaScript Example
```javascript
fetch('https://example.com/users/1', {
  method: 'DELETE'
})
.then(response => response.json())
.then(data => console.log(data));
```

## Summary
- **GET**: Retrieve data from a server. Safe, idempotent, and cacheable.
- **POST**: Send data to a server to create a new resource. Not safe, not idempotent, and not cacheable.
- **PUT**: Update an existing resource with new data. Idempotent, not safe, and not cacheable.
- **DELETE**: Remove a resource from the server. Idempotent, not safe, and not cacheable.
