## [install-certificate](https://github.com/q42/actions/blob/main/install-certificate/action.yml)

Installs the specified certificate in the keychain.

```yml
- name: Install Certificate
  uses: q42/actions/install-certificate@v1
  with:
    build-certificate-base64: ${{ secrets.BUILD_CERTIFICATE_BASE64 }}
    certificate-password: ${{ secrets.BUILD_CERTIFICATE_PASSWORD }}
```
