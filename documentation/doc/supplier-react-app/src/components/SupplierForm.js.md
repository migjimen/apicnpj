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
