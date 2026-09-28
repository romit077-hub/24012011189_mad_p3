# Android Intent Demonstration App - MAD Practical 3

**Enrollment Number:** 24012011189  
**Course:** Mobile Application Development (MAD)  
**Practical:** Practical 3 - Implicit & Explicit Intent  
**University:** Ganpat University  

---

## 🎯 AIM

Create an Android application that demonstrates the use of **Implicit Intent** and **Explicit Intent**.

The application demonstrates the following operations:

1. Make a call to a specific number
2. Open a specific URL
3. Open the Call Log
4. Open the Gallery
5. Set an Alarm
6. Open the Camera
7. Open the Login Activity

---

## 📱 About the Practical

This practical demonstrates how Android applications can communicate with:

- Other applications
- Android system components
- Activities within the same application

The application uses **Implicit Intents** for operations such as opening the browser, camera, gallery, call log, and alarm application, while **Explicit Intent** is used to navigate between activities inside the application.

---

## 🛠️ Tech Stack & Requirements

- **Language:** Kotlin / Java
- **UI Toolkit:** Android XML Layouts (`ConstraintLayout`)
- **Min SDK:** 24 (Android 7.0)
- **Compile SDK:** 37
- **Target SDK:** 37
- **Build System:** Gradle (Kotlin DSL)
- **IDE:** Android Studio

---

## 🧠 Concepts Studied

The following Android concepts are covered in this practical:

- Intent (Explicit & Implicit)
- Intent Actions (`ACTION_VIEW`, `ACTION_DIAL`, `ACTION_GET_CONTENT`, `ACTION_SET_ALARM`, `ACTION_IMAGE_CAPTURE`)
- `Intent.setData()`
- `Intent.setType()`
- `Uri.parse()`
- `startActivity()`
- `ConstraintLayout`
- Runtime Permissions & Manifest Permissions

---

## 🔀 Types of Intent

### 1. Explicit Intent
An **Explicit Intent** specifies the exact component or Activity that should be started.

```kotlin
val intent = Intent(this@MainActivity, LoginActivity::class.java)
startActivity(intent)
```

### 2. Implicit Intent
An **Implicit Intent** does not specify a particular application component. Instead, it describes the action to perform.

```kotlin
val intent = Intent(Intent.ACTION_VIEW, Uri.parse("https://www.google.com"))
startActivity(intent)
```

---

## 🚀 How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/romit077-hub/24012011189_mad_p3.git
   ```
2. Open the project in **Android Studio**.
3. Sync Gradle project files.
4. Run the application on an Android Emulator or connected physical device.

---

## 🧪 Expected UI Layout

The application provides controls for each intent action:

```text
┌──────────────────────────────┐
│       INTENT DEMO APP        │
├──────────────────────────────┤
│ 🌐  Web URL  [Browse]        │
│ 📞  Phone No [Call]          │
│ 📋  Call Log [Call Log]      │
│ 🖼️  Gallery  [Gallery]       │
│ 📷  Camera   [Camera]        │
│ ⏰  Alarm    [Alarm]         │
│ 🔐  Login    [Login]         │
└──────────────────────────────┘
```

---

## 📚 References

- **Practical List:** [MAD Practical 3](https://sites.google.com/ganpatuniversity.ac.in/mad/practical-list/practical-3)
- **New Activity Guide:** [Android New Activity](https://sites.google.com/ganpatuniversity.ac.in/mad/views-android/new-activity)
