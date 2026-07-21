# [install-provisioning-profile](https://github.com/q42/actions/blob/main/install-provisioning-profile/action.yml)

Installs the specified provisioning profile so that Xcode can use it.

## Inputs

| Input | Required | Description |
| --- | --- | --- |
| `build-provision-profile-base64` | yes | The base64-encoded build provisioning profile. |

## Example

```yml
- name: Install Provisioning Profile
  uses: q42/actions/install-provisioning-profile@v1
  with:
    build-provision-profile-base64: ${{ vars.PROVISIONING_PROFILE_PRODUCTION }}
```

The example reads from `vars` rather than `secrets` because a provisioning profile is not sensitive (it contains no private key). Storing it as a repository/organization variable keeps it out of your secret store; using a secret works too.
