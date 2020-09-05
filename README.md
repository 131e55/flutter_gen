<p align="center">
  <a href="https://pub.dev/packages/flutter_gen">
    <img src="./art/logo.png" width="480px"/>
  </a>
</p>
<p align="center">
  <a href="https://pub.dartlang.org/packages/flutter_gen">
    <img src="https://img.shields.io/pub/v/flutter_gen.svg">
  </a>
  <a href="https://github.com/wasabeef/flutter_gen/actions?query=workflow%3A%22Flutter+CI%22">
    <img src="https://github.com/wasabeef/flutter_gen/workflows/Flutter%20CI/badge.svg?branch=master" />
  </a>
</p>

The Flutter code generator for your assets, fonts, colors, … — Get rid of all String-based APIs.

Inspired by [SwiftGen](https://github.com/SwiftGen/SwiftGen).

## Motivation.

Using asset path string directly is not safe.

```yaml
# pubspec.yaml
flutter:
  assets:
    - assets/images/profile.jpg
```

❌ **Bad**  
What would happen if you made a typo?

```dart
Widget build(BuildContext context) {
  return Image.asset('assets/images/profile.jpeg');
}

// The following assertion was thrown resolving an image codec:
// Unable to load asset: assets/images/profile.jpeg
```

⭕️ **Good**  
We want to use it safely.

```dart
Widget build(BuildContext context) {
  return Assets.images.profile.image();
}
```

## Installation

### Use this package as an executable

Run `fluttergen` after the configuration [`pubspec.yaml`](https://dart.dev/tools/pub/pubspec).

1. Install [FlutterGen]

```sh
$ pub global activate flutter_gen

$ export PATH="$PATH":"$HOME/.pub-cache/bin"
```

2. Use [FlutterGen]

```sh
$ fluttergen -h

$ fluttergen -c example/pubspec.yaml
```

### Use this package as a part of build_runner

1. Add [build_runner] and [FlutterGen] to your package's pubspec.yaml file:

```
dev_dependencies:
  build_runner:
  flutter_gen:
```

2. Install [FlutterGen]

```sh
$ flutter pub get
```

3. Use [FlutterGen]

```
$ flutter packages pub run build_runner build
```

## Configuration file

[FlutterGen] generates dart files based on the key **`flutter`** and **`flutter_gen`** of [`pubspec.yaml`](https://dart.dev/tools/pub/pubspec).

```yaml
# pubspec.yaml
# ...

flutter_gen:
  output: lib/gen/ # Optional (default: lib/gen/)
  lineLength: 80 # Optional (default: 80)

  colors:
    inputs:
      - assets/color/colors.xml

flutter:
  uses-material-design: true
  assets:
    - assets/images/

  fonts:
    - family: Raleway
      fonts:
        - asset: assets/fonts/Raleway-Regular.ttf
        - asset: assets/fonts/Raleway-Italic.ttf
          style: italic
```

## Available Parsers

### Assets

Just follow the doc [Adding assets and images#Specifying assets](https://flutter.dev/docs/development/ui/assets-and-images#specifying-assets) to specify assets, then [FlutterGen] will generate related dart files.  
No other specific configuration is required.  
_Ignore duplicated._

```yaml
# pubspec.yaml
flutter:
  assets:
    - assets/images/
    - assets/images/chip3/chip.jpg
    - assets/images/chip4/chip.jpg
    - assets/images/icons/paint.svg
    - assets/json/fruits.json
    - pictures/ocean_view.jpg
```

These configurations will generate **`assets.gen.dart`** under the **`lib/gen/`** directory by default.

#### Usage Example

[FlutterGen] generates [Image](https://api.flutter.dev/flutter/widgets/Image-class.html) class if the asset is Flutter supported image format.

Example results of `assets/images/chip.jpg`:

- **`Assets.images.chip`** is an implementation of [`AssetImage class`](https://api.flutter.dev/flutter/painting/AssetImage-class.html).
- **`Assets.images.chip.image(...)`** returns [`Image class`](https://api.flutter.dev/flutter/widgets/Image-class.html).
- **`Assets.images.chip.path`** just returns the path string.

```dart
Widget build(BuildContext context) {
  return Image(image: Assets.images.chip);
}

Widget build(BuildContext context) {
  return Assets.images.chip.image(
    width: 120,
    height: 120,
    fit: BoxFit.scaleDown,
  );

Widget build(BuildContext context) {
  // Assets.images.chip.path = 'assets/images/chip3/chip3.jpg'
  return Image.asset(Assets.images.chip.path);
}

```

In other cases, the asset is generated as String class.

```dart
final svg = SvgPicture.asset(Assets.images.icons.paint);

final json = await rootBundle.loadString(Assets.json.fruits);
```

The root directory will be omitted if it is either **`assets`** or **`asset`**.

```
assets/images/chip3/chip.jpg  => Assets.images.chip3.chip
assets/images/chip4/chip.jpg  => Assets.images.chip4.chip
assets/images/icons/paint.svg => Assets.images.icons.paint
assets/json/fruits.json       => Assets.json.fruits
pictures/ocean_view.jpg       => Assets.pictures.oceanView
```

<details><summary>Example of code generated by FlutterGen</summary>
<p>

```dart
/// GENERATED CODE - DO NOT MODIFY BY HAND
/// *****************************************************
///  FlutterGen
/// *****************************************************

import 'package:flutter/widgets.dart';

class AssetGenImage extends AssetImage {
  const AssetGenImage(String assetName)
      : _assetName = assetName,
        super(assetName);
  final String _assetName;

  Image image({
    ImageFrameBuilder frameBuilder,
    ImageLoadingBuilder loadingBuilder,
    ImageErrorWidgetBuilder errorBuilder,
    String semanticLabel,
    bool excludeFromSemantics = false,
    double width,
    double height,
    Color color,
    BlendMode colorBlendMode,
    BoxFit fit,
    AlignmentGeometry alignment = Alignment.center,
    ImageRepeat repeat = ImageRepeat.noRepeat,
    Rect centerSlice,
    bool matchTextDirection = false,
    bool gaplessPlayback = false,
    bool isAntiAlias = false,
    FilterQuality filterQuality = FilterQuality.low,
  }) {
    return Image(
      image: this,
      frameBuilder: frameBuilder,
      loadingBuilder: loadingBuilder,
      errorBuilder: errorBuilder,
      semanticLabel: semanticLabel,
      excludeFromSemantics: excludeFromSemantics,
      width: width,
      height: height,
      color: color,
      colorBlendMode: colorBlendMode,
      fit: fit,
      alignment: alignment,
      repeat: repeat,
      centerSlice: centerSlice,
      matchTextDirection: matchTextDirection,
      gaplessPlayback: gaplessPlayback,
      isAntiAlias: isAntiAlias,
      filterQuality: filterQuality,
    );
  }

  String get path => _assetName;
}

class $PicturesGen {
  const $PicturesGen();

  AssetGenImage get chip5 => const AssetGenImage('pictures/chip5.jpg');
}

class $AssetsImagesGen {
  const $AssetsImagesGen();

  AssetGenImage get chip2 => const AssetGenImage('assets/images/chip2.jpg');
  AssetGenImage get chip1 => const AssetGenImage('assets/images/chip1.jpg');
  AssetGenImage get logo => const AssetGenImage('assets/images/logo.png');
  AssetGenImage get profile => const AssetGenImage('assets/images/profile.jpg');
  $AssetsImagesChip3Gen get chip3 => const $AssetsImagesChip3Gen();
  $AssetsImagesChip4Gen get chip4 => const $AssetsImagesChip4Gen();
  $AssetsImagesIconsGen get icons => const $AssetsImagesIconsGen();
}

class $AssetsJsonGen {
  const $AssetsJsonGen();

  String get fruits => 'assets/json/fruits.json';
}

class $AssetsImagesChip3Gen {
  const $AssetsImagesChip3Gen();

  AssetGenImage get chip3 =>
      const AssetGenImage('assets/images/chip3/chip3.jpg');
}

class $AssetsImagesChip4Gen {
  const $AssetsImagesChip4Gen();

  AssetGenImage get chip4 =>
      const AssetGenImage('assets/images/chip4/chip4.jpg');
}

class $AssetsImagesIconsGen {
  const $AssetsImagesIconsGen();

  String get paint => 'assets/images/icons/paint.svg';
}

class Assets {
  Assets._();

  static const $AssetsImagesGen images = $AssetsImagesGen();
  static const $AssetsJsonGen json = $AssetsJsonGen();
  static const $PicturesGen pictures = $PicturesGen();
}
```

</p>
</details>

### Fonts

Just follow the doc [Use a custom font](https://flutter.dev/docs/cookbook/design/fonts) to specify fonts, then [FlutterGen] will generate related dart files.  
No other specific configuration is required.  
_Ignore duplicated._

```yaml
# pubspec.yaml
flutter:
  fonts:
    - family: Raleway
      fonts:
        - asset: assets/fonts/Raleway-Regular.ttf
        - asset: assets/fonts/Raleway-Italic.ttf
          style: italic
    - family: RobotoMono
      fonts:
        - asset: assets/fonts/RobotoMono-Regular.ttf
        - asset: assets/fonts/RobotoMono-Bold.ttf
          weight: 700
```

These configurations will generate **`fonts.gen.dart`** under the **`lib/gen/`** directory by default.

#### Usage Example

```dart
Text(
  'Hi there, I\'m FlutterGen',
  style: TextStyle(
    fontFamily: FontFamily.robotoMono,
    fontFamilyFallback: const [FontFamily.raleway],
  ),
```

<details><summary>Example of code generated by FlutterGen</summary>
<p>

```dart
/// GENERATED CODE - DO NOT MODIFY BY HAND
/// *****************************************************
///  FlutterGen
/// *****************************************************

class FontFamily {
  FontFamily._();

  static const String raleway = 'Raleway';
  static const String robotoMono = 'RobotoMono';
}

```

</p>
</details>

### Colors

_Ignore duplicated._

```yaml
# pubspec.yaml
flutter_gen:
  colors:
    inputs:
      - assets/color/colors.xml
      - assets/color/colors2.json
      - assets/color/colors3.xml
```

[FlutterGen] supports the following input file formats:

- a [XML file](example/assets/color/colors.xml), the same format as the Android colors.xml files, containing tags

```xml
<color name="milk_tea">#F5CB84</color>
<color name="cinnamon">#955E1C</color>
<color name="black_50">#80000000</color>
```

- a [JSON file](example/assets/color/colors2.json), representing a dictionary of names -> values, each value being the hex representation of the color

```json
{
  "disabled": "#666666",
  "accent_red": "#FF4D4D"
}
```

These configurations will generate **`colors.gen.dart`** under the **`lib/gen/`** directory by default.

#### Usage Example

```dart
Text(
  'Hi there, I\'m FlutterGen',
  style: TextStyle(
    color: ColorName.denim,
  ),
```

<details><summary>Example of code generated by FlutterGen</summary>
<p>

```dart
/// GENERATED CODE - DO NOT MODIFY BY HAND
/// *****************************************************
///  FlutterGen
/// *****************************************************

import 'package:flutter/painting.dart';

class ColorName {
  ColorName._();

  static const Color white = Color(0xFFFFFFFF);
  static const Color gray70 = Color(0xFFEEEEEE);
  static const Color gray150 = Color(0xFFD8D8D8);
  static const Color gray410 = Color(0xFF979797);
  static const Color gray470 = Color(0xFF878787);
  static const Color gray550 = Color(0xFF737373);
  static const Color gray600 = Color(0xFF666666);
  static const Color gray620 = Color(0xFF606060);
  static const Color gray680 = Color(0xFF525252);
  static const Color gray770 = Color(0xFF37373D);
  static const Color gray800 = Color(0xFF333333);
  static const Color gray860 = Color(0xFF222226);
  static const Color gray880 = Color(0xFF1D1D22);
  static const Color gray900 = Color(0xFF18181C);
  static const Color gray910 = Color(0xFF141418);
  static const Color black = Color(0xFF000000);
  static const Color seaPink = Color(0xFFEB9798);
  static const Color coral = Color(0xFFFE6363);
  static const Color strawberry = Color(0xFFFF4D4D);
  static const Color crimsonRed = Color(0xFFCF2A2A);
  static const Color rustRed = Color(0xFF421E21);
  static const Color milkTea = Color(0xFFF5CB84);
  static const Color cornBrond = Color(0xFFF5CB84);
  static const Color yellowOcher = Color(0xFFDF9527);
  static const Color cinnamon = Color(0xFF955E1C);
  static const Color tulipTree = Color(0xFFE6A53A);
  static const Color gullGray = Color(0xFFA1B3BC);
  static const Color fleryOrange = Color(0xFFB36111);
  static const Color denim = Color(0xFF127DB8);
  static const Color forestGreen = Color(0xFF238833);
  static const Color amazon = Color(0xFF367A62);
  static const Color copperCanyon = Color(0xFF8A4213);
  static const Color russet = Color(0xFF7B5A19);
  static const Color bronzetone = Color(0xFF533C10);
  static const Color bush = Color(0xFF0F3A2B);
  static const Color bronze = Color(0xFF421F0A);
  static const Color highEmphasis = Color(0xFFEEEEEE);
  static const Color mediumEmphasis = Color(0xFF979797);
  static const Color disabled = Color(0xFF666666);
  static const Color accentRed = Color(0xFFFF4D4D);
  static const Color accentYellow = Color(0xFFF2B756);
  static const Color highEmphasis30 = Color(0x4DEEEEEE);
  static const Color white00016 = Color(0x29FFFFFF);
  static const Color white00020 = Color(0x33FFFFFF);
  static const Color white00030 = Color(0x4DFFFFFF);
  static const Color white00032 = Color(0x52FFFFFF);
  static const Color white00040 = Color(0x66FFFFFF);
  static const Color white00060 = Color(0x99FFFFFF);
  static const Color gray91000 = Color(0x00141418);
  static const Color gray91030 = Color(0x4D141418);
  static const Color gray91070 = Color(0xB3141418);
  static const Color gray910100 = Color(0xFF141418);
  static const Color colorAccentDark15 = Color(0x26CF2B2B);
  static const Color colorAccentDark20 = Color(0x33CF2B2B);
  static const Color black30 = Color(0x4D000000);
  static const Color black40 = Color(0x66000000);
  static const Color black50 = Color(0x80000000);
  static const Color black60 = Color(0x99000000);
}
```

</p>
</details>

## Issues

Please file [FlutterGen] specific issues, bugs, or feature requests in our [issue tracker](https://github.com/wasabeef/flutter_gen/issues/new).

Plugin issues that are not specific to [FlutterGen] can be filed in the [Flutter issue tracker](https://github.com/flutter/flutter/issues/new).

## Contributing

**We are looking for co-developers.**

If you wish to contribute a change to any of the existing plugins in this repo,
please review our [contribution guide](https://github.com/wasabeef/flutter_gen/blob/master/CONTRIBUTING.md)
and open a [pull request](https://github.com/wasabeef/flutter_gen/pulls).

### Milestone

- [ ] Documentation (English proofreading)
- [x] Assets generation
- [x] Fonts generation
- [x] Colors generation
  - [x] Support json
  - [x] Support xml
  - [ ] Support clr?
- [x] Support change output path
- [x] Support hierarchical generation  
       'assets/image/home/label.png' => Assets.image.home.label  
       'assets/image/detail/label.png' => Assets.image.detail.label
- [ ] Platforms channels generation

[build_runner]: https://pub.dev/packages/build_runner
[fluttergen]: https://pub.dev/packages/flutter_gen
