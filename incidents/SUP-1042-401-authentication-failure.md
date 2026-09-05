## API Investigation

The issue was reproduced using Postman.

### Request

```http
POST /v1/customers
Authorization: Bearer expired_token_123
Content-Type: application/json
```

### Request Body

```json
{
  "firstName": "John",
  "lastName": "Smith",
  "email": "john.smith@example.com",
  "company": "ABC Technologies"
}
```

### API Response

```http
401 Unauthorized
```

```json
{
  "error": "invalid_token",
  "message": "The access token has expired."
}
```

## Investigation Findings

The following checks were performed:

1. Confirmed the API endpoint was reachable.
2. Reproduced the failure in Postman.
3. Reviewed the HTTP status code.
4. Inspected the API response body.
5. Verified the Authorization header.
6. Identified that the configured access token had expired.

## Root Cause

The CRM integration was using an expired authentication token.

### Contributing Factor

The integration did not have an effective token-expiration monitoring or automatic refresh mechanism.

## Resolution

1. Obtained a valid authentication token.
2. Updated the integration configuration.
3. Re-ran the API request in Postman.
4. Verified that the request completed successfully.
5. Confirmed customer record creation.

## Successful Validation

The API request returned:

```http
201 Created
```

The customer record was successfully created and synchronization was validated.

## Preventive Recommendation

Implement authentication-token monitoring and automated token refresh where supported.

## Support Skills Demonstrated

- API incident investigation
- REST API troubleshooting
- HTTP status-code analysis
- Authentication troubleshooting
- JSON request/response analysis
- Root-cause analysis
- Resolution validation
- Technical documentation
