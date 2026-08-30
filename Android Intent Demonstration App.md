# Android Intent Demonstration App

## Practical: Implicit & Explicit Intent

### AIM

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

## 🧠 Concepts Studied

The following Android concepts are covered in this practical:

- Intent
- Explicit Intent
- Implicit Intent
- Intent Actions
- `Intent.setData()`
- `Intent.setType()`
- `Uri.parse()`
- `startActivity()`
- `Button`
- `ConstraintLayout`
- `CoordinatorLayout`
- `ActivityResultContracts`
- Runtime Permissions
- Manifest Permissions
- `ContextCompat.checkSelfPermission()`
- `ActivityCompat.requestPermissions()`
- `ContactsContract.Contacts.CONTENT_TYPE`
- `CallLog.Calls.CONTENT_TYPE`
- `"image/*"`
- `"tel:"`

---

# 🔀 Types of Intent

## 1. Explicit Intent

An **Explicit Intent** specifies the exact component or Activity that should be started.

Example:

```java
Intent intent = new Intent(MainActivity.this, LoginActivity.class);
startActivity(intent);
```

In this practical, Explicit Intent is used to open the **Login Activity**.

---

## 2. Implicit Intent

An **Implicit Intent** does not specify a particular application or component.

Instead, it describes the action that should be performed, and Android finds an appropriate application to handle it.

Example:

```java
Intent intent = new Intent(Intent.ACTION_VIEW);
intent.setData(Uri.parse("https://www.google.com"));
startActivity(intent);
```

---

# 🚀 Practical Demonstrations

## 1. 📞 Make Call to Specific Number

The application opens the phone dialer with a predefined phone number.

```java
Intent intent = new Intent(Intent.ACTION_DIAL);
intent.setData(Uri.parse("tel:9876543210"));
startActivity(intent);
```

### Important

Using `ACTION_DIAL` opens the dialer and allows the user to make the call manually.

If `ACTION_CALL` is used, the application requires the `CALL_PHONE` permission.

---

# 2. 🌐 Open Specific URL

The application opens a specified website using the device's default browser.

```java
Intent intent = new Intent(Intent.ACTION_VIEW);
intent.setData(Uri.parse("https://www.google.com"));
startActivity(intent);
```

### Key Concept

```java
Uri.parse()
```

converts the URL string into a `Uri` object that can be supplied to the Intent.

---

# 3. 📋 Open Call Log

The application opens the device's call log.

```java
Intent intent = new Intent(Intent.ACTION_VIEW);
intent.setType(CallLog.Calls.CONTENT_TYPE);
startActivity(intent);
```

### Content Type

```java
CallLog.Calls.CONTENT_TYPE
```

is used to identify the call-log content.

Depending on the Android version and device, access to call-log information may require appropriate permissions.

---

# 4. 🖼️ Open Gallery

The application launches an application capable of selecting images.

```java
Intent intent = new Intent(Intent.ACTION_GET_CONTENT);
intent.setType("image/*");
startActivity(intent);
```

### Key Concept

```java
"image/*"
```

specifies that the application is interested in image files.

---

# 5. ⏰ Set Alarm

The application opens the system alarm interface.

```java
Intent intent = new Intent(AlarmClock.ACTION_SET_ALARM);
intent.putExtra(AlarmClock.EXTRA_HOUR, 7);
intent.putExtra(AlarmClock.EXTRA_MINUTES, 30);
intent.putExtra(AlarmClock.EXTRA_MESSAGE, "Morning Alarm");

startActivity(intent);
```

Required import:

```java
import android.provider.AlarmClock;
```

The exact behavior can vary depending on the device's installed clock application.

---

# 6. 📷 Open Camera

The application launches the device camera.

```java
Intent intent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
startActivity(intent);
```

Required import:

```java
import android.provider.MediaStore;
```

If the application directly accesses the camera, camera permission may be required.

---

# 7. 🔐 Open Login Activity

This demonstrates **Explicit Intent**.

```java
Intent intent = new Intent(MainActivity.this, LoginActivity.class);
startActivity(intent);
```

Here Android is explicitly told to open:

```text
LoginActivity
```

rather than asking the system to find an application capable of handling an action.

---

# 🔐 Permissions

Some Android operations require permissions.

Permissions can be declared in:

```text
AndroidManifest.xml
```

Example:

```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.CALL_PHONE" />
<uses-permission android:name="android.permission.READ_CALL_LOG" />
```

> **Note:** Permission requirements depend on the exact Intent/action being used and the Android version. For example, `ACTION_DIAL` does not require `CALL_PHONE`, while directly placing a call with `ACTION_CALL` does.

---

# 🛡️ Runtime Permission Checking

Modern Android versions require dangerous permissions to be requested at runtime.

### Check Permission

