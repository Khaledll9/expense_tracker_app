# expense_tracker — AGENTS.md

## Project
Single-module Flutter app (no monorepo, no codegen).

## Commands
| Action | Command |
|--------|---------|
| Analyze/lint | `flutter analyze` |
| Test | `flutter test` |
| Run | `flutter run` |
| Get deps | `flutter pub get` |

## Architecture
- **Entrypoint**: `lib/main.dart` → renders `Expenses` widget
- **State**: `_ExpensesState` in `lib/widget/expenses.dart` holds a `List<Expense>` in memory (no persistence)
- **Model**: `lib/models/expense.dart` — `Expense` class (id via `uuid`), `Category` enum (`food`, `travel`, `leisure`, `work`), `ExpenseBucket` helper
- **Widgets**:
  - `lib/widget/expenses.dart` — main screen, breakpoint at 600px width switches between column (mobile) and row (tablet/desktop) layouts
  - `lib/widget/new_expense.dart` — bottom sheet form with responsive layout (≥600px switches to horizontal row layout)
  - `lib/widget/expenses_list/` — `ExpensesList` (ListView with Dismissible swipe-to-delete + Undo snackbar) and `ExpenseItem`
  - `lib/widget/chart/` — `Chart` and `ChartBar`

## Quirks
- `lib/widget/chart/chat.dart` defines `Chart` class (filename has typo `chat` vs `chart`)
- `test/widget_test.dart` is a stale counter test that does **not** reflect the current app — ignores or rewrite before relying on
- `analysis_options.yaml` uses `package:flutter_lints/flutter.yaml` — no custom rules
- `flutter_lints: ^3.0.0` in dev_dependencies (not `flutter_lints` alone — the package name is `flutter_lints` not `lints`)
- App uses `MaterialApp` with no `home` route name, just `home: const Expenses()`

## Style conventions
- Dart imports use `package:` paths (e.g., `package:expense_tracker/models/expense.dart`)
- `#` comments only in Dart code (no doc comments `///` used anywhere)
- Top-level `const`/`var` for theme colors (`kColorScheme`, `kDarkColorScheme`)
- `const` constructors preferred where possible
