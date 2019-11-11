# Darwin Camera <img src="https://user-images.githubusercontent.com/9272830/68128635-18c30500-ff3e-11e9-8a32-c32496d5856f.jpg" width="35%" align="right"></img> 

Camera plugin for [Flutter](https://flutter.io).
Supports both iOS and Android.

- Quickly capture image using the using this plugin without going deep into the implementation of official Camera plugin provides by the flutter developers. 
- Image compression using [flutter_image_compress](https://pub.dev/packages/flutter_image_compress)

<img src="https://img.shields.io/badge/license-MIT-green"></img>

## Screenshots


| Camera Stream                  | Preview Captured Image         |
|     :---:       |     :---:       |
| <img src="https://user-images.githubusercontent.com/9272830/68597615-4ae6e080-04c3-11ea-9e1d-77b002827807.PNG" width="50%" ></img> | <img src="https://user-images.githubusercontent.com/9272830/68597699-69e57280-04c3-11ea-9faf-ef5bbdbf2c9f.PNG" width="50%" ></img> |
| Press the `White circular button` to capture image | Press the `Green button` to save image |
| Press the button at the bottom right to `toggle camera` | Press the close button to `discard captured image` |





## Getting Started

In your flutter project add `darwin_camera` as a dependency in `pubspec.yaml`:

```yml
dependencies:
  ...
  darwin_camera: ^0.0.1
```
### iOS

Add two rows to the `ios/Runner/Info.plist`:

* one with the key `Privacy - Camera Usage Description` and a usage description.
* and one with the key `Privacy - Microphone Usage Description` and a usage description.

Or in text format add the key:

```xml
<key>NSCameraUsageDescription</key>
<string>Can I use the camera please?</string>
<key>NSMicrophoneUsageDescription</key>
<string>Can I use the mic please?</string>
```

### Android

Change the minimum Android sdk version to 21 (or higher) in your `android/app/build.gradle` file.

```
minSdkVersion 21
```



## Usage example
```dart
import 'package:darwin_camera/darwin_camera.dart';

 DarwinCameraResult result = await Navigator.push(
   context,
   MaterialPageRoute(
     builder: (context) => DarwinCamera(
       cameraDescription: cameraDescription,
       filePath: filePath,
       resolution: ResolutionPreset.high,
     ),
   ),
 );

if (result != null && result.isFileAvailable) {
   /// File object returned by Camera.
   print(result.file);
   /// Path where the file is faced. 
   print(result.file.path);
 }

```

### Creating a Image capture Widget

This widget captures an image at a provided file path.

```dart
DarwinCamera({
  
  ///
  /// Flag to enable/disable image compression.
  bool enableCompression = false, 
  
  ///
  /// Disables native back functionality provided by iOS using the swipe gestures.
  bool disableNativeBackFunctionality = false,
  
  /// @Required
  /// List of cameras availale in the device.
  /// 
  /// How to get the list available cameras?
  /// `List<CameraDescription> cameraDescription = await availableCameras();`
  List<CameraDescription> cameraDescription, 
  
  /// @Required
  
  /// Path where the image file will be saved.
  String filePath, 
  
  /// 
  /// Resolution of the image captured
  /// Possible values:
  /// 1. ResolutionPreset.high
  /// 2. ResolutionPreset.medium
  /// 3. ResolutionPreset.low
  ResolutionPreset resolution = ResolutionPreset.high, 

})
```

### Complete example with handling permission
See the [example](https://github.com/atlanhq/darwin-camera/tree/master/example) directory in the github repository



### Directory structure

```
.
├── darwin_camera.dart
└── core
    ├── core.dart
    ├── helper.dart
    └── ui.dart
```

<img src="https://user-images.githubusercontent.com/408863/66741678-a78ab780-ee93-11e9-8d90-b274af222339.png" align="centre" />

