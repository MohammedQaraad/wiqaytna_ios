# Wiqaytna iOS

![alt text](./wiqaytna_logo.png "Wiqaytna Logo")



Wiqaytna is the official Moroccan exposure notification app.
---


## Building the code

1. Install the latest [Xcode developer tools](https://developer.apple.com/xcode/downloads/) from Apple
2. Install [CocoaPods](https://github.com/CocoaPods/CocoaPods)
3. Clone the repository
4. Run `pod install` at root of project

## Configuration

### Setting up Firebase for Staging and Production

The app relies on Firebase functions to work.

1. After setting up Firebase, place your configuration files in the respective directories.

   ```****
   |-- /FIREBASE
       |-- /PROD
           |-- GoogleService-Info.plist
       |-- /STG
           |-- GoogleService-Info.plist
   ```

2. In `Targets > Wiqaytna > Build Phases > Setup Firebase Environment GoogleService-Info.plist`, you will find the code that is used to copy the Plist files into the Plist destination.

3. In `Targets > Wiqaytna > Info > URL Types`, insert the GoogleService-Info.plist `REVERSED_CLIENT_ID` in URL schemes.

### Configuring BlueTrace

You can find BlueTrace config variables at `BluetraceConfig.swift`.

### Setting build variables

To configure STG and PROD variables, define them in `Targets > Wiqaytna > Build Settings > User-Defined` and declare them in `Info.plist`.

These are some of the User-Defined variables.

```
PRODUCT_BUNDLE_IDENTIFIER
FIREBASE_STORAGE_URL
SERVICE_UUID
V2_CHARACTERISTIC_ID
```

### Adding a privacy statement URL

Find `ConsentViewController.swift` and replace the placeholder with your privacy statement URL.

```swift
@IBAction func privacySafeguardsBtn(_ sender: Any) {
        // check if website exists
        guard let url = URL(string: "<PRIVACY_STATEMENT_URL>") else {
            return
        }
...
```

### Setting Firebase remote config

The "Share" message uses Firebase remote config. The key is "ShareText". If it is unable to be retrieved, the app falls back to `defaultShareText`.

## Debug Screen

There is a debug screen accessible within the staging version of the app. This allows you to view the app's Bluetooth communication log. To access it, you first have to set up the app. Then, tap on the home screen image.

## Linting

There's a build script in `Targets > Wiqaytna > Build Phases > Swiftlint` which runs [SwiftLint](https://github.com/realm/SwiftLint) on Build.
Run `{PODS_ROOT}/SwiftLint/swiftlint autocorrect` to auto-fix some linting errors.

## Security Enhancements

SSL pinning is not included as part of the repo

## Statement from Apple

The following is a statement from Apple: "To ensure the credibility of health and safety information, Apple is only accepting COVID-19 related apps from recognised entities such as government organisations, health-focused NGOs, companies deeply credentialed in health issues, and medical or educational institutions. Only developers from one of these recognized entities should submit an app related to COVID-19 to the App Store.

For more information visit <https://developer.apple.com/news/?id=03142020a>"

## Known issues

iOS has limitations on background Bluetooth activity.
