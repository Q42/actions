## [install-provisioning-profile](https://github.com/q42/actions/blob/main/install-provisioning-profile/action.yml)

Installs the specified provisioning profile so that Xcode can use it.

```yml
- name: Install Provisioning Profile
  uses: q42/actions/install-provisioning-profile@v1
  with:
    build-provision-profile-base64: ${{ vars.PROVISIONING_PROFILE_PRODUCTION }}
```
