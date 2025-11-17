# Data Model: Create Login Screen

**Date**: 2025-11-17

This document outlines the data entities required for the "Create Login Screen" feature, as derived from the feature specification.

## Entity: UserCredentials

Represents the data entered by the user on the login screen. This is a transient data structure used by the UI and presentation layer.

**Source**: `spec.md`, Section: "Key Entities"

### Attributes

| Name | Type | Description | Validation Rules |
|---|---|---|---|
| `email` | String | The email address provided by the user. | Must be a valid email format. |
| `password` | String | The password provided by the user. | Must not be empty. |

### State Transitions

The `UserCredentials` entity is part of the overall `LoginState`, which can transition between the following states within the ViewModel:

- **Idle**: The initial state before any user interaction.
- **Editing**: The state when the user is actively typing in the email or password fields.
- **Submitting**: The state when the user has clicked the "Sign In" button (Note: for this feature, this will trigger a mock interaction).
- **Error**: The state when validation fails (e.g., invalid email format).
