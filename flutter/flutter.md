# Flutter

Use stable channel:

```shell
flutter channel stable
flutter upgrade
```

## Web support

- [Building a web application](https://docs.flutter.dev/platform-integration/web/building)

```shell
flutter config --enable-web
```

### Run/debug in Chrome

```shell
flutter run -d chrome
```

When running in Chrome shows blank browser, use `--web-renderer html` flag with `flutter run command`.
Add the flag in [Android studio](https://developer.android.com/studio/run/rundebugconfig).

### Run/debug web server

```shell
flutter run -d web-server
```

The web-server device requires the Dart Debug Chrome extension for debugging. (Was not able to resolve with debugging)
