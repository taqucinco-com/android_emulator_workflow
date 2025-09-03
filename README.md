# android_emulator_workflow

## firebase test lab on Android Device

gcloud 準備
```sh
gcloud auth login
gcloud --quiet config set project <PROJECT_NAME>
```

aab/apk作成
```
fvm flutter build apk --debug
./gradlew app:bundleDebug -Ptarget=<pwd>/../integration_test/counter_test.dart
# e.g. ./gradlew app:bundleDebug -Ptarget=/Users/username/Documents/workspace/flutter/android_emulator_workflow/android/../integration_test/counter_test.dart
./gradlew app:assembleAndroidTest
```

```
# device確認
gcloud firebase test android models list

# test
gcloud firebase test android run --type instrumentation \
--app build/app/outputs/bundle/debug/app-debug.aab \
--test build/app/outputs/apk/androidTest/debug/app-debug-androidTest.apk \
--results-bucket=<BUCKET_NAME> --device=model=akita,version=34

https://github.com/flutter/flutter/tree/main/packages/integration_test#firebase-test-lab
https://cloud.google.com/sdk/gcloud/reference/firebase/test/android/run
https://docs.flutter.dev/testing/integration-tests#test-on-an-android-device
