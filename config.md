1. powershell 

cd C:\Users\tester\Documents\acode

keytool -genkeypair -v `
  -keystore app-release.keystore `
  -storetype pkcs12 `
  -alias acode `
  -keyalg RSA `
  -keysize 2048 `
  -validity 10000

$encoded = [Convert]::ToBase64String(
  [IO.File]::ReadAllBytes("C:\Users\tester\Documents\acode\app-release.keystore")
)
$encoded | Set-Clipboard

2. Create the GitHub secret:   
  Repository Settings
  Secrets and variables → Actions
  New repository secret
  Name: KEYSTORE_CONTENT
  Paste the encoded value

3. save config.json below to C:\Users\tester\Documents\acode\build.json:

{
  "android": {
    "release": {
      "keystore": "/tmp/app-release.keystore",
      "storePassword": "temp1234",
      "alias": "acode",
      "password": "temp1234",
      "keystoreType": "pkcs12"
    }
  }
}

4. powershell

$encoded = [Convert]::ToBase64String(
  [IO.File]::ReadAllBytes("C:\Users\tester\Documents\acode\build.json")
)
$encoded | Set-Clipboard

5. Create the GitHub secret:
  Repository Settings
  Secrets and variables → Actions
  New repository secret
  Name: BUILD_JSON_CONTENT
  Paste the encoded value
