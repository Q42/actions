## [upload-symbols-to-firebase](https://github.com/q42/actions/blob/main/upload-symbols-to-firebase/action.yml)

Uploads dSYM files to Firebase Crashlytics using the `upload-symbols` tool from the Firebase iOS SDK.

The action needs to locate the `upload-symbols` binary, which ships as part of the Firebase iOS SDK SPM package. There are three ways to point it at the tool, in order of precedence: an explicit `upload-symbols-path`, a custom `source-packages-path`, or auto-discovery inside `derived-data-path`.

The `archive-path` parameter should point to an Xcode archive bundle (`.xcarchive`). Any dSYM files contained within this archive will be uploaded to Firebase.

The `google-service-info-plist` specifies the path to the `GoogleService-Info.plist` file for your Firebase project.

### Discover via DerivedData

When your build resolves Firebase via SPM and writes its checkouts into the default `DerivedData/<project>/SourcePackages` location, the action can discover `upload-symbols` automatically.

```yml
- name: Upload dSYMs to Firebase Crashlytics
  uses: q42/actions/upload-symbols-to-firebase@v1
  with:
    derived-data-path: ${{ runner.temp }}/DerivedData
    google-service-info-plist: ./MyApp/GoogleService-Info.plist
    archive-path: ${{ runner.temp }}/MyApp.xcarchive
```

### Discover via a custom SPM source packages path

If your build uses `-clonedSourcePackagesDirPath` to keep SPM checkouts outside of DerivedData, pass that same path as `source-packages-path`.

```yml
- name: Upload dSYMs to Firebase Crashlytics
  uses: q42/actions/upload-symbols-to-firebase@v1
  with:
    source-packages-path: ${{ runner.temp }}/SourcePackages
    google-service-info-plist: ./MyApp/GoogleService-Info.plist
    archive-path: ${{ runner.temp }}/MyApp.xcarchive
```

### Specify the `upload-symbols` binary directly

If your project resolves Firebase through a different mechanism (e.g. Cocoapods or a vendored binary), point `upload-symbols-path` at the tool directly.

```yml
- name: Upload dSYMs to Firebase Crashlytics
  uses: q42/actions/upload-symbols-to-firebase@v1
  with:
    upload-symbols-path: ./Pods/FirebaseCrashlytics/upload-symbols
    google-service-info-plist: ./MyApp/GoogleService-Info.plist
    archive-path: ${{ runner.temp }}/MyApp.xcarchive
```
