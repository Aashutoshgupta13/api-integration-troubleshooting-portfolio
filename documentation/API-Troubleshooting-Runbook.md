# API Troubleshooting Runbook

> This runbook is part of a simulated Technical Support and API Integration portfolio.

## Purpose

This document provides a structured approach for investigating common REST API integration failures.

The troubleshooting process follows:

**Client Issue → Reproduce → Investigate → Identify Root Cause → Resolve → Validate → Document**

---

## 1. Gather Incident Information

Before testing the API, collect:

- Client-reported symptoms
- Affected operation
- Approximate time of failure
- Example request or customer record
- HTTP status code, if available
- Error message
- Request ID or correlation ID, when available

---

## 2. Reproduce the Issue

Use Postman or another API testing tool to reproduce the reported behavior.

Confirm:

- HTTP method
- API endpoint
- Request headers
- Authentication
- Query parameters
- Request body
- Expected response
- Actual response

---

## 3. Analyze the HTTP Status Code

### 400 Bad Request

Usually indicates an invalid request.

Check:

- Required fields
- JSON syntax
- Data types
- Field names
- Request parameters

### 401 Unauthorized

Usually indicates an authentication problem.

Check:

- Authorization header
- Token validity
- Token expiration
- Authentication scheme

### 403 Forbidden

Usually indicates that authentication succeeded but the client does not have permission.

Check:

- User or application permissions
- API scopes
- Role configuration
- Endpoint access

### 404 Not Found

Check:

- Endpoint URL
- Resource ID
- API version
- Resource availability

### 500 Internal Server Error

Investigate:

- Server-side failure
- Upstream service failure
- Application logs
- Request/correlation ID

Escalate when the problem cannot be resolved from the support side.

### 503 Service Unavailable

Check:

- Service availability
- Maintenance status
- Upstream dependency
- Retry behavior

---

## 4. Authentication Troubleshooting

For a `401 Unauthorized` error:

1. Verify the Authorization header.
2. Confirm the authentication scheme.
3. Check token validity.
4. Check token expiration.
5. Obtain or refresh the token.
6. Retest the request.
7. Validate the successful response.

Example:

```http
Authorization: Bearer <token>
```

Never store real credentials, API keys, or access tokens in this repository.

---

## 5. Request Payload Validation

For `400 Bad Request` errors:

Check the request body against the expected API structure.

Example:

```json
{
  "firstName": "John",
  "lastName": "Smith",
  "email": "john.smith@example.com",
  "company": "ABC Technologies"
}
```

Validate:

- Required fields
- Field names
- Data types
- JSON syntax
- Business rules

---

## 6. Root-Cause Analysis

Document the difference between:

**Symptom:** What the client experienced.

**Finding:** What the investigation revealed.

**Root Cause:** The underlying reason the failure occurred.

**Contributing Factor:** A condition that increased the likelihood or impact of the incident.

Example:

**Symptom:** Customer creation returned `401 Unauthorized`.

**Finding:** The API rejected the authentication token.

**Root Cause:** The configured authentication token had expired.

**Contributing Factor:** No effective token-expiration monitoring or automatic refresh mechanism.

---

## 7. Resolution and Validation

After applying the resolution:

1. Repeat the failed request.
2. Confirm the HTTP status changed as expected.
3. Review the response body.
4. Verify the expected system behavior.
5. Record the result.
6. Update the incident ticket.

For API-level testing, a successful result may look like:

```http
201 Created
```

---

## 8. Incident Documentation

Each incident should contain:

- Incident ID
- Client issue
- Business impact
- Investigation steps
- Evidence
- Root cause
- Resolution
- Validation
- Preventive recommendation

---

## 9. Escalation

Escalate to the appropriate technical team when:

- The failure is confirmed to be server-side.
- The issue requires code changes.
- Infrastructure or service availability is involved.
- The issue requires access unavailable to support.
- The problem cannot be resolved using documented support procedures.

Include useful technical evidence such as:

- Endpoint
- HTTP method
- Status code
- Error message
- Timestamp
- Request/correlation ID
- Reproduction steps

Do not include passwords, API keys, access tokens, or other sensitive information.

---

## Skills Demonstrated

- REST API troubleshooting
- Postman
- HTTP status-code analysis
- Authentication troubleshooting
- JSON validation
- Root-cause analysis
- Incident management
- Technical escalation
- Technical documentation
