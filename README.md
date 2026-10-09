# Telecom API Postman Collection

## Project overview

This project contains a Postman collection named **Test_Telecom** and a QA environment named **QA_env**. The collection exercises user account and contact-management API workflows. It contains 11 requests, each with response checks.

## Collection contents

| Area | Requests | What they cover |
|---|---|---|
| User accounts | Adduser, Get user Profile, Update User, Log In User, Logout User, Delete User | Create an account, read and update the current profile, authenticate, end a session, and delete the current account |
| Contacts | Add Contact, Get Contact List, Get Contact, Update Contact (PUT), Update Contact (PATCH) | Create, list, retrieve, replace, and partially update contacts |

The requests use `{{Base_URI}}` as their base URL. Several tests check expected HTTP status codes; additional checks validate response data, record ownership, and (for one update) response time.

## Environment variables

The QA environment defines these variables:

- `Base_URI` — API base URL
- `token` — authentication token
- `_id` — contact identifier used by the collection
- `owner` — expected contact owner
- `contact_id` — contact identifier used by update requests
- `user_id` — user identifier used by profile checks (currently has no value in the supplied environment)

The exported environment contains populated values. Keep the original environment private if any values are credentials or identify real systems or records. For a Git repository, commit a sanitized example environment with placeholder values and keep the real QA environment out of version control.

## Running the collection

1. Import `Test_Telecom.postman_collection.json` into Postman.
2. Import `QA_env.postman_environment.json`, or select a sanitized environment configured with the same variable names.
3. Select the QA environment and confirm `Base_URI` points to the intended QA API.
4. Supply valid credentials and current record identifiers where required. In particular, set `user_id` to the expected user ID before running the profile checks.
5. Run requests in a workflow-compatible order: register or log in, perform profile and contact operations, then log out.
6. Run **Delete User** only when account deletion is intended. It is a destructive request.

Some requests depend on existing accounts, authentication state, or records. If the collection’s tests expect a specific ID or response value, update the corresponding environment variable and test data to match the QA API before running.

## Suggested Git contents

```text
.
├── Test_Telecom.postman_collection.json
├── QA_env.example.postman_environment.json
├── README.md
└── .gitignore
```

Do not commit an environment export containing real tokens, passwords, or other secrets. A `.gitignore` entry can exclude the private export, for example:

```gitignore
QA_env.postman_environment.json
```

Commit the sanitized example environment instead. Before pushing, review the collection and example file for credentials embedded in request bodies, scripts, URLs, or variable values.
