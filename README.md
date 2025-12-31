# 📘 MVP Architecture in Flutter

This project follows the **MVP (Model–View–Presenter)** architecture pattern in Flutter.

MVP is a UI architectural pattern that helps keep the code **clean, structured, testable, and easy to maintain** by clearly separating responsibilities.

---

## 🧱 What is MVP?

**MVP = Model – View – Presenter**
- **Model** → Business logic, API, Database
- **View** → UI (Flutter Widgets)
- **Presenter** → Handles logic & connects View with Model

✔ Clear separation of concerns   
✔ Highly testable   
✔ Easy to understand   
✔ Ideal for small to medium projects

Each layer has a single, clear responsibility.


---

## 📁 Project Folder Structure
```text
lib/
│
├── extensions/
│   └── app_extension.dart
│
├── helper/
│   ├── connection_helper.dart
│   └── db/
│
├── services/
│   ├── api_services.dart
│   └── firebase_services.dart
│
├── localization/
│   ├── app_translation.dart
│   ├── app_strings.dart
│   └── en_translation.dart
│
├── model/
│   └── data_models.dart
│
├── src/
│   └── feature_name/
│       ├── view/
│       │   ├── feature_screen.dart
│       │   └── feature_view.dart
│       │
│       ├── presenter/
│       │   └── feature_presenter.dart
│       │
│       └── widgets/
│           └── feature_widgets.dart
│
├── utils/
│   ├── app_colors.dart
│   ├── app_constants.dart
│   ├── app_enums.dart
│   └── app_routes.dart
│
└── widgets/
    └── buttons/
        └── primary_button_widget.dart
```


---

## 🔹 Model

**Role:**
- Handles business logic
- Manages data
- Communicates with API, database, or services

**Rules:**
- ❌ Does NOT know about UI
- ❌ Does NOT depend on Flutter widgets

**Examples:**
- Data models
- API services
- Database helpers

---

## 🔹 View

**Role:**
- Displays UI
- Handles user interaction
- Forwards actions to Presenter

**In Flutter:**
- `StatefulWidget` / `StatelessWidget`
- Screens and UI widgets

**Rules:**
- ❌ No business logic
- ❌ No API calls
- ✅ Implements a View interface (contract)

---

## 🔹 Presenter

**Role:**
- Acts as the middle layer (UI logic)
- Receives events from View
- Fetches data from Model
- Updates View via interface methods

**Rules:**
- ❌ Does NOT import Flutter widgets
- ✅ Knows both View and Model
- ✅ One Presenter per screen

---

## 🔄 MVP Data Flow

```text
User Action
   ↓
View (UI)
   ↓
Presenter
   ↓
Model (API / DB)
   ↑
Presenter
   ↑
View (UI Update)
```

---

## 🧪 Example: MVP Flow (Concept)
**View Contract**
```dart
abstract class FeatureView {
  void showLoading();
  void hideLoading();
  void showError(String message);
  void showData(String data);
}
```

**Presenter**
```dart
class FeaturePresenter {
  final FeatureView view;
  final ApiServices api;

  FeaturePresenter(this.view, this.api);

  void loadData() async {
    view.showLoading();
    try {
      final data = await api.fetchData();
      view.showData(data);
    } catch (e) {
      view.showError(e.toString());
    }
    view.hideLoading();
  }
}
```

**View (Flutter Screen)**
```dart
class FeatureScreen extends StatefulWidget {
  @override
  _FeatureScreenState createState() => _FeatureScreenState();
}

class _FeatureScreenState extends State<FeatureScreen>
    implements FeatureView {

  late FeaturePresenter presenter;

  @override
  void initState() {
    super.initState();
    presenter = FeaturePresenter(this, ApiServices());
    presenter.loadData();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(child: Text("MVP Screen")),
    );
  }

  @override
  void showLoading() {}
  @override
  void hideLoading() {}
  @override
  void showError(String message) {}
  @override
  void showData(String data) {}
}
```

---

## 🎯 When to Use MVP?
✔ Small to medium apps   
✔ Form-based screens   
✔ Learning architecture basics   
✔ Apps without heavy real-time updates

---

## 📄 License
```text
Copyright (c) 2025 Excelsior Technologies

Permission is hereby granted, free of charge, to any person obtaining a copy  
of this software and associated documentation files (the "Software"), to deal  
in the Software without restriction, including without limitation the rights  
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell  
copies of the Software, and to permit persons to whom the Software is  
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all  
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED **"AS IS"**, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR  
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,  
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```
