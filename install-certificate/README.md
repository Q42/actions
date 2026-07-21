# [install-certificate](https://github.com/q42/actions/blob/main/install-certificate/action.yml)

Installs the code signing certificate(s) from a base64-encoded P12 file into a temporary keychain. A P12 may contain more than one certificate; all of them are imported.

## Inputs

| Input | Required | Description |
| --- | --- | --- |
| `build-certificate-base64` | yes | The base64-encoded P12 build certificate. |
| `certificate-password` | yes | The password for the P12 build certificate. |
| `keychain-password` | no | Password for the temporary keychain the certificate is imported into. Defaults to a randomly generated value (`uuidgen`) when unset or empty, which is fine for most CI runs. |

## Example

```yml
- name: Install Certificate
  uses: q42/actions/install-certificate@v1
  with:
    build-certificate-base64: ${{ secrets.BUILD_CERTIFICATE_BASE64 }}
    certificate-password: ${{ secrets.BUILD_CERTIFICATE_PASSWORD }}
```
