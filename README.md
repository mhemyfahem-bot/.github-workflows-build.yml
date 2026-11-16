name: Build APK
on:
  workflow_dispatch:
  push:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: unzip -q MyDaySystem.zip
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 17
      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: 8.7
      - run: gradle assembleDebug --no-daemon
        working-directory: MyDaySystem
      - uses: actions/upload-artifact@v4
        with:
          name: MyDaySystem-apk
          path: MyDaySystem/app/build/outputs/apk/debug/app-debug.apk# .github-workflows-build.yml
