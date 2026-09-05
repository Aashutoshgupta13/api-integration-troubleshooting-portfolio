# SUP-1043 — CRM Customer Creation Failing with 400 Bad Request

> **Note:** This is a simulated technical support incident created for portfolio demonstration.

## Incident Summary

**Priority:** Medium  
**Status:** Resolved  
**System:** CRM → Customer Management REST API  
**Issue Type:** Invalid Request Payload

## Client Issue

The client reported that customer records were not being created in the external system.

The integration returned a `400 Bad Request` response when attempting to create a customer.

## Business Impact

- Customer records could not be created through the integration.
- Manual processing was required.
- The synchronization workflow was interrupted.

## API Investigation

The issue was reproduced using Postman.

### Request

```http
POST /v1/customers
Authorization: Bearer valid_test_token
Content-Type: application/json
```

### Request Body

```json
{
  "firstName": "John",
  "lastName": "Smith",
  "company": "ABC Technologies"
}
```

### API Response

```http
400 Bad Request
```

```json
{
  "error": "invalid_request",
  "message": "The email field is required."
}
```

## Investigation Findings

The following checks were performed:

1. Confirmed the API endpoint was reachable.
2. Reproduced the failure in Postman.
3. Reviewed the HTTP status code.
4. Inspected the API response body.
5. Compared the request payload with the expected customer data.
6. Identified that the required `email` field was missing.

## Root Cause

The request payload did not contain the required `email` field.

### Contributing Factor

The integration did not validate required fields before sending the request to the API.

## Resolution

1. Reviewed the required API fields.
2. Added the missing `email` field to the request payload.
3. Re-ran the request in Postman.
4. Verified that the request was accepted by the API.
5. Confirmed successful API-level validation.

## Successful Validation

The corrected request included:

```json
{
  "firstName": "John",
  "lastName": "Smith",
  "email": "john.smith@example.com",
  "company": "ABC Technologies"
}
```

The corrected request passed API-level validation.

## Preventive Recommendation

Implement client-side or integration-level validation for required fields before sending requests to the API.

## Support Skills Demonstrated

- REST API troubleshooting
- JSON payload analysis
- HTTP status-code analysis
- Request validation
- Root-cause analysis
- Incident investigation
- Resolution validation
- Technical documentation
