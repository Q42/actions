## [upload-symbols-to-firebase](https://github.com/q42/actions/blob/main/upload-symbols-to-firebase/action.yml)

Uploads dSYM files to Firebase Crashlytics using the `upload-symbols` tool from the Firebase iOS SDK.

```yml
- name: Upload dSYMs to Firebase Crashlytics
  uses: q42/actions/upload-symbols-to-firebase@main
  with:
    derived-data-path: ${{ runner.temp }}/DerivedData
    google-service-info-plist: ./MyApp/GoogleService-Info.plist
    archive-path: ${{ runner.temp }}/MyApp.xcarchive
```

By default, the action discovers the `upload-symbols` tool from the Firebase iOS SDK SPM checkout inside `derived-data-path`. If your project resolves Firebase via a different mechanism, pass `upload-symbols-path` to point at the tool directly.
