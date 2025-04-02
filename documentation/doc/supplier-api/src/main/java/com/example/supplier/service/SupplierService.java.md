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
