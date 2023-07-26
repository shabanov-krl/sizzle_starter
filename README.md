# Sizzle Starter

This is an immensely adaptable Flutter starter, crafted with an ideally predetermined layout and encompassing libraries that can be used across a vast array of applications.

To take advantage of this repository, simply click on the "Use this template" button. The subsequent instructions will guide you through the process of integrating and deploying this starter within your distinct projects.

## Features

- 🔥 Rapid installation process
- 🧜 Designed to be flexible, easy to expand, and simple to maintain
- 📦 Assortment of reliable and tested libraries
- 🚛 GitHub Actions and GitLab CI pre-configured
- 🚀 Cutting-edge, feature-oriented architecture
- 📌 Comprehensive documentation and exciting roadmap ahead
- 🐛 Bug reporting, error tracking and analytical capabilities
- 😌 Themes and additional amenities...

## Table Of Contents

- [Sizzle Starter](#sizzle-starter)
  - [Features](#features)
  - [Table Of Contents](#table-of-contents)
  - [Initialization](#initialization)
    - [Initialization Steps](#initialization-steps)
    - [Initialization Progress](#initialization-progress)
    - [Initialization Processor](#initialization-processor)
    - [Dependencies Scope](#dependencies-scope)
  - [Themes](#themes)
  - [Database](#database)
  - [Example Apps](#example-apps)
  - [Recommended libraries](#recommended-libraries)
    - [Core](#core)
    - [External](#external)
  - [Destructive Libraries](#destructive-libraries)
    - [hive](#hive)
    - [getx](#getx)
    - [get\_it](#get_it)
    - [ferry](#ferry)
    - [flutter\_hooks](#flutter_hooks)
    - [mobx](#mobx)
    - [riverpod](#riverpod)
    - [hydrated\_bloc](#hydrated_bloc)
  - [Resources](#resources)
  - [How to guides](#how-to-guides)
    - [How to run](#how-to-run)
    - [How to add a new dependency](#how-to-add-a-new-dependency)
  - [Star History](#star-history)
  - [Credits](#credits)

## Initialization

### Initialization Steps

Here are the steps to initialize the dependencies. It is a map of steps, where the key is the name of the step and the value is a function that fills the `initialization_progress` model. The steps are executed in the order in which they are specified in the map, which gives you the ability to access the results of the previous steps.

### Initialization Progress

```dart
abstract interface class Dependencies {
  /// Shared preferences
  abstract final SharedPreferences sharedPreferences;

  /// App router
  abstract final AppRouter router;

  /// Freeze dependencies, so they cannot be modified
  Dependencies freeze();
}
```

In `dependencies` you can store the results of the steps. There is mutable a model that is passed to each step and then immutable one is returned to the `InitializationProcessor` which maps it to the immutable model.

### Initialization Processor

`InitializationProcessor` as said previously is controlling all the stuff. It is responsible for running the steps, storing the result of each and mapping it to the immutable model. It returns `InitializationResult` with spent time, immutable progress model, etc. Later, all the results are delivered by inherited widgets and can be accessed from BuildContext, see `dependencies_scope` which is in the widget folder.

### Dependencies Scope

`DependenciesScope` is inherited widget that provides access to `Dependendencies`. It is a great DI in a flutter way which gives you a possibility to access your initialized dependencies from context which exists in each widget.

## Themes

Color scheme is generated by [Material Theme Builder](https://www.figma.com/community/plugin/1034969338659738588/Material-Theme-Builder). Then, generated code is added to `core/theme/color_schemes.dart`. Then, pretty simple theme datas are passed to MaterialApp in `app_context.dart`. This way you can easily change the color scheme of the app with many pros:

- Creating own design system in Figma
- Support of dynamic color schemes
- Easy to change the color scheme
- All Material widgets that come with Flutter are already supported and use the color scheme

## Database

`Sizzle starter` comes with drift and its executors preinstalled in `packages/database`. It is **recommended** to use drift for database management.

If you are building for the *Web* too, you should go to [https://drift.simonbinder.eu/web/](https://drift.simonbinder.eu/web/) and follow the instructions.

## Example Apps

1. [Catty](https://github.com/hawkkiller/catty) - simple, but pretty app that uses ChatGPT and cats api to show different cat pictures and generate the facts.
2. [AuthEx](https://github.com/hawkkiller/authex) - an example of implementing request authentication, interceptors and route guards.
3. [Midjourney Client UI](https://github.com/hawkkiller/midjourney_client_ui) - this app utilizes the midjourney_client library to generate images.

## Recommended libraries

### Core

- [async] - Future, Stream, Completer, FutureOr, Zone
- [collection] - List, Map, Queue, extensions
- [convert] - JSON, UTF8, ASCII, Base64, Hex, LineSplitter
- [core] - Object, num, int, double, bool, String, RegExp, Duration, DateTime, Stopwatch, Uri
- [developer] - log, Timeline, TimelineTask, TimelineTaskArgument
- [meta] - annotations
- [typed_data] - ByteData, Endian, Float32List, Float64List, Int16List, Int32List, Int64List, Int8List, Uint16List, Uint32List, Uint64List, Uint8ClampedList, Uint8List
- [js] - interop with JavaScript
- [math] - Math library: Random, min, max, pow, sin, cos, tan, atan2, e, pi, ...
- [io] - I/O support for non web applications
- [http] - A composable, Future-based library for making HTTP requests

### External

- [bloc] - An implementation of the BLoC pattern which helps implement the business logic layer of an application
- [flutter_bloc] - Flutter Widgets that make it easy to integrate blocs into Flutter
- [sentry] - Sentry client for Dart and Flutter
- [firebase_crashlytics] - Firebase Crashlytics for Flutter
- [firebase_analytics] - Firebase Analytics for Flutter
- [firebase_messaging] - Firebase Cloud Messaging for Flutter
- [drift] - A type-safe, composable SQL client for Dart and Flutter
- [sqflite] - A wrapper around SQLite for Flutter, but I'd recommend to use [drift] instead
- [shared_preferences] - A persistent key-value store for Flutter
- [rive] - Great tool and library for creating animations. Moreover, their editor is also written in Flutter.
- [rxdart] - RxDart is a reactive programming library for Dart and Flutter. It provides a set of extension methods on Dart Streams and StreamControllers to transform and combine streams in a declarative way. It also provides a set of Subjects that extend StreamControllers to allow for broadcasting of the latest value(-s) to new listeners.
- [stream_transform] - A collection of Stream transformers
- [path] - A library that provides a cross-platform API for manipulating paths.
- [url_launcher] - A Crossplatform Flutter plugin for launching urls.
- [funvas] - Funvas is a library for creating animations in Flutter. It is a wrapper around the Canvas API, which makes it easy to create animations.

## Destructive Libraries

### [hive]

1. **Lack of thorough testing**: Compared to SQLite, Hive has significantly less testing, raising concerns about its reliability.
2. **No built-in failure recovery**: If a Hive database encounters an issue, it doesn't have a built-in mechanism to recover or fallback.
3. **Complexity of queries**: Simple key-value queries are straightforward, but anything more complex requires a significant amount of code.
4. **Non-standard**: Hive is not an industry standard and its implementation appears to be hastily put together.
5. **Poor support and maintenance**: The database seems to have been abandoned, and its maintenance is questionable.
6. **No migration support**: Any changes to models can potentially crash the application, and the only workaround seems to be deleting the entire database with each version.
7. **Mutable models**: This can cause problems in a database.
8. **Misleading documentation and benchmarks**: Claims made in the documentation and benchmarks don't match the actual performance.
9. **Performance issues**: Hive is significantly slower than SQLite.
10. **Small community**: Hive's community is much smaller compared to SQLite's, leading to less support and fewer resources.
11. **Memory management issues**: Hive keeps all data in memory, which can cause issues for larger datasets.
12. **Hardcoded adapters and keys**: This makes the code hard to follow and maintain.
13. **No synchronization between isolates**: Attempting to interact with the same box across isolates can lead to a crash.
14. **Poor code generation**: The autogenerated code is difficult to work with, making JSON storage or protobufs in shared_preferences seem like better alternatives.
15. **Lack of database features**: Hive lacks key database features like relations, foreign keys, joins, triggers, virtual and generated fields, views, and temporary tables.
16. **Complexity of testing**: Testing Hive databases is non-intuitive compared to SQLite where a :memory: database can be used.
17. **Limited capabilities**: Lack of support for handling JSON or in-database search functionality.
18. **No field indexes**: Any non-key-based queries require full database scans.
19. **No transactions**: Hive does not support transactions, making it unsuitable for financial applications.
20. **Reliability issues**: Due to many of the above reasons, Hive's reliability is questionable.
21. **Limited external software support**: There's a lack of tools to interact with Hive, hindering inspection and design of the database.
22. **Non-transferable experience**: Due to its non-standard nature and project abandonment, time spent learning Hive could be considered wasted, with limited transferable knowledge or benefits to one's career.

### [getx]

GetX is a library for Flutter that tries to combine everything in one package like navigation, state-management, storage, etc. Therefore, it is usually considered as a framework. However, everything is not so good. Even an idea to combine all the stuff is mad from the beginning. Moreover, the source code is awful. It has a lot of bugs, not only talking about the documentation, coverage, etc. On top of that, there is no single approach to write the code. In addition, the idea of how to manage the logic\business logic and all the stuff is completely non-engineering. That is why projects that use this lib are very difficult to maintain. Hence many problems arise. It becomes really tough to produce new features, releases.

### [get_it]

Service locator with all the problems that come in. Basically, you register your objects in the map and access them throughthout the app. Obviously, having a possibility to access any object wherever you want from any place is a destructive idea. For example, you can pull one entity out of a completely different layer and/or location in the application, change its state, dispose resources, and so on. Even if you know it's not good to do that, it still doesn't prohibit you from doing it, or juniors with less experience. Moreover, in such cases it's better to have global variables, because they will be more understandable. To summarize, you deprive yourself of a clear dependency injection, moreover, you are likely to violate the principle of dependency inversion. If you still need the [get_it], then I would recommend you to use [injectable]. All in all, constructors are the best way to inject dependencies. In Flutter, you can use BuildContext to inject dependencies.

### [ferry]

GraphQL codegen for Dart and Flutter. Generally, it is usable, but generates a lot of code. It can happen that at some point the time spent on codegen and build will be more than a few hours, or even not work at all. Moreover, using this package is fraught with the fact that the size of your application will also be increased by huge numbers, 20-60 megabytes

### [flutter_hooks]

Hooks are only pointless tricks, imposing their own rules and complicating the flow. Also, the creation of subscriptions, animations will be greatly complicated. To summarize, this package will not make your life easier, you will not write code faster, on the contrary, you are more likely to have difficulties. I would advise you to use snippets instead and a more Flutter way with StatefulWidget and State.

### [mobx]

MobX is a reactive state management library. You are likely to have many implicit subscriptions that cause rebuilds. I'd suggest to use [bloc] or Value Notifier instead.

### [riverpod]

Riverpod is kinda popular library for state *management*. It is based on global variables that store state. Let alone creating a bunch of global variables, it is also a bad idea to store state in global variables. Moreover, it is not easy to test.

### [hydrated_bloc]

Hydrated Bloc is a library that allows you to persist bloc state. It is a bad idea to persist state. It is better to persist data, but not state. For example, you emitted an error or loading state. It was persisted. Next time, when user opens the app they will see an error or loading state.

## Resources

1. [Flutter docs](https://flutter.dev/docs) - official docs, one of the best ways of learning
2. [Dart docs](https://dart.dev/guides) - official dart docs
3. [DartPad](https://dartpad.dev/) - it's a great tool to play with Dart, has some examples and tutorials
4. [Flutter CodeLabs](https://flutter.dev/docs/codelabs) - Flutter Google Codelabs(great starting point)
5. [Dart CodeLabs](https://dart.dev/codelabs) - Dart Google Codelabs(very little, but still)
6. [Great Roadmap](https://plugfox.dev/flutter-developer-roadmap/)
7. [Communities](https://plugfox.dev/communities/)
8. [Influencers](https://plugfox.dev/influencers/)
9. [Human Resources](https://plugfox.dev/hr/)
10. [Flutter Fundamentals](https://plugfox.dev/flutter-fundamentals/)
11. [Flutter Awesome](https://github.com/Solido/awesome-flutter)
12. [Dart Awesome](https://github.com/yissachar/awesome-dart)
13. [Flutter Channel](https://www.youtube.com/@flutterdev)

## How to guides

### How to run

1. Click `Use this template` button
2. Clone this repository via `git clone`
3. Decide which platforms your app will be running on
4. Run `flutter create . --org com.yourdomain --platforms ios,android,... or nothing if you are writing an app for each platform` in your terminal.
5. Run `flutter pub get` to install all dependencies
6. Run `flutter run` to run your app
7. Here you go, start coding!

### How to add a new dependency

**This section describes how to add a new dependency to your app.** Please, check the [initialization](#initialization) section before.

1. Open `lib/src/feature/initialization/model/dependencies.dart`
2. Add new dependency to `Dependencies$Mutable` and `Dependencies$Immutable`
3. Go to `lib/src/feature/initialization/logic/initialization_steps.dart`
4. Add new entry to the map and write down all the logic needed to initialize your dependency and set it in the `Dependencies$Mutable` object
5. Now, you can use the dependency in the app receiving it from context.

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hawkkiller/sizzle_starter&type=Date)](https://star-history.com/#hawkkiller/sizzle_starter&Date)

## Credits

- [Purple Starter](https://github.com/purplenoodlesoop) - Yakov Karpov
- [Plugfox](https://github.com/PlugFox) - Michael Matiunin

[//]: <recommended>
[bloc]: https://pub.dev/packages/bloc
[flutter_bloc]: https://pub.dev/packages/flutter_bloc
[sqflite]: https://pub.dev/packages/sqflite
[drift]: https://pub.dev/packages/drift
[shared_preferences]: https://pub.dev/packages/shared_preferences
[sentry]: https://pub.dev/packages/sentry
[firebase_crashlytics]: https://pub.dev/packages/firebase_crashlytics
[firebase_analytics]: https://pub.dev/packages/firebase_analytics
[firebase_messaging]: https://pub.dev/packages/firebase_messaging
[rive]: https://pub.dev/packages/rive
[path]: https://pub.dev/packages/path
[funvas]: https://pub.dev/packages/funvas
[stream_transform]: https://pub.dev/packages/stream_transform
[url_launcher]: https://pub.dev/packages/url_launcher
[rxdart]: https://pub.dev/packages/rxdart

[//]: <core>
[async]: https://api.flutter.dev/flutter/dart-async/dart-async-library.html
[collection]: https://api.dart.dev/stable/2.19.2/dart-collection/dart-collection-library.html
[convert]: https://api.dart.dev/stable/2.19.2/dart-convert/dart-convert-library.html
[core]: https://api.dart.dev/stable/2.19.2/dart-core/dart-core-library.html
[developer]: https://api.flutter.dev/flutter/dart-developer/dart-developer-library.html
[meta]: https://api.flutter.dev/flutter/meta/meta-library.html
[typed_data]: https://api.dart.dev/stable/2.19.2/dart-typed_data/dart-typed_data-library.html
[js]: https://api.dart.dev/stable/2.19.2/dart-js/dart-js-library.html
[math]: https://api.dart.dev/stable/2.19.2/dart-math/dart-math-library.html
[io]: https://api.dart.dev/stable/2.19.2/dart-io/dart-io-library.html
[http]: https://pub.dev/packages/http

[//]: <not recommended>
[hive]: https://pub.dev/packages/hive
[getx]: https://pub.dev/packages/get
[get_it]: https://pub.dev/packages/get_it
[injectable]: https://pub.dev/packages/injectable
[ferry]: https://pub.dev/packages/ferry
[riverpod]: https://pub.dev/packages/riverpod
[flutter_hooks]: https://pub.dev/packages/flutter_hooks
[hydrated_bloc]: https://pub.dev/packages/hydrated_bloc
[mobx]: https://pub.dev/packages/mobx
