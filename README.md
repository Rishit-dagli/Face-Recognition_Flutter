# Face Recognition_Flutter

## Table of contents

1. [Introduction](#Introduction)


2. [Key capabilities](#Key-capabilities)<br>
    2.1 [Production-ready for common use cases](#Production-ready-for-common-use-cases)<br>
    2.2 [On-device or in the cloud](#On-device-or-in-the-cloud )<br>
    2.3 [Deploy custom models](#Deploy-custom-models)<br>
   
   
3. [Example (Face detection)](#Example-(Face-detection))<br>
   3.1 [Adding Firebase to Flutter project](#Adding-Firebase-to-Flutter-project)
   
        
4. [Examples](#Examples)


5. [What next!](#What-next!)


## Introduction
A face recognition app using FLutter to demonstrate the use of Firebase SDKs and edge AI with Flutter

ML Kit is a mobile SDK that brings Google's machine learning expertise to Android and iOS apps in a powerful yet easy-to-use package. Whether you're new or experienced in machine learning, you can implement the functionality you need in just a few lines of code. There's no need to have deep knowledge of neural networks or model optimization to get started. On the other hand, if you are an experienced ML developer, ML Kit provides convenient APIs that help you use your custom TensorFlow Lite models in your mobile apps.

Watch this video for a better understanding-

[![youtube.com/watch?v=ejrn_JHksws](http://img.youtube.com/vi/ejrn_JHksws/0.jpg)](http://www.youtube.com/watch?v=ejrn_JHksws "Introducing ML Kit")

## Key capabilities

1. Production-ready for common use cases 	

ML Kit comes with a set of ready-to-use APIs for common mobile use cases: recognizing text, detecting faces, identifying landmarks, scanning barcodes, labeling images, and identifying the language of text. Simply pass in data to the ML Kit library and it gives you the information you need.

2. On-device or in the cloud 	

ML Kit’s selection of APIs run on-device or in the cloud. Our on-device APIs can process your data quickly and work even when there’s no network connection. Our cloud-based APIs, on the other hand, leverage the power of Google Cloud Platform's machine learning technology to give you an even higher level of accuracy.

3. Deploy custom models 	

If ML Kit's APIs don't cover your use cases, you can always bring your own existing TensorFlow Lite models. Just upload your model to Firebase, and we'll take care of hosting and serving it to your app. ML Kit acts as an API layer to your custom model, making it simpler to run and use.

![](https://github.com/Rishit-dagli/MLKit-Firebase/blob/master/images/ML%20kit%20capabilities.png)

## Example (Face detection) 

### Adding Firebase to Flutter project

#### Prerequisites

*   Install your preferred editor or IDE.

*   Make sure that your app meets the following requirements:<br>
        - Flutter SDK<br>
        - Uses Gradle 4.1 or later<br>

*    Set up a device or emulator for running your app. Emulators must use an emulator image with Google Play.

*    [Install Flutter](https://flutter.io/get-started/install/) for your specific operating system, including the following:<br>
        - Flutter SDK<br>
        - Supporting libraries<br>
        - Platform-specific software and SDKs<br>

*    [Sign into Firebase](https://console.firebase.google.com/) using your Google account.

If you don't already have a Flutter app, you can complete the [Get Started: Test Drive](https://flutter.io/get-started/test-drive/#androidstudio) to create a new Flutter app using your preferred editor or IDE.

#### Create a Firebase project

Before you can add Firebase to your Flutter app, you need to create a Firebase project to connect to your app. Visit Understand Firebase Projects to learn more about Firebase projects.


*    In the Firebase console, click Add project, then select or enter a Project name.

*    If you have an existing Google Cloud Platform (GCP) project, you can select the project from the dropdown menu to add Firebase resources to that project.

*    (Optional) If you are creating a new project, you can edit the Project ID.

*    Firebase automatically assigns a unique ID to your Firebase project. Visit Understand Firebase Projects to learn about how Firebase uses the project ID.
*    After Firebase provisions resources for your Firebase project, you cannot change your project ID.
*    To use a specific identifier, you must edit your project ID during this setup step.

*    Click Continue.

 *   (Optional) Set up Google Analytics for your project, which enables you to have an optimal experience using any of the following Firebase products:<br>
    - Firebase Crashlytics<br>
    - Firebase Predictions<br>
    - Firebase Cloud Messaging<br>
    - Firebase In-App Messaging<br>
    - Firebase Remote Config<br>
    - Firebase A/B Testing<br>

 *   When prompted, select to use an existing Google Analytics account or to create a new account.
 *   If you choose to create a new account, select your Analytics reporting location, then accept the data sharing settings and Google Analytics terms for your project.
 *   You can always set up Google Analytics later in the Integrations tab of your settings Project settings.

*    Click Create project (or Add Firebase, if you're using an existing GCP project).

*    Firebase automatically provisions resources for your Firebase project. When the process completes, you'll be taken to the overview page for your Firebase project in the Firebase console.

#### Register your app with Firebase

Important: If you're releasing your Flutter app on both iOS and Android, register both the iOS and Android versions of your app with the same Firebase project.

*    In the center of the Firebase console's project overview page, click the Android icon (plat_android) to launch the setup workflow.

*    If you've already added an app to your Firebase project, click Add app to display the platform options.

*    Enter your app's package name in the Android package name field.
*    Make sure that you enter the ID that your app is actually using. You cannot add or modify this value after you register your app with your Firebase project.
*        A package name is sometimes referred to as an application ID.

*        Find this package name in your module (app-level) Gradle file, usually `app/build.gradle` (example package name: `com.yourcompany.yourproject`).

*    (Optional) Enter other app information as prompted by the setup workflow.<br>

        - App nickname: An internal, convenience identifier that is only visible to you in the Firebase console<br>

        - Debug signing certificate SHA-1: A SHA-1 hash is required by Firebase Authentication (when using Google Sign In or phone number sign in) and Firebase Dynamic Links.<br>

*    Click Register app.

#### Add a Firebase configuration file

 *   Click Download `google-services.json` to obtain your Firebase Android config file (`google-services.json`).<br>
        - You can download your Firebase Android config file again at any time.<br>
        - Make sure the config file is not appended with additional characters, like (2).<br>
        
        
*   Note: The Firebase config file contains unique, but non-secret identifiers for your project.

*    Move your config file into the android/app directory of your Flutter app.

*    To enable Firebase services in your Android app, add the google-services plugin to your Gradle files, as follows:<br>

      - In your root-level (project-level) Gradle file (android/build.gradle), add rules to include the Google Services Gradle plugin. Check that you have Google’s Maven repository, as well.<br>

```
        buildscript {

            repositories {
              // Check that you have the following line (if not, add it):
              google()  // Google's Maven repository
            }

            // ...

            dependencies {
              // ...

              // Add the following line:
              classpath 'com.google.gms:google-services:4.3.3'  // Google Services plugin
            }
        }

        allprojects {
            // ...

            repositories {
              // Check that you have following line (if not, add it):
              google()  // Google's Maven repository
              // ...
            }
        }
```

In your module (app-level) Gradle file (usually `android/app/build.gradle`), apply the Google Services Gradle plugin.

```
// Add the following line:
apply plugin: 'com.google.gms.google-services'  // Google Services plugin

android {
  // ...
}

// ...
```

*    Run flutter packages get.

*    Back in the Firebase console setup workflow, click Next to skip the remaining steps.

*    Continue to Add FlutterFire plugins.

#### Add FlutterFire plugins

Flutter uses plugins to provide access to a wide range of platform-specific services, such as Firebase APIs. Plugins include platform-specific code to access services and APIs on each platform.

Firebase is accessed through a number of different libraries, one for each Firebase product (for example: Realtime Database, Authentication, Analytics, or Storage). Flutter provides a set of Firebase plugins, which are collectively called FlutterFire.

Since Flutter is a multi-platform SDK, each FlutterFire plugin is applicable for both iOS and Android. So, if you add any FlutterFire plugin to your Flutter app, it will be used by both the iOS and Android versions of your Firebase app.

Be sure to check the FlutterFire docs for the most up-to-date list of FlutterFire plugins.

Note: The steps in this section are an example of how to add Flutter-supported Firebase products) to your Flutter-Firebase app (both the iOS and Android versions).

*    Ensure that your app is not currently running in your emulator or on your device.

*    From the root directory of your Flutter app, open your `pubspec.yaml` file.

*    Add the FlutterFire plugin for the Firebase Core Flutter SDK.

    Note: All Flutter-Firebase apps, both iOS and Android versions, require the `firebase_core plugin` for Flutter.

```
    dependencies:
      flutter:
        sdk: flutter
      # Add the dependency for the Firebase Core Flutter SDK
      firebase_core: ^0.4.0+9
```

*   Add the FlutterFire plugins for the Firebase products that you want to use in your app.<br>
(Analytics enabled)

```
dependencies:
  flutter:
    sdk: flutter
  # Check that you have this dependency (added in the previous step)
  firebase_core: ^0.4.0+9

  # Add the dependency for the FlutterFire plugin for Google Analytics
  firebase_analytics: ^5.0.2

  # Add the dependencies for any other Firebase products you want to use in your app
  # For example, to use Firebase Authentication and Cloud Firestore
  firebase_auth: ^0.14.0+5
  cloud_firestore: ^0.12.9+5
```

*    Run flutter packages get.

*    If you added Analytics, run your app to send verification to Firebase that you've successfully integrated Firebase. Otherwise, you can skip the verification step.

You’re all set! Your Flutter app is registered and configured to use Firebase
