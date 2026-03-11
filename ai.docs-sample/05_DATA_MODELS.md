# Data Models (Master Schema)
## ⚡ STRICT CONSTRAINTS FOR AI (MANDATORY)
- **Tenant Scope:** Every table (except global ones like `roles`) MUST have `company_id`.
- **Stateless IDs:** Use `public_id` (ULID) for all external references.
- **Append-Only:** Tables like `interactions` and `audit_logs` are IMMUTABLE.
- **FK Integrity:** Do not suggest queries that skip relational constraints.

---

## 1. Global Conventions
- **IDs:** `id` (bigint, internal) | `public_id` (ulid, external).
- **Timestamps:** `created_at`, `updated_at`.
- **Tenant:** `company_id` (FK -> companies.id).

---

## 2. Entity Dictionary

### 2.1 Identity & Tenant
| Table | Purpose | Key Columns |
| :--- | :--- | :--- |
| **companies** | Tenants | `id`, `public_id`, `name`, `status` (active, suspended) |
| **users** | Auth users | `id`, `public_id`, `company_id`, `email`, `password_hash`, `status` |

### 2.2 Authorization (RBAC)
| Table | Purpose | Key Columns |
| :--- | :--- | :--- |
| **roles** | Role registry | `id`, `name` (COMPANY_OWNER, etc) |
| **permissions** | Atomic perms | `id`, `name` |
| **user_roles** | Assignment | `user_id`, `role_id` |
| **role_permissions**| Mapping | `role_id`, `permission_id` |

### 2.3 CRM Core
| Table | Purpose | Key Columns |
| :--- | :--- | :--- |
| **clients** | Accounts | `id`, `public_id`, `company_id`, `name`, `email`, `status` |
| **contacts** | Contacts | `id`, `public_id`, `company_id`, `client_id`, `name`, `email` |
| **interactions** | Immutable Logs | `id`, `public_id`, `client_id`, `author_user_id`, `content` |

### 2.4 Traceability
| Table | Purpose | Key Columns |
| :--- | :--- | :--- |
| **audit_logs** | Security trail | `id`, `company_id`, `user_id`, `action`, `metadata` |

---

## 3. Physical Schema Reference

### **`companies`**
- `id`: bigint, PK
- `public_id`: ulid, unique
- `name`: varchar(160)
- `status`: varchar(20)

### **`users`**
- `id`: bigint, PK
- `company_id`: FK(companies)
- `email`: unique(company_id, email)
- `status`: active, invited, disabled

### **`clients`**
- `id`: bigint, PK
- `company_id`: FK(companies)
- `created_by_user_id`: FK(users)
- `name`: varchar(200)

### **`interactions`** (IMMUTABLE)
- `client_id`: FK(clients)
- `author_user_id`: FK(users)
- `content`: text
- `created_at`: timestamptz (now)
