# SupplierController Documentation

## Overview
The `SupplierController` is a RESTful controller in a Spring Boot application that manages CRUD operations for `Supplier` entities. It provides endpoints for creating, reading, updating, and deleting suppliers. The controller interacts with the `SupplierService` to perform business logic and data manipulation.

## Metadata
- **File Name**: `SupplierController.java`
- **Package**: `com.example.supplier.controller`

## Endpoints

| HTTP Method | Endpoint               | Description                                      | Request Body         | Response Type         |
|-------------|------------------------|--------------------------------------------------|----------------------|-----------------------|
| `GET`       | `/api/suppliers`       | Retrieve all suppliers.                         | None                 | `List<Supplier>`      |
| `GET`       | `/api/suppliers/{id}`  | Retrieve a supplier by its ID.                  | None                 | `ResponseEntity<Supplier>` |
| `POST`      | `/api/suppliers`       | Create a new supplier.                          | `Supplier`           | `Supplier`            |
| `PUT`       | `/api/suppliers/{id}`  | Update an existing supplier by its ID.          | `Supplier`           | `ResponseEntity<Supplier>` |
| `DELETE`    | `/api/suppliers/{id}`  | Delete a supplier by its ID.                    | None                 | `ResponseEntity<Void>` |

## Dependencies
- **Spring Framework**:
  - `@RestController`: Marks the class as a RESTful controller.
  - `@RequestMapping`: Maps the base URL `/api/suppliers` for all endpoints in this controller.
  - `@Autowired`: Injects the `SupplierService` dependency.
  - `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`: Maps HTTP methods to specific endpoints.
  - `ResponseEntity`: Used to handle HTTP responses with appropriate status codes.

- **SupplierService**: A service layer that encapsulates business logic for supplier management.

## Methods

### `getAllSuppliers()`
- **Description**: Fetches all suppliers from the database.
- **Return Type**: `List<Supplier>`
- **HTTP Method**: `GET`
- **Endpoint**: `/api/suppliers`

### `getSupplierById(Long id)`
- **Description**: Fetches a supplier by its ID. Returns `404 Not Found` if the supplier does not exist.
- **Parameters**:
  - `@PathVariable Long id`: The ID of the supplier to retrieve.
- **Return Type**: `ResponseEntity<Supplier>`
- **HTTP Method**: `GET`
- **Endpoint**: `/api/suppliers/{id}`

### `createSupplier(Supplier supplier)`
- **Description**: Creates a new supplier in the database.
- **Parameters**:
  - `@RequestBody Supplier supplier`: The supplier object to be created.
- **Return Type**: `Supplier`
- **HTTP Method**: `POST`
- **Endpoint**: `/api/suppliers`

### `updateSupplier(Long id, Supplier supplierDetails)`
- **Description**: Updates an existing supplier by its ID. Returns `404 Not Found` if the supplier does not exist.
- **Parameters**:
  - `@PathVariable Long id`: The ID of the supplier to update.
  - `@RequestBody Supplier supplierDetails`: The updated supplier details.
- **Return Type**: `ResponseEntity<Supplier>`
- **HTTP Method**: `PUT`
- **Endpoint**: `/api/suppliers/{id}`

### `deleteSupplier(Long id)`
- **Description**: Deletes a supplier by its ID. Returns `404 Not Found` if the supplier does not exist.
- **Parameters**:
  - `@PathVariable Long id`: The ID of the supplier to delete.
- **Return Type**: `ResponseEntity<Void>`
- **HTTP Method**: `DELETE`
- **Endpoint**: `/api/suppliers/{id}`

## Insights
- **Error Handling**: The controller uses `ResponseEntity` to handle HTTP responses, ensuring proper status codes (`200 OK`, `404 Not Found`, `204 No Content`) are returned based on the operation's outcome.
- **Dependency Injection**: The `SupplierService` is injected using `@Autowired`, promoting loose coupling and testability.
- **RESTful Design**: The controller adheres to RESTful principles, using appropriate HTTP methods (`GET`, `POST`, `PUT`, `DELETE`) for CRUD operations.
- **Optional Handling**: The `getSupplierById` method uses `Optional` to handle cases where a supplier may not exist, improving code readability and robustness.
- **Scalability**: The controller is designed to handle supplier-related operations, making it easy to extend or integrate with other parts of the application.
