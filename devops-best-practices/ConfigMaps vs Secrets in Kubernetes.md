# ConfigMaps vs Secrets in Kubernetes

If you treat ConfigMaps and Secrets as interchangeable, you're doing Kubernetes wrong.

This document explains **what they are, how they differ, when to use each**, and the mistakes that cause real production incidents.

---

## 1. What is a ConfigMap?

A **ConfigMap** is used to store **non-sensitive configuration data** separately from application code.

### Common Use Cases
- Application configuration files
- Environment variables
- Feature flags
- Log levels
- Service URLs
- Port numbers

### Key Characteristics
- Stored in **plain text**
- Easily readable
- Meant for configuration, **not security**

### Example
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_ENV: production
  LOG_LEVEL: info
```

---

2. What is a Secret?

A Secret is used to store sensitive data such as credentials and keys.

Common Use Cases

Database passwords

API keys

Tokens

Certificates


✅ Key Characteristics

Stored as Base64-encoded values

Slightly more restricted than ConfigMaps

Not encrypted by default


⚠️ Base64 encoding is not security. It’s just encoding.

Example

apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  DB_PASSWORD: cGFzc3dvcmQxMjM=


---

3. Core Differences

Feature	ConfigMap	Secret

Purpose	Configuration	Sensitive data
Data Storage	Plain text	Base64-encoded
Security Level	Low	Higher (but not secure)
Use Case	App settings	Credentials & keys



---

4. How Pods Consume Them

Using ConfigMap

env:
  - name: LOG_LEVEL
    valueFrom:
      configMapKeyRef:
        name: app-config
        key: LOG_LEVEL

Using Secret

env:
  - name: DB_PASSWORD
    valueFrom:
      secretKeyRef:
        name: db-secret
        key: DB_PASSWORD


---

5. Common (and Dangerous) Mistakes

❌ Storing passwords in ConfigMaps
❌ Assuming Secrets are encrypted
❌ Giving broad RBAC access to Secrets
❌ Committing Secrets to Git repositories

If someone with cluster access can read it easily, it’s not secure.


---

6. Security Reality Check

Kubernetes Secrets alone are not enough for real-world security.

What You Actually Need

RBAC to restrict access

Encryption at rest enabled

External secret managers:

HashiCorp Vault

AWS Secrets Manager

Azure Key Vault

GCP Secret Manager




---

7. Simple Rule to Remember

ConfigMaps → configuration

Secrets → credentials

Sensitive data in ConfigMaps = bad DevOps


If you can’t explain why you chose one over the other, you probably chose wrong.


---

8. Final Thoughts

Kubernetes gives you tools. Security depends on how responsibly you use them.

Design your cluster as if:

Someone else will audit it

Someone else will maintain it

Someone else will exploit your mistakes


Because eventually — they will.

---

