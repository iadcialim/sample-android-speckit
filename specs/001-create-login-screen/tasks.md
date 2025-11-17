# Tasks: Create Login Screen

**Input**: Design documents from `/specs/001-create-login-screen/`
**Prerequisites**: plan.md (required), spec.md (required for user stories)

**Tests**: Test tasks are included as specified in the implementation plan.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1)
- Include exact file paths in descriptions

---

## Phase 1: Setup (Module & Dependencies)

**Purpose**: Create the new feature module and configure its dependencies.

- [ ] T001 Create the new Gradle module named `:feature:login` in the `feature/login` directory.
- [ ] T002 [P] Add Jetpack Compose, Navigation, Hilt, and Coroutines dependencies to `feature/login/build.gradle.kts`.
- [ ] T003 [P] Add the `cognizant-logo.png` to the appropriate drawable resource folder.
- [ ] T004 Update `settings.gradle.kts` to include the new `:feature:login` module.
- [ ] T005 Update the `:app` module's `build.gradle.kts` to add a dependency on `:feature:login`.

---

## Phase 2: Foundational (Navigation & DI)

**Purpose**: Core infrastructure that MUST be complete before the UI can be shown.

- [ ] T006 Set up the navigation graph in the `:app` module to make the `LoginScreen` the start destination.
- [ ] T007 Create the Hilt dependency injection module `feature/login/src/main/java/com/iadcialimguno/samplespeckitapp/login/di/LoginModule.kt`.

**Checkpoint**: Foundation ready. The app can now navigate to an empty login screen.

---

## Phase 3: User Story 1 - Visual Login Screen (Priority: P1) 🎯 MVP

**Goal**: Implement the complete UI for the login screen, matching the design specification, with mock data and state management.

**Independent Test**: The screen can be launched and visually verified via UI tests. The ViewModel logic can be verified with unit tests.

### Tests for User Story 1 ⚠️

> **NOTE: Write these tests FIRST, ensure they FAIL before implementation**

- [ ] T008 [P] [US1] Create a unit test file for the ViewModel in `feature/login/src/test/java/com/iadcialimguno/samplespeckitapp/login/presentation/LoginViewModelTest.kt`.
- [ ] T009 [P] [US1] Create an Android UI test file for the composable screen in `feature/login/src/androidTest/java/com/iadcialimguno/samplespeckitapp/login/presentation/LoginScreenTest.kt`.

### Implementation for User Story 1

- [ ] T010 [P] [US1] Define the UI state in `feature/login/src/main/java/com/iadcialimguno/samplespeckitapp/login/domain/model/LoginState.kt`.
- [ ] T011 [P] [US1] Create the mock repository `feature/login/src/main/java/com/iadcialimguno/samplespeckitapp/login/data/LoginRepository.kt`.
- [ ] T012 [US1] Implement the `LoginViewModel` in `feature/login/src/main/java/com/iadcialimguno/samplespeckitapp/login/presentation/LoginViewModel.kt` (depends on T010, T011).
- [ ] T013 [P] [US1] Create the `EmailField` composable component in `feature/login/src/main/java/com/iadcialimguno/samplespeckitapp/login/presentation/components/EmailField.kt`.
- [ ] T014 [P] [US1] Create the `PasswordField` composable component in `feature/login/src/main/java/com/iadcialimguno/samplespeckitapp/login/presentation/components/PasswordField.kt`.
- [ ] T015 [P] [US1] Create the `SignInButton` composable component in `feature/login/src/main/java/com/iadcialimguno/samplespeckitapp/login/presentation/components/SignInButton.kt`.
- [ ] T016 [US1] Assemble the main UI in `feature/login/src/main/java/com/iadcialimguno/samplespeckitapp/login/presentation/LoginScreen.kt` (depends on T012, T013, T014, T015).
- [ ] T017 [US1] Ensure the `LoginScreen` correctly observes state from the `LoginViewModel`.

**Checkpoint**: At this point, User Story 1 should be fully functional and visually match the spec. All tests should pass.

---

## Phase 4: Polish & Cross-Cutting Concerns

**Purpose**: Final validation and cleanup.

- [ ] T018 Run all unit and UI tests and ensure they pass.
- [ ] T019 Manually validate the UI on an emulator or device, checking for visual consistency with `cogira-login-page.jpg` and responsiveness.
- [ ] T020 Perform a final code cleanup and refactoring pass.
- [ ] T021 Validate that the `quickstart.md` instructions are accurate.

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: Can start immediately.
- **Foundational (Phase 2)**: Depends on Setup completion.
- **User Story 1 (Phase 3)**: Depends on Foundational completion.
- **Polish (Phase 4)**: Depends on User Story 1 completion.

### User Story Dependencies

- **User Story 1 (P1)**: Is the only user story and represents the full scope of this feature.

### Parallel Opportunities

- Within Setup (Phase 1), dependency configuration (T002, T003) can happen in parallel with module creation.
- In User Story 1 (Phase 3), the creation of tests (T008, T009), data/domain classes (T010, T011), and individual UI components (T013, T014, T015) can all be done in parallel before the final assembly.

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup.
2. Complete Phase 2: Foundational.
3. Complete Phase 3: User Story 1.
4. **STOP and VALIDATE**: Run all tests and manually verify the UI.
5. Complete Phase 4: Polish.
6. The feature is now ready for deployment/demo.
