## [cmp-change-version](https://github.com/q42/actions/blob/main/cmp-change-version/action.yml)

Overrides the app version code, and optionally the version name, of a Compose Multiplatform project for all later steps in the job.

By default the version code is the workflow run number plus `version-code-offset`, so every build gets a higher version code than the previous one. That way an Android build can be installed over the previous one, and an iOS build can be uploaded to TestFlight again.

The action sets `ORG_GRADLE_PROJECT_<property>` environment variables through `GITHUB_ENV`. Gradle reads these as project properties, which take precedence over `gradle.properties`. This works without changing tracked files, and also applies to Gradle calls started by Xcode, such as `embedAndSignAppleFrameworkForXcode`.

Your build scripts must read the version from Gradle project properties. By default the action uses `appVersionCode` and `appVersionName`; use `version-code-property` and `version-name-property` if your project uses different names.

### Use the run number as version code

```yml
- name: Change app version
  uses: q42/actions/cmp-change-version@v1
```

### Add an offset

Use an offset when the project already has published builds with a higher version code than the current run number.

```yml
- name: Change app version
  id: app_version
  uses: q42/actions/cmp-change-version@v1
  with:
    version-code-offset: 1000

- run: echo "Building version code ${{ steps.app_version.outputs.version-code }}"
```

### Set an explicit version code and version name

```yml
- name: Change app version
  uses: q42/actions/cmp-change-version@v1
  with:
    version-code: 42
    version-name: 1.2.0
```

### Inputs

| Input                   | Default          | Description                                                                         |
|-------------------------|------------------|-------------------------------------------------------------------------------------|
| `version-code`          |                  | Explicit version code. Defaults to the run number plus `version-code-offset`.      |
| `version-code-offset`   | `0`              | Added to the run number. Ignored when `version-code` is set.                        |
| `version-code-property` | `appVersionCode` | Gradle project property that holds the version code.                                |
| `version-name`          |                  | Version name. Not overridden when empty.                                            |
| `version-name-property` | `appVersionName` | Gradle project property that holds the version name.                                |

### Outputs

| Output         | Description                      |
|----------------|----------------------------------|
| `version-code` | The version code that was set.   |
