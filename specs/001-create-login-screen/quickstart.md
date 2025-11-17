# Quickstart: Create Login Screen

**Date**: 2025-11-17

This document provides a brief guide to getting started with the "Create Login Screen" feature.

## Overview

The login screen is a self-contained feature module located in `:feature:login`. It is built using Jetpack Compose and follows the MVVM and Clean Architecture principles outlined in the project constitution.

## How to Run

1.  **Sync Gradle**: Ensure the new `:feature:login` module is recognized by Android Studio.
2.  **Build the App**: Build the project to compile the new module.
3.  **Launch the App**: Run the application on an emulator or a physical device. The login screen should be the first screen you see.

## Key Components

-   **`LoginScreen.kt`**: The main Composable function that builds the UI.
-   **`LoginViewModel.kt`**: The ViewModel responsible for managing the UI state.
-   **`LoginState.kt`**: An immutable data class representing the state of the login screen.
-   **`LoginModule.kt`**: The Hilt module for providing dependencies related to the login feature.
