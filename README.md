Below is a simplified example of single sign-on (SSO) code using JSON Web Tokens (JWT) in Python without comments:

```python
import jwt
from datetime import datetime, timedelta

# Secret key for signing JWT
SECRET_KEY = 'secret'

# Generate JWT token
def generate_jwt_token(user_id):
    payload = {
        'user_id': user_id,
        'exp': datetime.utcnow() + timedelta(minutes=30)  # Token expires in 30 minutes
    }
    token = jwt.encode(payload, SECRET_KEY, algorithm='HS256')
    return token

# Verify JWT token
def verify_jwt_token(token):
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=['HS256'])
        return payload
    except jwt.ExpiredSignatureError:
        return {'error': 'Token has expired'}
    except jwt.InvalidTokenError:
        return {'error': 'Invalid token'}

# Example usage
if __name__ == "__main__":
    # Generate JWT token for user with ID = 123
    token = generate_jwt_token(123)
    print("Generated token:", token)

    # Verify JWT token
    decoded_token = verify_jwt_token(token)
    print("Decoded token:", decoded_token)
```

In this code:

- We use the `jwt` library to generate and verify JWT tokens.
- The `generate_jwt_token` function generates a JWT token with a payload containing the user ID and expiration time.
- The `verify_jwt_token` function verifies the JWT token and decodes the payload.
- We use a secret key (`SECRET_KEY`) for signing and verifying the JWT token.
- The example usage section demonstrates how to generate and verify a JWT token for a user with ID 123.

This is a basic example of using JWT for single sign-on in a distributed site. Actual implementation may involve additional security measures and integration with authentication systems.
