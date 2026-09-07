# Veristudy Security and Privacy

## Data minimization

Veristudy evaluates study context using limited metadata such as foreground application names, approved website domains, idle state, interaction counts, focus duration, and context switches.

The application is not designed to read webpage text, document contents, messages, passwords, files, or keystroke contents.

## Identity and authorization

- Accounts are scoped to an organization.
- New join requests require owner or administrator approval.
- The organization creator becomes its sole initial owner.
- Owners may grant or remove administrator access.
- Administrators cannot change owner or administrator roles.
- Removed members lose access to synchronized organization data.

## Credential handling

- Account passwords are handled by the authentication backend.
- Owner and administrator passwords are not stored in the local SQLite database.
- Remembered sessions store only an encrypted renewable token through operating-system protected storage.
- Backend service keys and email-provider credentials remain server-side secrets.

## Backend protections

- Authenticated RPC and Edge Function requests
- Role checks for administrative operations
- Organization-scoped data access
- Server-side session-integrity validation
- Server-calculated accountability reports
- Layered request and report rate limits
- Password hashing with an explicit bcrypt cost of 12 where application-managed hashes are required

## Responsible disclosure

This repository intentionally excludes production source code, infrastructure secrets, internal identifiers, organization join codes, and real member information. Please do not open a public issue containing a credential or private member data.

