# Veristudy Architecture

## Design goals

Veristudy separates device-level activity verification from shared organization administration. The desktop application remains responsible for observing and classifying the active study context. Supabase is responsible for identity, authorization, synchronized organization data, and authenticated reporting.

## Desktop application

The Electron desktop application provides the member and administrator interfaces. Its local services manage session timing, idle detection, activity-context classification, and SQLite persistence.

Platform-specific helpers identify the foreground application and supported browser domain. Windows uses one bundled hidden helper process for the life of the application. macOS uses native operating-system integrations and requires Accessibility permission.

## Local data

SQLite supports offline-friendly session state, organization selection, approved-tool data, and recovery of interrupted sessions. Organization data is scoped so switching workspaces does not mix members, settings, or sessions.

Veristudy does not persist owner or administrator passwords locally. A renewable authentication session may be remembered using Electron secure storage, which relies on operating-system protected credential storage.

## Supabase backend

Supabase Authentication provides organization-scoped accounts. PostgreSQL tables and RPCs store shared organization membership, roles, settings, approved tools, policy acknowledgements, and session history.

Authorization is enforced on the backend. Owners can manage administrator access, owners and administrators can review membership requests, and ordinary members cannot unlock administrative actions with a password alone.

## Reporting

The treasurer-report Edge Function accepts an authenticated organization request, retrieves the server-owned recipient and organization rules, calculates the report from approved session data, applies rate limits, and submits the resulting email through the configured provider.

The desktop never receives or stores the provider API key.

## Release model

macOS and Windows artifacts are built separately for their native platforms. Public binaries are distributed through a release-only GitHub repository. The application checks that repository for newer semantic versions and directs users to the trusted release page; it does not silently replace or execute downloaded updates.

