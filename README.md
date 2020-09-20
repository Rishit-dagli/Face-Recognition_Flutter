# Face Recognition_Flutter [![Twitter](https://img.shields.io/twitter/url?style=social&url=https%3A%2F%2Fgithub.com%2FRishit-dagli%2FFace-Recognition_Flutter)](https://twitter.com/intent/tweet?text=Wow:&url=https%3A%2F%2Fgithub.com%2FRishit-dagli%2FFace-Recognition_Flutter)

![Flutter CI](https://github.com/Rishit-dagli/Face-Recognition_Flutter/workflows/Flutter%20CI/badge.svg)
[![Twitter Follow](https://img.shields.io/twitter/follow/rishit_dagli?style=social)](https://twitter.com/intent/follow?screen_name=rishit_dagli)
[![GitHub followers](https://img.shields.io/github/followers/Rishit-dagli?label=Follow&style=social)](https://github.com/Rishit-dagli)

A project which shows you how you code use AI algorithms with Flutter, here I show the example of a Face recognition application with 
Flutter and FireBase. I also gave a talk about this at [Flutter Mumbai Community](https://www.meetup.com/Mumbai-Flutter/) and 
[Flutter Bangalore](https://www.meetup.com/flutter-bangalore-group/events/272057891/). I strongly 
advise you to check out the [talk](https://github.com/Rishit-dagli/Face-Recognition_Flutter/tree/master/talk) folder which has details
regarding the talk.

## Table of contents

- [Introduction](#introduction)
- [Key capabilities](#key-capabilities)
- [Example (Face detection)](#example--face-detection-)
  * [Adding Firebase to Flutter project](#adding-firebase-to-flutter-project)
    + [Prerequisites](#prerequisites)
    + [Create a Firebase project](#create-a-firebase-project)
    + [Register your app with Firebase](#register-your-app-with-firebase)
    + [Add a Firebase configuration file](#add-a-firebase-configuration-file)
    + [Add FlutterFire plugins](#add-flutterfire-plugins)
  * [Some Dependencies](#some-dependencies)
  * [A simple Home Page UI](#a-simple-home-page-ui)
    + [Startup UI](#startup-ui)
    + [Adding a FAB](#adding-a-fab)
  * [Work Flow](#work-flow)
  * [Select an image](#select-an-image)
  * [Load image for processing](#load-image-for-processing)
  * [Perform face detection](#perform-face-detection)
    + [Customising faceDetector](#customising-facedetector)
    + [Get the bounding Box](#get-the-bounding-box)
    + [Fixing a minor problem](#fixing-a-minor-problem)
  * [Drawing over the image](#drawing-over-the-image)
    + [Load images in canvas](#load-images-in-canvas)
    + [Paint the faces](#paint-the-faces)
    + [Another minor problem](#another-minor-problem)
- [Examples](#examples)
- [What next!](#what-next-)

## Introduction
A face recognition app using FLutter to demonstrate the use of Firebase SDKs and edge AI with Flutter

ML Kit is a mobile SDK that brings Google's machine learning expertise to Android and iOS apps in a powerful yet easy-to-use package. Whether you're new or experienced in
machine learning, you can implement the functionality you need in just a few lines of code. There's no need to have deep knowledge of neural networks or model optimization to 
get started. On the other hand, if you are an experienced ML developer, ML Kit provides convenient APIs that help you use your custom TensorFlow Lite models in your mobile apps.

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

> Note: The steps in this section are an example of how to add Flutter-supported Firebase products) to your Flutter-Firebase app (both the iOS and Android versions).

*    Ensure that your app is not currently running in your emulator or on your device.

*    From the root directory of your Flutter app, open your `pubspec.yaml` file.

*    Add the FlutterFire plugin for the Firebase Core Flutter SDK.

>Note: All Flutter-Firebase apps, both iOS and Android versions, require the `firebase_core plugin` for Flutter.

```yaml
dependencies:
  flutter:
    sdk: flutter
  # Add the dependency for the Firebase Core Flutter SDK
  firebase_core: ^0.4.0+9
```

*   Add the FlutterFire plugins for the Firebase products that you want to use in your app.<br>
(Analytics enabled)

```yaml
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

### Some Dependencies

We need the-
* [image_picker](https://pub.dev/packages/image_picker) - So we can easily upload images or  click photos
* [firebase_ml_vision](https://pub.dev/packages/firebase_ml_vision) - To provide us the core Firebase capabilities

So, now my `pubsec.yaml` looks like this-

```yaml
...
...

dependencies:
  flutter:
    sdk: flutter
  image_picker: ^0.6.1+4
  firebase_ml_vision: ^0.9.2+1
  
...
....
```

### A simple Home Page UI

#### Startup UI

```
class FacePage extends StatefulWidget {
  @override
  _FacePageState createState() => _FacePageState();
}

class _FacePageState extends State<FacePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Face Detector')
      ),
      body: Container(),
    );
}
```

Here, we are making a `FacePage` class as a `StatefulWidget`

#### Adding a FAB

Now, you need to add a FLoating Action Button to allow the user to pick an image

```
floatingActionButton: FloatingActionButton(
        onPressed: (){},
        tooltip: 'Pick Image',
        child: Icon(Icons.add_a_photo)
```

We will fill the `onPressed` part later

### Work Flow

1. Select an image
2. Load image for processing
3. Perform face detection

### Select an image

Selecting aan image is very easy in Flutter

```
final imageFile = await ImagePicker.pickImage(
  source: ImageSource.gallery,
);
```

You can change it to

```
source: ImageSource.camera
```

To allow the user to use a camera to upload the image

### Load image for processing

```
final image = FirebaseVisionImage.fromFile(imageFile);
```

This code will load my image file in a format suitable for us to work on it

### Perform face detection

```
final faceDetector = FirebaseVision.instance.faceDetector();
```

Here we are simply initializing an instancce of `FirebaseVision` class with `faceDetector`

You can also try these other models-

```
FirebaseVision.instance.faceDetector();
FirebaseVision.instance.barcodeDetector();
FirebaseVision.instance.labelDetector();
FirebaseVision.instance.textDetector();
FirebaseVision.instance.cloudLabelDetector();
```

#### Customising faceDetector

```
final faceDetector = FirebaseVision.instance.faceDetector(
      FaceDetectorOptions(
        mode: FaceDetectorMode.fast,
        enableLandmarks: true,
)
```

You can make these changes to code to customise the `faceDetector`, you can also experiment with different modes like `fast` and 
`accurate`. The `enableLandmarks` also allows you to detect eyes, ears and nose in a face.

#### Get the bounding Box

This is the `Face` class-

```
class Face{
  final Rectangle<int> boundingBox;
  final double headEulerAngleY;
  final double headEulerAngleZ;
  final double leftEyeOpenProbability;
  final double rightEyeOpenProbability;
  final double smilingProbability;
  final int trackingId;
  FaceLadmark getLandmark(
    FaceLandmarkType landmark,
 ) => _landmarks[landmark]
}
```

We are most interested in the `Rectangle<int> boundingBox` variable and we can easily get its value.

#### Fixing a minor problem

Note: We have 2 `await` while getting image from user and getting faces list. The face page  widget might not be mounted, the 
user could have closed the app too and we could be wasting compute power

So, we will first check if the widget is `mounted` and thenn call `setState()`

```
if (mounted) {
      setState(() {
        _imageFile = imageFile;
        _faces = faces;
     });

```

### Drawing over the image

We will use the `customPaint` widget to do this

A sample `customPaint` widget-

```
final customPaint = CustomPaint(
  painter: myPainter(),
  child: AnyWidget(),
)

class MyPainter extends CustomPainter{
  @override
  void paint(ui.Canvas canvas, ui.Size size){
    // implement paint
  }
  @override
  void shouldRepaint(CustomPainter oldDelegate){
    // implement shoudRepaint
  }
}

```

#### Load images in canvas

We first need to load the images in the `customPainter` canvas before we can draw over them.

```
Future<ui.Image> _loadImage(File file) async {
  final data = await file.readAsBytes();
  return await decodeImageFromList(data);
}

```

So, now my code looks like this

```
class FacePainter extends CustomPainter{
  FacePainter(this.image, this.faces);
  final ui.Image image;
  final List<Rect> faces;

  @override
  void paint(ui.Canvas canvas, ui.Size size){}
  @override
  void shouldRepaint(CustomPainter oldDelegate){
    return null;
 }

```

#### Paint the faces

This is a very simple self explanatory code-

```
@override
  void paint(ui.Canvas canvas, ui.Size size) {
  canvas.drawImage(image, Offset.zero, Paint());
    for (var i = 0; i < faces.length; i++) {
      canvas.drawRect(rects[i], paint);
    }
  }

```

We will now implement `shouldRepaint` 

```
@override
  bool shouldRepaint(FacePainter oldDelegate) {
    return image != oldDelegate.image || faces != oldDelegate.faces;
  }

```

#### Another minor problem

Flutter is not good when you try to draw something out of canvas and your image can go outside of your canvas

```
SizedBox(
            width: _image.width.toDouble(),
            height: _image.height.toDouble(),
            child: CustomPaint(
              painter: FacePainter(_image, _faces),
            ),

```

Placing custom paint in a container and trying to size it is a bad idea!!! So we will use another widget.

```
FittedBox(
          child: SizedBox(
            width: _image.width.toDouble(),
            height: _image.height.toDouble(),
            child: CustomPaint(
              painter: FacePainter(_image, _faces),
            ),

```

## Examples
<br>
<br>

<img src="https://github.com/Rishit-dagli/Face-Recognition_Flutter/blob/master/Screenshots/example1.png" height = 400>
<img src="https://github.com/Rishit-dagli/Face-Recognition_Flutter/blob/master/Screenshots/example2.jpeg" height = 400>

## What next!

You can contribute to this project, all you need to do is submit a pull request. Be sure to first read [CONTRIBUTING.md](https://github.com/Rishit-dagli/Face-Recognition_Flutter/blob/master/CONTRIBUTING.md).
