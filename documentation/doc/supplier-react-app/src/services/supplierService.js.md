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
