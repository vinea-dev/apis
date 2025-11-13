# 🤖 AGENTS.md - AI Context & Guidelines

> **Mission:** This repository is the **Single Source of Truth (SSOT)** for all API definitions, data schemas, and RPC service contracts. When generating code or modifying files here, **strict adherence to backward compatibility and style conventions is required.**

## 1. Repository Identity & Purpose
* **Type:** Interface Definition Language (IDL) Repository.
* **Core Technology:** Protocol Buffers v3 (`syntax = "proto3";`).
* **Role:** Centralizes contracts between services (Microservices) and clients (Frontend/Mobile).
* **Output:** Generates client/server stubs for Go, TypeScript, Python, Java, etc. (Verify specific targets in `buf.gen.yaml` or `Makefile`).

## 2. Directory Structure Map
Understanding the hierarchy is crucial for correct package naming.

```text
.
├── proto/                  # ROOT of all protobuf definitions
│   ├── common/             # Shared messages/enums (Time, Money, Pagination)
│   │   └── v1/
│   │── [service]/      # E.g., profile, history
│   │   └── v1/         # Versioning is MANDATORY
│   │       └── api.proto
│   └── google/             # Vendored Google standard protos (if not using Buf registry)
├── gen/                    # (Optional) Generated code output (if committed)
├── buf.yaml                # Buf module configuration
├── buf.gen.yaml            # Code generation settings
└── AGENTS.md               # This file

## 3. Coding Conventions (Strict Mode)

### Naming Standards

- Files: `snake_case.proto` (e.g., `user_api.proto`).
- Packages: Must match directory structure.
    * Pattern: [company].[domain].[service].[version]
    * Example: `acme.payment.processing.v1`
- Messages: `PascalCase` (e.g., `CreateOrderRequest`).
- Fields: `snake_case` (e.g., `user_id`, `created_at`).
- RPC Services: `PascalCase` (e.g., `PaymentAPI`).
- RPC Methods: `PascalCas`e (e.g., `GetTransactionHistory`).
- Enums: `PascalCase`, with `CAPS_SNAKE_CASE` values.
    * Rule: The zero value MUST be `ENUM_NAME_UNSPECIFIED`.

### Backward Compatibility Rules

**NEVER** suggest changes that break existing clients.

- ❌ DO NOT change the numeric tag of an existing field.
- ❌ DO NOT rename an existing field (unless focusing purely on wire-format, but JSON mappings break).
- ❌ DO NOT change the type of an existing field.
- ❌ DO NOT remove a field. Mark it as `deprecated = true` instead.
    * Example: `string email = 3 [deprecated = true];`
- ✅ DO add new fields with new tags.

## 4. Workflow Instructions for Agents

### When Asked to Create a New Service

1. Create the directory: proto/[service]/v1alpha1.
2. Define the `package` directive immediately.
3. Import `google/protobuf/empty.proto` or `common/v1/meta.proto` if needed.
4. Define standard request/response pairs (e.g., `GetXRequest` / `GetXResponse`).

### When Asked to Modify a Proto

1. Check `buf.yaml` or `buf.lock` for dependencies.
2. Locate the correct version folder (don't edit `v1` if `v2` exists unless specified).
3. Ensure the next available field ID is used (scan the file visually).

### When Asked to "Lint" or "Check"

1. Assume the user is using Buf.
2. Look for `buf.yaml` configuration.
3. Flag any missing comments on RPCs (documentation is required).
4. Flag any enums missing an `UNSPECIFIED` zero value.

## 5. Standard Imports & Dependencies

Be aware of these commonly available packages in this repo:

- `google.protobuf.Timestamp` (Use for all time fields).
- `google.protobuf.Duration` (Use for time spans).
- `google.protobuf.FieldMask` (Use for update operations).
- `google.api.http` (If gRPC-Gateway/HTTP annotations are used).

---

End of Agent Context. Prioritize consistency and type safety above all.