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
