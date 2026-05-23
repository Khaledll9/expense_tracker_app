![Expense Tracker Banner](https://via.placeholder.com/1200x400/7c3aed/ffffff?text=Expense+Tracker)

<p align="center">
  <strong>Track. Categorize. Visualize. — A lightweight Flutter expense manager with real-time charts and swipe-to-delete.</strong>
</p>

<p align="center">
  <a href="https://flutter.dev"><img src="https://img.shields.io/badge/Flutter-3.22+-02569B?logo=flutter&logoColor=white" alt="Flutter"></a>
  <a href="https://dart.dev"><img src="https://img.shields.io/badge/Dart-3.4+-0175C2?logo=dart&logoColor=white" alt="Dart"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-green" alt="License"></a>
  <a href="https://github.com/your-org/expense_tracker"><img src="https://img.shields.io/badge/build-passing-brightgreen" alt="Build"></a>
</p>

---

## About The Project

Expense Tracker is a cross-platform mobile application built with **Flutter** that helps individuals log, categorize, and visualize daily expenses. Users can add expenses with a title, amount, date, and category (Food, Travel, Leisure, Work), then view a real-time breakdown via color-coded bar charts.

The app was designed as a **lean, single-responsibility project** that demonstrates clean widget decomposition, responsive layout patterns, and local state management — ideal for onboarding new Flutter contributors or serving as a portfolio reference.

---

## Tech Stack & Core Ecosystem

| Technology | Role |
|---|---|
| **Flutter & Dart** | Cross-platform UI framework and language |
| **intl** | Locale-aware date formatting (`DateFormat.yMd`) |
| **uuid** | Unique `Expense` ID generation (`uuid.v4()`) |
| **flutter_lints** | Static analysis lint rules (via `package:flutter_lints/flutter.yaml`) |
| **flutter_test** | Widget and unit testing |

---

## Key Architecture

The project follows a **widget-composition architecture** — a pragmatic, single-module structure without a formal state management library. Data flows unidirectionally from state down through widgets:

```
Expenses (StatefulWidget)          ← In-memory List<Expense>
  │
  ├── Chart (StatelessWidget)      ← Reads expenses, renders ExpenseBucket categories
  │     └── ChartBar               ← FractionallySizedBox per category
  │
  └── ExpensesList (StatelessWidget)
        └── ExpenseItem (Card)     ← Dismissible swipe-to-delete
              │
              └── onRemoveExpense callback
                     └── _ExpensesState.removeExpense()
                           └── SnackBar with Undo action
```

- **State holder:** `_ExpensesState` at the screen root maintains a single `List<Expense>`.
- **No external state management** — `setState()` is sufficient for this scale.
- **Responsive breakpoint:** 600px width switches between stacked `Column` (phone) and side-by-side `Row` (tablet/desktop).
- **Bottom sheet form** (`NewExpense`) adapts its own layout at the same 600px threshold.

---

## Key Features

### Expense Management
- **Add expenses** — title, amount (USD), date picker, and category selector.
- **Swipe to delete** — dismissible cards with a 3-second undo snackbar.
- **Input validation** — alerts on empty titles, invalid amounts, or missing dates.

### Data Visualization
- **Category bar chart** — four color-coded bars (Food, Travel, Leisure, Work) proportional to total spend.
- **Responsive layout** — column on narrow screens, side-by-side row on wider screens.

### Platform & UX
- **Material Design 3** — dynamic color scheme generated from a seed color.
- **Dark mode ready** — dark color scheme defined and ready to activate.
- **Lightweight** — zero persistence layer, no network calls, no build_runner.

---

## Getting Started & Local Setup

### Prerequisites

- Flutter SDK **^3.22.0** (Dart **^3.4.0**)
- Platform tooling:
  - **Android:** Android Studio & Android SDK
  - **iOS/macOS:** Xcode & CocoaPods
  - **Windows/Linux:** Visual Studio or relevant desktop toolchain

### Setup Steps

```bash
# 1. Clone the repository
git clone https://github.com/your-org/expense_tracker.git
cd expense_tracker

# 2. Fetch dependencies
flutter pub get

# 3. Run static analysis
flutter analyze

# 4. Run tests
flutter test

# 5. Launch the app
flutter run
```

> No code generation step required — the project uses zero `build_runner` or generated code.

---

## Screenshots & UI Showcase

| Mobile (Light) | Mobile (Dark) |
|---|---|
| ![Mobile Light](https://via.placeholder.com/320x640/e2e8f0/1e293b?text=Light+Mode) | ![Mobile Dark](https://via.placeholder.com/320x640/1e293b/e2e8f0?text=Dark+Mode) |
| **Tablet (Landscape)** | **Add Expense Sheet** |
| ![Tablet](https://via.placeholder.com/640x360/7c3aed/ffffff?text=Tablet+Layout) | ![Sheet](https://via.placeholder.com/320x400/7c3aed/ffffff?text=Bottom+Sheet) |

*Replace placeholder images with actual screenshots captured from `flutter run`.*

---

## Contact & Licensing

**Project maintainer:** [Your Name](https://github.com/your-profile) — [email@example.com](mailto:email@example.com) — [LinkedIn](https://linkedin.com/in/your-profile)

Distributed under the **MIT License**. See `LICENSE` for more information.
