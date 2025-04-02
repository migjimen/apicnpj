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
