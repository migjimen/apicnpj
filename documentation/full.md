
# Table of Contents

## doc

### supplier-api

#### src

##### main

###### java

###### com

###### example

###### supplier
 - [Documentation: GlobalExceptionHandler.java](#documentation-globalexceptionhandlerjava)
 - [Documentation: `ErrorResponse` Class](#documentation-errorresponse-class)
 - [SupplierApplication Documentation](#supplierapplication-documentation)

###### controller
 - [SupplierController Documentation](#suppliercontroller-documentation)

###### model
 - [Documentation: Supplier.java](#documentation-supplierjava)

###### repository
 - [Documentation: SupplierRepository.java](#documentation-supplierrepositoryjava)

###### service
 - [SupplierService Documentation](#supplierservice-documentation)

###### util
 - [Documentation: `CodigoUtil.java`](#documentation-codigoutiljava)

##### test

###### java

###### com

###### example

###### supplier
 - [Documentation: `SupplierApplicationTests.java`](#documentation-supplierapplicationtestsjava)

### supplier-react-app

#### src
 - [Documentation](#documentation)
 - [Documentation: App.js](#documentation-appjs)

##### components
 - [Documentation: SupplierForm Component](#documentation-supplierform-component)
 - [Documentation: SupplierList Component](#documentation-supplierlist-component)

##### services
 - [Documentation: Supplier Service](#documentation-supplier-service)
---
<div style="page-break-after: always;"></div>

# Documentation: GlobalExceptionHandler.java

## Overview
The `GlobalExceptionHandler` class is a centralized exception handling mechanism for a Spring Boot application. It uses the `@ControllerAdvice` annotation to intercept and handle exceptions thrown by controllers globally. This approach ensures consistent error responses across the application.

## Features
- Handles specific exceptions such as `ConstraintViolationException` and `IllegalArgumentException`.
- Provides a fallback mechanism for handling generic exceptions.
- Returns structured error responses with HTTP status codes and descriptive messages.

## Class Details

### Annotations
| Annotation         | Purpose                                                                 |
|--------------------|-------------------------------------------------------------------------|
| `@ControllerAdvice`| Marks the class as a global exception handler for all controllers.     |
| `@ExceptionHandler`| Specifies the type of exception to handle for each method.             |

### Methods

#### `handleConstraintViolationException`
Handles exceptions of type `ConstraintViolationException`.

| **Parameter** | **Type**                     | **Description**                                   |
|---------------|------------------------------|-------------------------------------------------|
| `ex`          | `ConstraintViolationException` | The exception object containing validation errors.|

| **Return Type** | **Description**                                                                 |
|-----------------|-------------------------------------------------------------------------------|
| `ResponseEntity<ErrorResponse>` | Returns a `400 BAD_REQUEST` status with a validation error message.|

---

#### `handleIllegalArgumentException`
Handles exceptions of type `IllegalArgumentException`.

| **Parameter** | **Type**                  | **Description**                                   |
|---------------|---------------------------|-------------------------------------------------|
| `ex`          | `IllegalArgumentException` | The exception object containing the error details.|

| **Return Type** | **Description**                                                                 |
|-----------------|-------------------------------------------------------------------------------|
| `ResponseEntity<ErrorResponse>` | Returns a `400 BAD_REQUEST` status with the exception message.|

---

#### `handleException`
Handles generic exceptions of type `Exception`.

| **Parameter** | **Type**      | **Description**                                   |
|---------------|---------------|-------------------------------------------------|
| `e`           | `Exception`   | The exception object containing the error details.|

| **Return Type** | **Description**                                                                 |
|-----------------|-------------------------------------------------------------------------------|
| `ResponseEntity<ErrorResponse>` | Returns a `500 INTERNAL_SERVER_ERROR` status with a generic error message.|

---

## Insights

### ErrorResponse Class
The methods in this class rely on an `ErrorResponse` object to structure the error details. While the `ErrorResponse` class is not provided in the code snippet, it is expected to have at least two fields:
- **Status**: Represents the HTTP status code as a string.
- **Message**: Contains the error description.

### Exception Handling Strategy
- **Specific Exceptions**: The class prioritizes handling specific exceptions (`ConstraintViolationException` and `IllegalArgumentException`) to provide meaningful error responses tailored to the exception type.
- **Generic Exceptions**: A fallback mechanism is implemented to handle all other exceptions, ensuring the application does not crash unexpectedly.

### HTTP Status Codes
The class uses the following HTTP status codes:
- **400 BAD_REQUEST**: Indicates client-side errors such as validation failures or illegal arguments.
- **500 INTERNAL_SERVER_ERROR**: Indicates server-side errors or unexpected issues.

### Logging
The `handleException` method includes a call to `e.printStackTrace()`, which logs the stack trace of the exception. This is useful for debugging but may need to be replaced with a proper logging framework in production environments.

### Scalability
The `GlobalExceptionHandler` class can be extended to handle additional exception types by adding more methods annotated with `@ExceptionHandler`.

### Dependencies
- **Spring Framework**: Provides annotations like `@ControllerAdvice` and `@ExceptionHandler`.
- **Jakarta Validation**: Used for handling `ConstraintViolationException`.

## File Metadata
| **File Name** | **Description**                     |
|---------------|-------------------------------------|
| `GlobalExceptionHandler.java` | Centralized exception handling for a Spring Boot application. |


---
<div style="page-break-after: always;"></div>

# Documentation: `ErrorResponse` Class

## Overview
The `ErrorResponse` class is a simple data structure designed to encapsulate error information. It provides a way to represent error details using a code and a message, which can be useful for error handling in applications, particularly in APIs or services.

---

## Class Details

### Package
The class is part of the package:
```
com.example.supplier
```

### Purpose
The `ErrorResponse` class is used to represent error details in a structured format. It contains two fields:
- `code`: A string representing the error code.
- `message`: A string representing the error message.

This class is typically used to communicate error information between different layers of an application or to external clients.

---

## Fields

| Field Name | Type   | Description                          |
|------------|--------|--------------------------------------|
| `code`     | String | Represents the error code.          |
| `message`  | String | Represents the error message.       |

---

## Constructors

| Constructor Signature                          | Description                                      |
|------------------------------------------------|--------------------------------------------------|
| `ErrorResponse(String code, String message)`   | Initializes the `ErrorResponse` object with the provided `code` and `message`. |

---

## Methods

| Method Name          | Return Type | Description                                      |
|-----------------------|-------------|--------------------------------------------------|
| `getCode()`           | `String`    | Retrieves the value of the `code` field.        |
| `setCode(String code)`| `void`      | Sets the value of the `code` field.             |
| `getMessage()`        | `String`    | Retrieves the value of the `message` field.     |
| `setMessage(String message)` | `void` | Sets the value of the `message` field.          |

---

## Insights

1. **Encapsulation**: The class uses private fields with public getter and setter methods, adhering to the principle of encapsulation.
2. **Reusability**: This class can be reused across different parts of an application to standardize error handling.
3. **Simplicity**: The class is straightforward and focuses solely on representing error information, making it lightweight and easy to use.
4. **Potential Use Cases**:
   - Returning error responses in REST APIs.
   - Logging error details in a structured format.
   - Communicating error information between application layers.


---
<div style="page-break-after: always;"></div>

# SupplierApplication Documentation

## Overview

The `SupplierApplication` is a Spring Boot application that serves as the entry point for the application. It includes configuration for enabling Cross-Origin Resource Sharing (CORS) to allow requests from different origins. This configuration is essential for enabling communication between the backend and frontend or other external services.

---

## File Metadata

- **File Name**: `SupplierApplication.java`
- **Package**: `com.example.supplier`

---

## Code Structure

### 1. **Main Class**
   - **Class Name**: `SupplierApplication`
   - **Annotations**:
     - `@SpringBootApplication`: Marks this class as the main entry point for the Spring Boot application. It combines the functionality of `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`.

   - **Main Method**:
     - The `main` method uses `SpringApplication.run()` to bootstrap the application.

### 2. **CORS Configuration**
   - **Method**: `corsConfigurer`
   - **Annotation**: `@Bean`
     - Registers the method as a Spring Bean, making it available in the application context.
   - **Purpose**: Configures CORS settings for the application.
   - **Implementation**:
     - Overrides the `addCorsMappings` method of `WebMvcConfigurer` to define CORS rules.
     - **CORS Rules**:
       - **Path Pattern**: `/**` (applies to all endpoints).
       - **Allowed Origins**: `*` (allows requests from any origin).
       - **Allowed Methods**: `GET`, `POST`, `PUT`, `DELETE`, `OPTIONS`.
       - **Allowed Headers**: `*` (allows all headers).
       - **Allow Credentials**: Commented out in the code (`.allowCredentials(true)`).

---

## Insights

### 1. **Spring Boot Application**
   - The `@SpringBootApplication` annotation simplifies the configuration and setup of the application by combining multiple annotations into one.

### 2. **CORS Configuration**
   - The `corsConfigurer` method ensures that the application can handle cross-origin requests, which is critical for modern web applications where the frontend and backend often reside on different domains.
   - The configuration is highly permissive (`*` for origins, headers, and multiple HTTP methods), which may be suitable for development but should be reviewed for production environments to avoid security risks.

### 3. **Extensibility**
   - The use of `WebMvcConfigurer` allows for easy extension and customization of web-related configurations in the future.

### 4. **Commented Code**
   - The `.allowCredentials(true)` line is commented out. If enabled, it would allow cookies and other credentials to be sent with cross-origin requests. This should be carefully considered based on the application's security requirements.

---

## Key Components

| Component                | Description                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| `@SpringBootApplication` | Marks the class as the main entry point for the Spring Boot application.   |
| `SpringApplication.run`  | Bootstraps the application.                                                |
| `@Bean`                  | Registers the `corsConfigurer` method as a Spring Bean.                   |
| `WebMvcConfigurer`       | Interface used to customize web-related configurations.                   |
| `addCorsMappings`        | Configures CORS rules for the application.                                |

---

## Recommendations

- **Security**: Review the permissive CORS settings (`*` for origins, headers, and methods) before deploying to production. Restrict origins and methods as needed.
- **Credentials**: If `.allowCredentials(true)` is required, ensure that the `allowedOrigins` is not set to `*` as it will cause a runtime error in Spring Boot. Use specific origins instead.


---
<div style="page-break-after: always;"></div>

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


---
<div style="page-break-after: always;"></div>

# Documentation: Supplier.java

## Overview
The `Supplier` class is a data structure representing a supplier entity in a system. It is annotated with JPA (Jakarta Persistence API) annotations to map it to a database table. This class contains fields for supplier details such as name, contact information, and a unique identifier.

## Metadata
- **File Name**: `Supplier.java`
- **Package**: `com.example.supplier.model`

## Class Details

### Annotations
- **`@Entity`**: Marks the class as a JPA entity, indicating that it is mapped to a database table.
- **`@Id`**: Specifies the primary key of the entity.
- **`@GeneratedValue(strategy = GenerationType.IDENTITY)`**: Configures the primary key to be auto-generated using the identity strategy.

### Fields
| Field Name       | Type    | Description                                                                 |
|------------------|---------|-----------------------------------------------------------------------------|
| `id`             | `Long`  | Unique identifier for the supplier. Auto-generated by the database.         |
| `nome`           | `String`| Name of the supplier.                                                       |
| `cnpj`           | `long`  | Brazilian company registration number (CNPJ).                              |
| `nomeContato`    | `String`| Name of the contact person for the supplier.                                |
| `emailContato`   | `String`| Email address of the contact person.                                        |
| `telefoneContato`| `String`| Phone number of the contact person.                                         |

### Methods
| Method Name            | Return Type | Description                                                                 |
|------------------------|-------------|-----------------------------------------------------------------------------|
| `getId()`              | `Long`      | Retrieves the unique identifier of the supplier.                           |
| `setId(Long id)`       | `void`      | Sets the unique identifier of the supplier.                                |
| `getNome()`            | `String`    | Retrieves the name of the supplier.                                        |
| `setNome(String nome)` | `void`      | Sets the name of the supplier.                                             |
| `getCnpj()`            | `long`      | Retrieves the CNPJ of the supplier.                                        |
| `setCnpj(long cnpj)`   | `void`      | Sets the CNPJ of the supplier.                                             |
| `getNomeContato()`     | `String`    | Retrieves the name of the contact person.                                  |
| `setNomeContato(String nomeContato)` | `void` | Sets the name of the contact person.                                      |
| `getEmailContato()`    | `String`    | Retrieves the email address of the contact person.                         |
| `setEmailContato(String emailContato)` | `void` | Sets the email address of the contact person.                             |
| `getTelefoneContato()` | `String`    | Retrieves the phone number of the contact person.                          |
| `setTelefoneContato(String telefoneContato)` | `void` | Sets the phone number of the contact person.                              |

## Insights
- **Database Integration**: The class is designed to integrate seamlessly with a relational database using JPA annotations. The `@GeneratedValue` annotation ensures that the `id` field is automatically managed by the database.
- **Encapsulation**: The class uses getter and setter methods to encapsulate its fields, promoting data integrity and controlled access.
- **Brazilian Context**: The inclusion of the `cnpj` field suggests that the application is tailored for Brazilian businesses, as CNPJ is specific to Brazil.
- **Contact Information**: The class provides fields for storing detailed contact information, making it suitable for applications that require communication with suppliers.


---
<div style="page-break-after: always;"></div>

# Documentation: SupplierRepository.java

## Overview
The `SupplierRepository` interface is a data structure that serves as a repository for managing `Supplier` entities. It leverages Spring Data JPA to provide CRUD operations and database interaction capabilities without requiring explicit implementation. This interface is annotated with `@Repository`, marking it as a Spring-managed component.

## Key Features
- **Entity Management**: Handles persistence operations for the `Supplier` entity.
- **Spring Data JPA Integration**: Utilizes the `JpaRepository` interface to inherit standard database operations.
- **Type Safety**: Operates on `Supplier` entities with a primary key of type `Long`.

## Code Structure

### Package
The class is part of the `com.example.supplier.repository` package, which likely organizes repository-related components for the application.

### Imports
| **Import**                          | **Purpose**                                                                 |
|-------------------------------------|-----------------------------------------------------------------------------|
| `com.example.supplier.model.Supplier` | Represents the entity managed by this repository.                          |
| `org.springframework.data.jpa.repository.JpaRepository` | Provides CRUD and query methods for database interaction.                  |
| `org.springframework.stereotype.Repository` | Marks the interface as a Spring-managed repository component.             |

### Interface Declaration
```java
@Repository
public interface SupplierRepository extends JpaRepository<Supplier, Long> {
}
```

#### Annotations
- **`@Repository`**: Indicates that this interface is a Spring repository, enabling exception translation and dependency injection.

#### Extension
- **`JpaRepository<Supplier, Long>`**: 
  - `Supplier`: The entity type managed by this repository.
  - `Long`: The type of the primary key for the `Supplier` entity.

## Insights
- **No Custom Methods**: The interface does not define any custom query methods, relying entirely on the default methods provided by `JpaRepository`.
- **Scalability**: Additional query methods can be added using method naming conventions or custom implementations if needed.
- **Spring Boot Compatibility**: This repository is designed to work seamlessly with Spring Boot applications, leveraging auto-configuration and dependency injection.

## Usage
The `SupplierRepository` can be injected into service classes or controllers to perform database operations on `Supplier` entities, such as:
- Saving a new supplier.
- Retrieving suppliers by ID.
- Updating supplier details.
- Deleting suppliers.

Example:
```java
@Autowired
private SupplierRepository supplierRepository;

Supplier supplier = supplierRepository.findById(1L).orElse(null);
supplierRepository.save(new Supplier(...));
supplierRepository.deleteById(1L);
```


---
<div style="page-break-after: always;"></div>

# SupplierService Documentation

## Overview

The `SupplierService` class is a service layer component in a Spring-based application. It provides business logic for managing `Supplier` entities, including creating, retrieving, updating, and deleting suppliers. The service interacts with the `SupplierRepository` for database operations and uses utility methods for validation.

---

## Class Details

### Package
`com.example.supplier.service`

### Annotations
- `@Service`: Marks this class as a Spring service component, making it eligible for component scanning and dependency injection.

### Dependencies
- **`SupplierRepository`**: Handles database operations for `Supplier` entities.
- **`CodigoUtil`**: Provides utility methods, such as validating CNPJ (Brazilian company registration numbers).

---

## Methods

### 1. `createSupplier(Supplier supplier)`
Creates a new supplier in the database after validating the CNPJ.

- **Parameters**:
  - `supplier`: The `Supplier` object to be created.
- **Returns**:
  - The saved `Supplier` object.
- **Throws**:
  - `IllegalArgumentException` if the CNPJ is invalid.
- **Logic**:
  - Validates the CNPJ using `CodigoUtil.isValidCNPJ`.
  - Saves the supplier using `supplierRepository.save`.

---

### 2. `getAllSuppliers()`
Retrieves all suppliers from the database.

- **Returns**:
  - A `List<Supplier>` containing all suppliers.
- **Logic**:
  - Fetches all suppliers using `supplierRepository.findAll`.

---

### 3. `getSupplierById(Long id)`
Fetches a supplier by its ID.

- **Parameters**:
  - `id`: The ID of the supplier to retrieve.
- **Returns**:
  - An `Optional<Supplier>` containing the supplier if found.
- **Logic**:
  - Uses `supplierRepository.findById` to fetch the supplier.

---

### 4. `updateSupplier(Long id, Supplier supplierDetails)`
Updates an existing supplier's details.

- **Parameters**:
  - `id`: The ID of the supplier to update.
  - `supplierDetails`: A `Supplier` object containing the updated details.
- **Returns**:
  - The updated `Supplier` object.
- **Throws**:
  - `IllegalArgumentException` if the CNPJ is invalid.
  - `RuntimeException` if the supplier with the given ID is not found.
- **Logic**:
  - Validates the CNPJ using `CodigoUtil.isValidCNPJ`.
  - Fetches the supplier by ID.
  - Updates the supplier's attributes (e.g., name, contact details).
  - Saves the updated supplier using `supplierRepository.save`.

---

### 5. `deleteSupplier(Long id)`
Deletes a supplier by its ID.

- **Parameters**:
  - `id`: The ID of the supplier to delete.
- **Returns**:
  - `true` if the deletion is successful.
- **Throws**:
  - `RuntimeException` if the supplier with the given ID is not found.
- **Logic**:
  - Fetches the supplier by ID.
  - Deletes the supplier using `supplierRepository.deleteById`.

---

## Insights

### Validation
- The service ensures data integrity by validating the CNPJ using `CodigoUtil.isValidCNPJ` before creating or updating a supplier.

### Exception Handling
- The service throws meaningful exceptions (`IllegalArgumentException` and `RuntimeException`) to handle invalid data and missing entities.

### Dependency Injection
- The `SupplierRepository` is injected using `@Autowired`, adhering to Spring's dependency injection principles.

### CRUD Operations
- The service provides full CRUD (Create, Read, Update, Delete) functionality for `Supplier` entities.

### Reusability
- The service is designed to be reusable and can be easily extended or modified to include additional business logic.

---

## Method Summary Table

| Method Name           | Purpose                              | Parameters                     | Returns                  | Exceptions                     |
|-----------------------|--------------------------------------|--------------------------------|--------------------------|--------------------------------|
| `createSupplier`      | Creates a new supplier              | `Supplier supplier`            | `Supplier`               | `IllegalArgumentException`    |
| `getAllSuppliers`     | Retrieves all suppliers             | None                           | `List<Supplier>`         | None                           |
| `getSupplierById`     | Fetches a supplier by ID            | `Long id`                      | `Optional<Supplier>`     | None                           |
| `updateSupplier`      | Updates an existing supplier        | `Long id`, `Supplier details`  | `Supplier`               | `IllegalArgumentException`, `RuntimeException` |
| `deleteSupplier`      | Deletes a supplier by ID            | `Long id`                      | `boolean`                | `RuntimeException`             |

---


---
<div style="page-break-after: always;"></div>

# Documentation: `CodigoUtil.java`

## Overview
The `CodigoUtil` class provides utility methods for validating Brazilian CNPJ numbers. A CNPJ (Cadastro Nacional da Pessoa Jurídica) is a unique identifier assigned to companies in Brazil. This class includes logic to verify the validity of a CNPJ based on its checksum calculation.

---

## Class: `CodigoUtil`

### Package
The class is part of the package:
```
com.example.supplier.util
```

---

## Method Details

### `isValidCNPJ(long cnpj)`
#### Description
This method validates a given CNPJ number by performing checksum calculations based on predefined weights. It ensures the CNPJ adheres to the Brazilian standard for company identification numbers.

#### Parameters
| Name  | Type   | Description                          |
|-------|--------|--------------------------------------|
| `cnpj`| `long` | The CNPJ number to be validated.     |

#### Return Value
| Type      | Description                          |
|-----------|--------------------------------------|
| `boolean` | Returns `true` if the CNPJ is valid, otherwise `false`. |

#### Logic
1. Converts the `long` CNPJ into a 14-digit string.
2. Validates the length of the CNPJ string (must be 14 characters).
3. Performs checksum calculations using two sets of weights:
   - `weight1`: Used for the first digit validation.
   - `weight2`: Used for the second digit validation.
4. Calculates the first and second verification digits based on modulo 11 arithmetic.
5. Compares the calculated digits with the actual digits in the CNPJ.
6. Returns `false` if any exception occurs during processing.

#### Exception Handling
If an exception occurs (e.g., invalid input or unexpected errors), the method returns `false`.

---

### `main(String[] args)`
#### Description
A simple test method to demonstrate the usage of the `isValidCNPJ` method. It validates a hardcoded example CNPJ and prints the result to the console.

#### Parameters
| Name   | Type         | Description                          |
|--------|--------------|--------------------------------------|
| `args` | `String[]`   | Command-line arguments (not used).   |

---

## Insights

### CNPJ Validation Algorithm
The validation algorithm uses two sets of weights (`weight1` and `weight2`) to calculate checksum digits. These weights are applied to the first 12 and 13 digits of the CNPJ, respectively. The modulo 11 operation determines the verification digits:
- If the modulo result is less than 2, the verification digit is `0`.
- Otherwise, the verification digit is `11 - mod`.

### Example CNPJ
The example CNPJ used in the `main` method is `12345678000195`. This is a placeholder and may not represent a valid CNPJ.

### Error Handling
The method gracefully handles errors by returning `false` if any exception occurs during processing. This ensures robustness when dealing with invalid or malformed input.

### Limitations
- The method assumes the input CNPJ is numeric and does not handle non-numeric inputs.
- It does not validate the format of the CNPJ beyond its checksum.

---

## Dependencies
This class does not rely on external libraries or dependencies. It uses standard Java functionality such as:
- `String.format`
- `Character.getNumericValue`

---

## Example Usage
```java
public class TestCodigoUtil {
    public static void main(String[] args) {
        long cnpj = 12345678000195L; // Example CNPJ
        boolean isValid = CodigoUtil.isValidCNPJ(cnpj);
        System.out.println("CNPJ is valid: " + isValid);
    }
}
```

---

## Summary of Weights
| Weight Set | Values                                      |
|------------|---------------------------------------------|
| `weight1`  | `{5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2}`      |
| `weight2`  | `{6, 5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2}`   |


---
<div style="page-break-after: always;"></div>

# Documentation: `SupplierApplicationTests.java`

## Overview
The `SupplierApplicationTests` class is a test class designed to verify the context loading of a Spring Boot application. It uses the `@SpringBootTest` annotation to bootstrap the application context for testing purposes. This class is part of the `com.example.supplier` package.

## Class Details

### Class: `SupplierApplicationTests`
| **Annotation**       | **Purpose**                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| `@SpringBootTest`     | Indicates that the class is a Spring Boot test and loads the application context for testing. |

#### Method: `contextLoads`
| **Annotation** | **Purpose**                                                                 |
|-----------------|-----------------------------------------------------------------------------|
| `@Test`         | Marks the method as a test case to be executed by the JUnit framework.     |

- **Functionality**: The `contextLoads` method is a placeholder test that checks if the Spring application context loads successfully. It does not contain any logic or assertions, serving as a basic sanity check for the application's configuration.

## Insights
- **Purpose of the Test**: The `contextLoads` method is commonly used in Spring Boot applications to ensure that the application context is correctly set up and can be loaded without errors. This is a fundamental test to verify the application's configuration integrity.
- **Scalability**: While the current test is minimal, additional test methods can be added to this class to verify specific components or behaviors within the application.
- **Frameworks Used**:
  - **JUnit 5**: The test is written using JUnit 5 (`org.junit.jupiter.api.Test`), which is the latest version of JUnit and provides enhanced features for testing.
  - **Spring Boot Test**: The `@SpringBootTest` annotation is part of the Spring Boot testing framework, enabling integration testing with the application context.

## Limitations
- The `contextLoads` method does not perform any assertions or validations beyond checking the application context's ability to load. It does not test specific functionality or business logic.
- No additional test cases are provided in this class, limiting its utility to a basic context validation.


---
<div style="page-break-after: always;"></div>

# Documentation

## Overview

This code is the entry point for a React application. It initializes the React application by rendering the root component (`App`) into the DOM. The file also imports necessary dependencies and applies strict mode to enforce best practices and catch potential issues during development.

---

## File Metadata

| **Attribute** | **Value**         |
|---------------|-------------------|
| **File Name** | `index.js`        |

---

## Code Structure

### Imports

The following modules and files are imported:

| **Import**         | **Description**                                                                 |
|---------------------|---------------------------------------------------------------------------------|
| `React`            | Core library for building user interfaces.                                     |
| `ReactDOM`         | Provides methods to render React components into the DOM.                      |
| `App`              | The root component of the application, imported from `./App`.                  |
| `./index.css`      | CSS file for global styling of the application.                                |

---

### Logic

The code contains the following logic:

1. **React.StrictMode**:
   - Wraps the `App` component to enable additional checks and warnings during development.
   - Helps identify unsafe lifecycle methods, deprecated APIs, and other potential issues.

2. **Rendering**:
   - The `ReactDOM.render()` method is used to render the `App` component into the DOM element with the ID `root`.
   - This connects the React application to the HTML file, typically `public/index.html`.

---

## Insights

- **Strict Mode**:
  - Using `React.StrictMode` is a best practice for modern React applications. It ensures that the application adheres to React's recommended practices and helps developers identify issues early in the development process.

- **Separation of Concerns**:
  - The code follows the principle of separation of concerns by importing the `App` component and a separate CSS file for styling. This modular approach improves maintainability.

- **Entry Point**:
  - This file serves as the entry point for the React application, connecting the React component tree to the DOM.

- **Global Styling**:
  - The inclusion of `index.css` suggests that global styles are applied to the application, which can be overridden or extended by component-specific styles.

---

## Dependencies

| **Dependency** | **Purpose**                                                                 |
|-----------------|-----------------------------------------------------------------------------|
| `react`         | Provides the core functionality for building React components.             |
| `react-dom`     | Enables rendering of React components into the DOM.                        |

---

## Key Functions

| **Function**         | **Description**                                                                 |
|-----------------------|---------------------------------------------------------------------------------|
| `ReactDOM.render()`   | Renders the React component tree into the specified DOM element (`root`).       |

---

## DOM Interaction

| **Element ID** | **Purpose**                                                                 |
|-----------------|-----------------------------------------------------------------------------|
| `root`          | Serves as the container for the React application.                         |


---
<div style="page-break-after: always;"></div>

# Documentation: App.js

## Overview
The `App.js` file serves as the entry point for a React application focused on supplier management. It integrates components and services to provide a user interface for managing suppliers. The application includes a form for adding new suppliers and a list to display existing suppliers.

---

## Components Used

### SupplierForm
- **Purpose**: Handles the creation of new suppliers.
- **Location**: Imported from `./components/SupplierForm`.

### SupplierList
- **Purpose**: Displays a list of all suppliers.
- **Location**: Imported from `./components/SupplierList`.

---

## Services Used

### getAllSuppliers
- **Purpose**: Fetches all supplier data from the backend or external service.
- **Location**: Imported from `./services/supplierService`.

### createSupplier
- **Purpose**: Sends data to create a new supplier in the backend or external service.
- **Location**: Imported from `./services/supplierService`.

---

## Code Logic

### App Component
- **Type**: Functional Component.
- **Purpose**: Acts as the main container for the supplier management application.
- **Structure**:
  - Renders a header (`<h1>Supplier Management`).
  - Includes the `SupplierForm` component for adding suppliers.
  - Includes the `SupplierList` component for displaying suppliers.

---

## Insights

- **Component Composition**: The application follows a modular design by separating the form and list functionalities into distinct components (`SupplierForm` and `SupplierList`).
- **Service Integration**: Although services (`getAllSuppliers` and `createSupplier`) are imported, they are not directly utilized within the `App.js` file. Their usage is likely encapsulated within the respective components (`SupplierForm` and `SupplierList`).
- **Scalability**: The structure allows for easy extension, such as adding new features or integrating additional services.
- **Styling**: The application uses a CSS class `App` for styling, indicating potential customization through external or inline styles.

---

## File Metadata

| **Attribute**   | **Value**           |
|------------------|---------------------|
| **File Name**    | `App.js`           |
| **Primary Role** | Entry point for the React application |


---
<div style="page-break-after: always;"></div>

# Documentation: SupplierForm Component

## Overview
The `SupplierForm` component is a React functional component designed to create a supplier by collecting relevant information such as name, CNPJ (Brazilian company registration number), contact name, contact email, and contact phone number. It includes validation logic for the CNPJ field and handles form submission to send the supplier data to a backend service.

---

## Features
- **Form Fields**: Collects supplier details including:
  - `nome`: Supplier's name.
  - `cnpj`: Supplier's CNPJ (validated for correctness).
  - `nomeContato`: Contact person's name.
  - `emailContato`: Contact person's email.
  - `telefoneContato`: Contact person's phone number.
- **CNPJ Validation**: Ensures the CNPJ is valid using custom logic.
- **Error Handling**: Displays error messages for invalid input or failed submission.
- **Integration**: Sends supplier data to a backend service using the `createSupplier` function.

---

## Code Structure

### State Management
The component uses React's `useState` hook to manage:
- `supplier`: An object containing the form fields.
- `error`: A string to store error messages.

### Form Validation
- **Required Fields**: All fields are mandatory.
- **CNPJ Validation**: The `validateCNPJ` function ensures the CNPJ is valid by:
  - Removing non-numeric characters.
  - Checking the length (must be 14 digits).
  - Performing mathematical checks on the digits.

### Form Submission
- Prevents default form submission behavior.
- Validates all fields and the CNPJ.
- Sends the supplier data to the backend using the `createSupplier` function.
- Resets the form on successful submission.
- Displays error messages for invalid input or submission failure.

---

## Key Functions

### `handleChange`
Handles input changes for form fields. Updates the `supplier` state dynamically based on the field name.

### `validateCNPJ`
Validates the CNPJ field using the following steps:
1. Removes non-numeric characters.
2. Checks if the length is exactly 14 digits.
3. Performs mathematical checks on the first and second verification digits.

### `handleSubmit`
Handles form submission:
1. Prevents default behavior.
2. Validates required fields and CNPJ.
3. Sends data to the backend using `createSupplier`.
4. Resets the form on success or displays error messages on failure.

---

## Dependencies
- **React**: For building the component and managing state.
- **react-input-mask**: Provides input masking for the CNPJ field.
- **supplierService**: Contains the `createSupplier` function for backend integration.

---

## Insights

### Validation Logic
The CNPJ validation logic is robust and ensures compliance with Brazilian standards. However, it could be refactored into a utility function for reusability across multiple components.

### Error Handling
The error handling mechanism is simple but effective. It could be enhanced by providing more detailed error messages from the backend.

### Input Masking
The use of `react-input-mask` for the CNPJ field improves user experience by enforcing the correct format during input.

### Scalability
The component is designed for a single form submission. If additional fields or complex validation rules are required, the code may need refactoring to maintain readability and scalability.

---

## Example Usage
```jsx
import SupplierForm from './SupplierForm';

function App() {
    return (
        <div>
            <SupplierForm />
        </div>
    );
}

export default App;
```

---

## File Metadata
- **File Name**: `SupplierForm.js`
- **Purpose**: React component for creating a supplier with validation and backend integration.


---
<div style="page-break-after: always;"></div>

# Documentation: SupplierList Component

## Overview
The `SupplierList` component is a React functional component designed to display a list of suppliers. It fetches supplier data from an external service and renders it in a structured format. The component also provides functionality to reload the supplier list.

---

## Features
- **Fetch Supplier Data**: Retrieves supplier information from an external service using the `getAllSuppliers` function.
- **Display Supplier List**: Renders supplier details including name, CNPJ, contact name, contact email, and contact phone.
- **Reload Functionality**: Allows users to manually reload the supplier list by clicking a button.

---

## Code Structure

### State Management
- **`suppliers`**: A state variable initialized as an empty array. It stores the list of suppliers fetched from the service.

### Lifecycle Methods
- **`useEffect`**: Executes the `fetchSuppliers` function when the component is mounted to fetch the initial supplier data.

### Functions
| Function Name   | Description                                                                 |
|-----------------|-----------------------------------------------------------------------------|
| `fetchSuppliers`| Asynchronously fetches supplier data using the `getAllSuppliers` service. Handles errors gracefully by logging them to the console. |

### JSX Structure
- **Header**: Displays the title "Supplier List".
- **Reload Button**: A button to manually trigger the `fetchSuppliers` function.
- **Supplier List**: An unordered list (`<ul>`) that maps over the `suppliers` state and displays each supplier's details in a list item (`<li>`).

---

## Dependencies
| Dependency Name       | Purpose                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| `React`               | Provides the core functionality for building the component.            |
| `useEffect`           | React hook used for side effects, such as fetching data on mount.      |
| `useState`            | React hook used for managing component state.                          |
| `getAllSuppliers`     | Service function to fetch supplier data from an external source.       |
| `createSupplier`      | Imported but not used in this component.                              |

---

## Insights
1. **Error Handling**: The `fetchSuppliers` function logs errors to the console but does not provide user feedback. Consider implementing a user-friendly error message or notification system.
2. **Unused Import**: The `createSupplier` function is imported but not utilized in the component. If not needed, it should be removed to improve code clarity.
3. **Dynamic Reload**: The reload button provides a simple way to refresh the supplier list, but it does not indicate loading status. Adding a loading spinner or disabled state during data fetching could enhance user experience.
4. **Data Structure**: The supplier object is expected to have the following fields:
   - `id`: Unique identifier for the supplier.
   - `nome`: Name of the supplier.
   - `cnpj`: CNPJ (Brazilian company registration number).
   - `nomeContato`: Name of the contact person.
   - `emailContato`: Email of the contact person.
   - `telefoneContato`: Phone number of the contact person.
5. **Scalability**: If the supplier list grows significantly, consider implementing pagination or infinite scrolling for better performance and usability.

---

## File Metadata
| Key       | Value              |
|-----------|--------------------|
| File Name | `SupplierList.js` |


---
<div style="page-break-after: always;"></div>

# Documentation: Supplier Service

## Overview
This module provides utility functions to interact with a supplier management API. It includes methods for retrieving all suppliers and creating new suppliers. The API is hosted on a server defined by the `serverUrl` constant.

---

## Functions

### `getAllSuppliers()`
Fetches all suppliers from the API.

#### **Details**
- **URL**: `http://localhost:8081/api/suppliers`
- **HTTP Method**: `GET`
- **Response Handling**: 
  - If the response is not successful (`response.ok` is `false`), an error is thrown with the message: `'Failed to fetch suppliers'`.
  - If successful, the response is parsed as JSON and returned.

#### **Usage**
```javascript
getAllSuppliers()
  .then(suppliers => console.log(suppliers))
  .catch(error => console.error(error));
```

---

### `createSupplier(supplier)`
Creates a new supplier by sending supplier data to the API.

#### **Details**
- **URL**: `http://localhost:8081/api/suppliers`
- **HTTP Method**: `POST`
- **Headers**:
  - `Content-Type`: `application/json`
- **Body**:
  - The supplier object is cleaned before being sent. Specifically, the `cnpj` field is stripped of all non-numeric characters using the regex `/\D/g`.
  - The cleaned supplier object is serialized into JSON format and sent in the request body.
- **Response Handling**:
  - If the response is not successful (`response.ok` is `false`), an error is thrown with the message: `'Failed to create supplier'`.
  - If successful, the response is parsed as JSON and returned.

#### **Parameters**
| Parameter | Type   | Description                          |
|-----------|--------|--------------------------------------|
| `supplier`| Object | The supplier data to be sent to the API. |

#### **Usage**
```javascript
const newSupplier = {
    name: 'Supplier Name',
    cnpj: '12.345.678/0001-90',
    address: '123 Supplier Street'
};

createSupplier(newSupplier)
  .then(createdSupplier => console.log(createdSupplier))
  .catch(error => console.error(error));
```

---

## Insights

1. **Error Handling**:
   - Both functions include error handling for unsuccessful API responses. This ensures that the application can gracefully handle issues such as network errors or server-side failures.

2. **Data Cleaning**:
   - The `createSupplier` function demonstrates a preprocessing step where the `cnpj` field is cleaned to remove non-numeric characters. This ensures that the data sent to the API is in the expected format.

3. **Modular Design**:
   - The functions are designed to be reusable and modular, making them easy to integrate into larger applications.

4. **Asynchronous Operations**:
   - Both functions use `async/await` for handling asynchronous operations, which simplifies the code and improves readability.

5. **Server URL Configuration**:
   - The `serverUrl` is defined as a constant, making it easy to update the base URL if the server location changes.

6. **Potential Enhancements**:
   - Adding validation for the `supplier` object in the `createSupplier` function could prevent invalid data from being sent to the API.
   - Implementing retry logic for failed requests could improve robustness in case of transient network issues.


---
<div style="page-break-after: always;"></div>

