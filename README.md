
# STX-name-registry - Name Registry and Marketplace Smart Contract

## Overview

This smart contract provides a decentralized name registry and marketplace on the **Stacks blockchain**, where users can:

* Register unique names
* Set validity periods for their names
* List names for sale
* Buy listed names from others

The contract includes robust name validation logic and pricing mechanisms to ensure fair and secure operation.

---

## Features

✅ Register unique ASCII names (letters, numbers, hyphen)
✅ Enforce character validation for names
✅ Set base registration fees
✅ Support marketplace listings and purchases
✅ Enforce minimum and maximum validity periods
✅ Modular error handling with predefined codes

---

## 🛠️ Constants

```clojure
(define-constant ADMIN-ACCOUNT tx-sender)
(define-constant ERR-UNAUTHORIZED (err u100))
(define-constant ERR-NAME-UNAVAILABLE (err u101))
(define-constant ERR-NAME-NOT-FOUND (err u102))
(define-constant ERR-INVALID-NAME (err u103))
(define-constant ERR-TRANSACTION-FAILED (err u104))
(define-constant ERR-PAYMENT-REQUIRED (err u105))
```

---

## 🗂 Data Structures

### `name-registry` (Map)

Stores registered names with:

* `holder` – principal who owns the name
* `validity` – uint timestamp until when the name is valid
* `listing-amount` – uint price if listed for sale

### `name-marketplace` (Map)

Stores purchase offers with:

* `buyer` – principal offering to buy
* `purchase-amount` – amount offered

---

## 📊 Data Variables

* `base-fee` – Default registration fee (e.g., `u10000000` = 0.1 STX)
* `min-validity-period` – Minimum validity (1 year in seconds)
* `max-validity-period` – Maximum validity (5 years in seconds)

---

## 🧮 Utility Functions

### Character Validations

* `is-lowercase-letter(char)` – Verifies lowercase alphabet
* `is-number(char)` – Verifies numeric character
* `is-valid-character(char)` – Allows letters, numbers, and `-`

### Name Validity Checks

* `check-name-char(name, index)` – Checks one character at a specific index
* Grouped character checks: `validate-chars-group-1` through `validate-chars-group-5`

  * Ensures up to 64 characters are validated (due to Clarity’s recursion limits)

### Time

* `current-time()` – Gets current block height (used as a timestamp)

---

## 🔐 Access Control

Currently, the only access control is for administrative actions using:

```clojure
(define-constant ADMIN-ACCOUNT tx-sender)
```

> You can extend this with additional `is-admin` checks as needed.

---

## ❌ Error Codes

| Error Constant           | Code       | Meaning                         |
| ------------------------ | ---------- | ------------------------------- |
| `ERR-UNAUTHORIZED`       | `err u100` | Admin-only action violated      |
| `ERR-NAME-UNAVAILABLE`   | `err u101` | Name already registered         |
| `ERR-NAME-NOT-FOUND`     | `err u102` | Name does not exist             |
| `ERR-INVALID-NAME`       | `err u103` | Name format is not valid        |
| `ERR-TRANSACTION-FAILED` | `err u104` | Transfer failed                 |
| `ERR-PAYMENT-REQUIRED`   | `err u105` | Payment insufficient or missing |

---

## 📦 Functions Overview

| Function                 | Type      | Description                         |
| ------------------------ | --------- | ----------------------------------- |
| `current-time`           | Read-Only | Returns current block height        |
| `is-lowercase-letter`    | Read-Only | Checks for lowercase ASCII letter   |
| `is-number`              | Read-Only | Checks for numeric character        |
| `is-valid-character`     | Read-Only | Checks if character is valid        |
| `check-name-char`        | Private   | Verifies a character in a string    |
| `validate-chars-group-X` | Private   | Groups of character checks for name |

> **Note**: Public functions for registration, listing, purchasing, and renewal are not yet implemented in the code you provided. You may want to add those based on your use case.

---

