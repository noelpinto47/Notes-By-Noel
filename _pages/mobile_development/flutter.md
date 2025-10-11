---
layout: default
title: Flutter
parent: Mobile Development
nav_order: 1
description: "Google's UI toolkit for building beautiful, natively compiled applications"
---

# Flutter
{: .no_toc }

Google's UI toolkit for building beautiful, natively compiled applications for mobile, web, desktop, and embedded devices from a single codebase.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## What is Flutter?

Flutter is an open-source UI software development kit created by Google. It allows developers to build natively compiled applications for mobile, web, and desktop from a single codebase using the Dart programming language.

### Key Features

- 🎨 **Beautiful UI**: Pixel-perfect designs with customizable widgets
- ⚡ **Fast Development**: Hot reload helps you see changes instantly
- 🚀 **Native Performance**: Compiled to native ARM code for optimal performance
- 🌐 **Cross-Platform**: Build for iOS, Android, web, and desktop from one codebase
- 🧩 **Rich Widgets**: Extensive catalog of customizable Material and Cupertino widgets
- 📦 **Great Packages**: Robust ecosystem with thousands of packages on pub.dev

## Why Choose Flutter?

### Single Codebase

Write once, deploy everywhere. One codebase for multiple platforms means:
- Faster development cycles
- Easier maintenance
- Consistent user experience
- Reduced development costs

### Hot Reload

See changes in your app almost instantly without losing state:

```dart
// Make a change
Text('Hello, World!')

// Save the file
// See the update in <1 second!
```

### Expressive UI

Everything is a widget in Flutter, making it easy to compose complex UIs:

```dart
Column(
  children: [
    Text('Welcome to Flutter'),
    ElevatedButton(
      onPressed: () => print('Clicked!'),
      child: Text('Click Me'),
    ),
  ],
)
```

## Core Concepts

### Everything is a Widget

In Flutter, everything you see is a widget - from structural elements to stylistic elements:

- **Structural Widgets**: `Container`, `Row`, `Column`, `Stack`
- **Styling Widgets**: `Padding`, `Center`, `SizedBox`
- **Interactive Widgets**: `Button`, `TextField`, `Slider`
- **Custom Widgets**: Build your own reusable components

### State Management

Flutter offers various approaches to manage app state:

1. **setState()** - For simple, local state
2. **Provider** - Recommended by Flutter team
3. **Riverpod** - Modern, compile-safe provider
4. **BLoC** - Business Logic Component pattern
5. **GetX** - Lightweight and powerful
6. **Redux** - Predictable state container

### Widget Tree

Flutter apps are structured as a tree of widgets:

```dart
MaterialApp
└── Scaffold
    ├── AppBar
    │   └── Text
    └── Body
        └── Column
            ├── Text
            └── Button
```

## Getting Started

### Installation

1. **Download Flutter SDK**
   ```bash
   # macOS (with Homebrew)
   brew install flutter
   
   # Or download from flutter.dev
   ```

2. **Verify Installation**
   ```bash
   flutter doctor
   ```

3. **Create First App**
   ```bash
   flutter create my_app
   cd my_app
   flutter run
   ```

### Hello World Example

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Hello Flutter',
      theme: ThemeData(
        primarySwatch: Colors.green,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Welcome to Flutter'),
        ),
        body: Center(
          child: Text(
            'Hello, Flutter! 🚀',
            style: TextStyle(fontSize: 24),
          ),
        ),
      ),
    );
  }
}
```

## Common Widgets

### Layout Widgets

**Container** - Box model widget
```dart
Container(
  width: 100,
  height: 100,
  color: Colors.blue,
  child: Text('Box'),
)
```

**Row & Column** - Horizontal and vertical layouts
```dart
Row(
  mainAxisAlignment: MainAxisAlignment.spaceAround,
  children: [
    Icon(Icons.star),
    Icon(Icons.favorite),
    Icon(Icons.share),
  ],
)
```

**Stack** - Overlay widgets
```dart
Stack(
  children: [
    Image.network('url'),
    Positioned(
      bottom: 10,
      right: 10,
      child: Icon(Icons.favorite),
    ),
  ],
)
```

### Interactive Widgets

**Button**
```dart
ElevatedButton(
  onPressed: () {
    print('Button pressed!');
  },
  child: Text('Click Me'),
)
```

**TextField**
```dart
TextField(
  decoration: InputDecoration(
    labelText: 'Enter your name',
    border: OutlineInputBorder(),
  ),
  onChanged: (value) {
    print('Input: $value');
  },
)
```

## Navigation

### Basic Navigation

```dart
// Navigate to new screen
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SecondScreen()),
);

