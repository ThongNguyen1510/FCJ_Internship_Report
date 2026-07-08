---
title: "Blog 4"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 3.4. </b> "
---

# Implementing Fine-Grained Access Control with Cognito User Pools

### 1. Fine-Grained Access Control (FGAC) Definition
In multi-tenant applications and enterprise systems, security dictates that users should only see and modify resources belonging to their organization, department, or level of clearance. This is called **Fine-Grained Access Control (FGAC)**.

Amazon Cognito User Pools, combined with API Gateway and AWS IAM, provides a powerful toolkit to enforce FGAC policies on REST endpoints.

---

### 2. Cognito User Groups and Custom Attributes
To implement FGAC, we define custom attributes inside our Amazon Cognito User Pool:
- `custom:tenant_id`: Identifies the client's corporate workspace.
- `custom:clearance_level`: Categorizes the user's role (e.g., Admin, ReadOnly).

When users authenticate, these attributes are baked into the ID token JWT claims. 

---

### 3. API Gateway Integration Patterns
We can enforce authorization rules at the API Gateway layer using two main patterns:
1. **Cognito Authorizer**: API Gateway automatically checks the signature of the Cognito JWT token and validates expiration. However, routing logic based on custom attributes must be handled inside the backend Lambda.
2. **Lambda Authorizer**: A custom Lambda function intercepts the token, parses the custom attributes, and dynamically generates an IAM Policy to return to API Gateway.

Here is a snippet of a Python Lambda Authorizer generating an IAM policy restricted by `tenant_id`:

```python
def generate_policy(principal_id, effect, resource, tenant_id):
    auth_response = {
        'principalId': principal_id,
        'policyDocument': {
            'Version': '2012-10-17',
            'Statement': [{
                'Action': 'execute-api:Invoke',
                'Effect': effect,
                'Resource': resource
            }]
        },
        'context': {
            'tenantId': tenant_id
        }
    }
    return auth_response
```

The downstream application Lambda can then read `requestContext.authorizer.tenantId` to query database records matching only that specific tenant.

---

### 4. Summary
Combining Cognito custom attributes with Lambda authorizers provides an absolute boundary between tenants, safeguarding data from unauthorized queries or leakage.