```java
if (ContextCompat.checkSelfPermission(
        this,
        Manifest.permission.CAMERA
) != PackageManager.PERMISSION_GRANTED) {

    ActivityCompat.requestPermissions(
            this,
            new String[]{Manifest.permission.CAMERA},
            100
    );
}
```

### Important Methods

#### `ContextCompat.checkSelfPermission()`

Checks whether a particular permission has already been granted.

#### `ActivityCompat.requestPermissions()`

Requests the required permission from the user.

---

# 🎯 ActivityResultContracts

Modern Android development recommends using the **Activity Result API** instead of relying only on the older `startActivityForResult()` approach.

Example:

```java
ActivityResultLauncher<Intent> galleryLauncher =
        registerForActivityResult(
                new ActivityResultContracts.StartActivityForResult(),
                result -> {
                    if (result.getResultCode() == RESULT_OK) {
                        // Handle selected image
                    }
                }
        );
```

Launch:

```java
Intent intent = new Intent(Intent.ACTION_GET_CONTENT);
intent.setType("image/*");

galleryLauncher.launch(intent);
```

---

# 🧩 Important Intent Actions

| Intent Action | Purpose |
|---|---|
| `ACTION_VIEW` | View/open content |
| `ACTION_DIAL` | Open phone dialer |
| `ACTION_CALL` | Directly place a phone call |
| `ACTION_GET_CONTENT` | Select content from another application |
| `ACTION_SET_ALARM` | Create an alarm |
| `ACTION_IMAGE_CAPTURE` | Launch camera |
| Explicit Intent | Open a specific Activity |

---

# 🛠️ Technologies Used

- **Language:** Java / Kotlin
- **Platform:** Android
- **IDE:** Android Studio
- **UI:** XML
- **Layout:** ConstraintLayout / CoordinatorLayout
- **Minimum SDK:** As configured in the project
- **Build System:** Gradle

---

# 📂 Suggested Project Structure

```text
IntentDemo/
│
├── app/
│   └── src/
│       └── main/
│           ├── java/
│           │   └── .../
│           │       ├── MainActivity.java
│           │       └── LoginActivity.java
│           │
│           ├── res/
│           │   ├── drawable/
│           │   ├── layout/
│           │   │   ├── activity_main.xml
│           │   │   └── activity_login.xml
│           │   └── values/
│           │
│           └── AndroidManifest.xml
│
└── README.md
```

---

# ▶️ How to Run

### 1. Clone the repository

```bash
git clone <YOUR-REPOSITORY-URL>
```

### 2. Open the project

Open the project in **Android Studio**.

### 3. Sync Gradle

Allow Android Studio to complete Gradle synchronization.

### 4. Connect a Device

Use either:

- Android Emulator
- Physical Android device

### 5. Run

Click:

```text
Run ▶
```

and select your target device.

---

# 🧪 Expected Output

The application should provide buttons for each operation:

```text
┌──────────────────────────────┐
│       INTENT DEMO APP        │
├──────────────────────────────┤
│ 📞  Make Call                │
│ 🌐  Open URL                 │
│ 📋  Open Call Log            │
│ 🖼️  Open Gallery             │
│ ⏰  Set Alarm                │
│ 📷  Open Camera              │
│ 🔐  Open Login Activity      │
└──────────────────────────────┘
```

Clicking each button should launch the corresponding Android system application or Activity.

---

# 📚 Learning Outcomes

After completing this practical, we understand:

- What an Intent is
- Difference between Explicit and Implicit Intent
- How Android communicates between applications
- How to launch system applications
- How to pass data through an Intent
- How `Uri.parse()` works
- How `Intent.setData()` is used
- How `Intent.setType()` is used
- How to launch another Activity
- How Android permissions work
- How to check runtime permissions
- How to request runtime permissions
- How to use the Activity Result API

---

# 📖 References

### Practical Resources

- **Add Drawable Resource in Android Project:**  
  https://sites.google.com/ganpatuniversity.ac.in/mad/practical-list/practical-3

- **Add Activity in Android Project:**  
  https://sites.google.com/ganpatuniversity.ac.in/mad/views-android/new-activity

### University Logo

The project can use the provided **GUNI Pink Logo** as the application/project drawable resource.

---

# 👨‍💻 Practical Information

**Subject:** Mobile Application Development (MAD)

**Practical:** Implicit & Explicit Intent

**University:** Ganpat University

**Project Type:** Android Application

---

## ⭐ Conclusion

This practical successfully demonstrates **Implicit Intent and Explicit Intent** in Android.

Implicit Intents allow the application to interact with suitable system or third-party applications, while Explicit Intents allow direct navigation between Activities within the same application.

Through this practical, we learn how Android uses Intents as a fundamental mechanism for communication between different components and applications.