// Go back
Navigator.pop(context);
```

### Named Routes

```dart
MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => HomeScreen(),
    '/details': (context) => DetailsScreen(),
  },
);

// Navigate using route name
Navigator.pushNamed(context, '/details');
```

## Networking

### HTTP Requests

```dart
import 'package:http/http.dart' as http;
import 'dart:convert';

Future<void> fetchData() async {
  final response = await http.get(
    Uri.parse('https://api.example.com/data'),
  );
  
  if (response.statusCode == 200) {
    final data = json.decode(response.body);
    print(data);
  }
}
```

### Using Dio Package

```dart
import 'package:dio/dio.dart';

final dio = Dio();

Future<void> getData() async {
  try {
    final response = await dio.get('https://api.example.com/data');
    print(response.data);
  } catch (e) {
    print('Error: $e');
  }
}
```

## Useful Packages

### Essential Packages

| Package | Purpose |
|:--------|:--------|
| `provider` | State management |
| `dio` | HTTP client |
| `shared_preferences` | Local storage |
| `sqflite` | SQLite database |
| `cached_network_image` | Image caching |
| `flutter_bloc` | BLoC pattern |
| `get_it` | Dependency injection |
| `go_router` | Declarative routing |

### UI Packages

| Package | Purpose |
|:--------|:--------|
| `flutter_svg` | SVG rendering |
| `lottie` | Animations |
| `shimmer` | Loading placeholders |
| `flutter_animate` | Easy animations |
| `carousel_slider` | Image carousels |

## Development Tips

> **💡 Tip**: Use `const` constructors whenever possible for better performance!

```dart
// Good
const Text('Hello')

// Avoid
Text('Hello')
```

> **💡 Tip**: Extract repeated widgets into separate classes or methods

```dart
// Extract to method
Widget _buildCard(String title) {
  return Card(
    child: Text(title),
  );
}
```

> **⚠️ Warning**: Avoid deeply nested widget trees. Extract into smaller widgets instead.

## Testing

### Widget Tests

```dart
testWidgets('Counter increments', (WidgetTester tester) async {
  await tester.pumpWidget(MyApp());
  
  expect(find.text('0'), findsOneWidget);
  
  await tester.tap(find.byIcon(Icons.add));
  await tester.pump();
  
  expect(find.text('1'), findsOneWidget);
});
```

### Unit Tests

```dart
test('Addition works', () {
  expect(2 + 2, equals(4));
});
```

## Performance Optimization

1. **Use const constructors** - Reduces widget rebuilds
2. **Avoid rebuilding entire widget trees** - Use keys and selective rebuilds
3. **Lazy load lists** - Use `ListView.builder` for long lists
4. **Optimize images** - Use appropriate formats and sizes
5. **Profile your app** - Use Flutter DevTools

## Resources

### Official Documentation
- [Flutter.dev](https://flutter.dev) - Official website
- [Flutter Docs](https://docs.flutter.dev) - Comprehensive documentation
- [Dart Language](https://dart.dev) - Dart programming language
- [Widget Catalog](https://docs.flutter.dev/ui/widgets) - All Flutter widgets

### Learning Resources
- [Flutter Codelabs](https://docs.flutter.dev/codelabs) - Hands-on tutorials
- [Flutter Cookbook](https://docs.flutter.dev/cookbook) - Recipe-style guides
- [Flutter YouTube](https://www.youtube.com/c/flutterdev) - Official videos
- [Awesome Flutter](https://github.com/Solido/awesome-flutter) - Curated resources

### Community
- [Flutter Discord](https://discord.gg/rflutterdev)
- [r/FlutterDev](https://reddit.com/r/FlutterDev)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/flutter)

## Next Steps

Ready to dive deeper? Check out:
- [Flutter Best Practices](flutter-best-practices) - Tips for writing clean, maintainable Flutter code
- Build your first real app
- Explore the widget catalog
- Join the Flutter community

---

*Last updated: October 2025*
