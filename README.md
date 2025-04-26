# Authentication Utilities

A secure Node.js authentication utility package providing password hashing and JWT (JSON Web Token) functionality.

## Features

- **Password Utilities**
  - Secure password hashing using PBKDF2
  - Random salt generation for each password
  - Constant-time password verification
  - Protection against timing attacks

- **JWT Utilities**
  - JWT token generation with customizable expiration
  - Secure token verification
  - Base64URL encoding/decoding
  - Signature validation using HMAC-SHA256

## Installation

```bash
npm install
```

## Usage

### Password Utilities

```javascript
const { hashPassword, verifyPassword } = require('./password-utils');

// Hash a password
const password = 'MySecurePassword123!';
const hashedPassword = hashPassword(password);

// Verify a password
const isValid = verifyPassword(password, hashedPassword);
```

### JWT Utilities

```javascript
const { signJWT, verifyJWT } = require('./jwt-utils');

// Create a JWT
const payload = { userId: '123', role: 'admin' };
const secret = 'yourSecretKey';
const token = signJWT(payload, secret, 3600); // Expires in 1 hour

// Verify a JWT
const decodedPayload = verifyJWT(token, secret);
```

## Security Features

- PBKDF2 with 100,000 iterations for password hashing
- 512-bit hash length
- 128-bit random salt for each password
- Constant-time comparison for password verification
- HMAC-SHA256 for JWT signatures
- Automatic token expiration handling

## API Reference

### Password Utilities

#### `hashPassword(password)`
- **Parameters**: `password` (string)
- **Returns**: String in format `salt:hash`
- **Throws**: TypeError if password is not a string

#### `verifyPassword(password, storedHash)`
- **Parameters**: 
  - `password` (string)
  - `storedHash` (string) - The stored hash in format `salt:hash`
- **Returns**: Boolean
- **Throws**: TypeError if parameters are invalid

### JWT Utilities

#### `signJWT(payload, secret, expiresInSeconds)`
- **Parameters**:
  - `payload` (object)
  - `secret` (string)
  - `expiresInSeconds` (number, default: 3600)
- **Returns**: JWT string
- **Throws**: TypeError for invalid parameters

#### `verifyJWT(token, secret)`
- **Parameters**:
  - `token` (string)
  - `secret` (string)
- **Returns**: Decoded payload object
- **Throws**: Error for invalid or expired tokens

## Running Tests

```bash
npm start
```

This will run the example code demonstrating both password and JWT functionality.

## Security Considerations

1. Always use strong secrets for JWT signing
2. Never store plain text passwords
3. Keep your secret keys secure and never commit them to version control
4. Regularly rotate JWT secrets in production
5. Set appropriate token expiration times
