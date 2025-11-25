# Flutter Boilerplate

A production-ready Flutter boilerplate with clean architecture, dependency injection, and modular services.

## Architecture Overview

This boilerplate follows **Clean Architecture** principles with **BLoC** state management, ensuring separation of concerns, testability, and scalability.

```
lib/
├── main.dart
├── app.dart
│
├── config/
│   ├── app_config.dart
│   └── env.dart
│
├── core/
│   ├── di/
│   │   └── injector.dart
│   │
│   ├── network/
│   │   ├── api_client.dart
│   │   ├── api_endpoints.dart
│   │   ├── api_request.dart
│   │   └── api_response.dart
│   │
│   ├── services/
│   │   ├── base/
│   │   │   ├── service_interface.dart
│   │   │   └── service_registry.dart
│   │   ├── monitoring/
│   │   │   ├── monitoring_service.dart
│   │   │   └── sentry_service_impl.dart
│   │   ├── push/
│   │   │   ├── push_service.dart
│   │   │   └── fcm_service_impl.dart
│   │
│   ├── localization/
│   │   ├── localization_service.dart
│   │   ├── localization_repository.dart
│   │
│   ├── sanitization/
│   │   ├── sanitizer.dart
│   │   ├── input_validator.dart
│   │   └── rules/
│   │       └── sanitization_rules.dart
│   │
│   ├── errors/
│   │   ├── failures.dart
│   │   ├── exceptions.dart
│   │   └── error_handler.dart
│   │
│   └── utils/
│       ├── logger.dart
│       └── extensions.dart
│
├── features/
│   └── [feature_name]/
│       ├── data/
│       │   ├── models/
│       │   │   └── [feature]_model.dart
│       │   └── [feature]_repository.dart
│       │
│       ├── domain/
│       │   ├── entities/
│       │   │   └── [feature].dart
│       │   └── usecases/
│       │       └── [feature]_usecase.dart
│       │
│       └── presentation/
│           ├── bloc/
│           │   ├── [feature]_bloc.dart
│           │   ├── [feature]_event.dart
│           │   └── [feature]_state.dart
│           └── pages/
│               └── [feature]_page.dart
│
├── shared/
│   ├── widgets/
│   └── constants/
│
test/
├── unit/
│   ├── core/
│   └── features/
└── integration/
```

## Why This Architecture?

### 1. **Config Layer** (`config/`)
Centralizes environment variables and app configuration. This makes it easy to switch between development, staging, and production environments without code changes.

### 2. **Core Layer** (`core/`)
Contains shared infrastructure used across all features:

- **Dependency Injection** (`di/`): Manages dependencies centrally using a service locator pattern, making code testable and loosely coupled

- **Network** (`network/`):
  - Dynamic API client that can be swapped (e.g., REST, GraphQL)
  - Centralized request/response models reduce boilerplate
  - Single source of truth for API endpoints

- **Services** (`services/`):
  - **Base**: Interface-based design allows swapping implementations (e.g., switch from Sentry to another monitoring tool)
  - **Registry pattern**: Dynamically register and retrieve service implementations
  - **Monitoring**: Track errors and performance
  - **Push notifications**: Handle FCM or alternative push services

- **Localization**: Fetch translations dynamically from API for multi-language support

- **Sanitization**: Validate and sanitize user input to prevent security vulnerabilities (XSS, injection attacks)

- **Error Handling**: Consistent error management across the app with typed failures and exceptions

- **Utils**: Reusable helpers and extensions

### 3. **Features Layer** (`features/`)
Each feature is isolated and follows **Clean Architecture**:

- **Data Layer**:
  - Models handle JSON serialization
  - Repositories fetch data from APIs or local storage

- **Domain Layer**:
  - Entities represent business objects (pure Dart, no dependencies)
  - Use cases contain business logic (single responsibility)

- **Presentation Layer**:
  - BLoC handles state management
  - Pages/widgets render UI based on state

**Why?** This separation allows you to change UI without affecting business logic, swap data sources easily, and test each layer independently.

### 4. **Shared Layer** (`shared/`)
Reusable widgets and constants used across multiple features, promoting DRY principles.

### 5. **Test Layer** (`test/`)
Organized by test type (unit, integration) mirroring the app structure for easy navigation and comprehensive test coverage.

## Key Benefits

- **Scalability**: Add new features without modifying existing code
- **Testability**: Each layer can be tested in isolation
- **Maintainability**: Clear separation makes code easy to understand and modify
- **Flexibility**: Swap implementations (APIs, services) without breaking changes
- **Security**: Built-in input sanitization and validation
- **Type Safety**: Strong typing with proper error handling

## Getting Started

1. Clone the repository
2. Run `flutter pub get`
3. Configure your environment in `config/env.dart`
4. Run the app with `flutter run`

For help with Flutter development, see the [online documentation](https://docs.flutter.dev/).
