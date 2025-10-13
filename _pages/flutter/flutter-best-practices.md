---
layout: default
title: Flutter Best Practices
parent: Flutter
nav_order: 1
description: "Essential best practices for writing clean, maintainable Flutter code"
---

# Flutter Best Practices
{: .no_toc }

Essential guidelines and patterns for writing clean, maintainable, and performant Flutter applications.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Code Organization

### Project Structure

Organize your Flutter project with a clear folder structure:

```
lib/
├── main.dart
├── app.dart
├── core/
│   ├── constants/
│   ├── themes/
│   ├── utils/
│   └── routes/
├── features/
│   ├── authentication/
│   │   ├── data/
│   │   ├── domain/
│   │   └── presentation/
│   └── home/
│       ├── data/
│       ├── domain/
│       └── presentation/
├── shared/
│   ├── widgets/
│   ├── models/
│   └── services/
└── config/
    └── environment.dart
```

### Feature-Based Architecture

Organize code by features, not by technical layers:

```dart
// ✅ Good - Feature-based
features/
  authentication/
    login_screen.dart
    signup_screen.dart
    auth_service.dart
    user_model.dart

// ❌ Bad - Layer-based
screens/
  login_screen.dart
  signup_screen.dart
services/
  auth_service.dart
models/
  user_model.dart
```

## Widget Best Practices

### Use Const Constructors

Always use `const` when possible for better performance:

```dart
// ✅ Good
const Text('Hello World')
const SizedBox(height: 16)
const Padding(
  padding: EdgeInsets.all(8.0),
  child: Text('Const child'),
)

// ❌ Bad
Text('Hello World')
SizedBox(height: 16)
```

> **💡 Tip**: Enable `prefer_const_constructors` lint rule to catch this automatically!

### Extract Widgets

Break down large widgets into smaller, reusable components:

```dart
// ❌ Bad - Everything in one widget
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home'),
        actions: [
          IconButton(icon: Icon(Icons.search), onPressed: () {}),
          IconButton(icon: Icon(Icons.settings), onPressed: () {}),
        ],
      ),
      body: Column(
        children: [
          Container(
            padding: EdgeInsets.all(16),
            child: Row(
              children: [
                Icon(Icons.user),
                SizedBox(width: 8),
                Column(
                  children: [
                    Text('John Doe', style: TextStyle(fontSize: 18)),
                    Text('john@example.com'),
                  ],
                ),
              ],
            ),
          ),
          // ... more nested widgets
        ],
      ),
    );
  }
}

// ✅ Good - Extracted widgets
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: _buildAppBar(),
      body: Column(
        children: [
          const UserProfileCard(),
          const PostList(),
        ],
      ),
    );
  }

  AppBar _buildAppBar() {
    return AppBar(
      title: const Text('Home'),
      actions: const [
        SearchButton(),
        SettingsButton(),
      ],
    );
  }
}

class UserProfileCard extends StatelessWidget {
  const UserProfileCard({super.key});

  @override
  Widget build(BuildContext context) {
    return Container(
      padding: const EdgeInsets.all(16),
      child: Row(
        children: [
          const Icon(Icons.user),
          const SizedBox(width: 8),
          Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: const [
              Text('John Doe', style: TextStyle(fontSize: 18)),
              Text('john@example.com'),
            ],
          ),
        ],
      ),
    );
  }
}
```

### Use Keys Wisely

Use keys when you need to preserve state or optimize widget tree updates:

```dart
// ✅ Good - Use keys for stateful widgets in lists
ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) {
    return TodoItem(
      key: ValueKey(items[index].id),
      todo: items[index],
    );
  },
)

// Use GlobalKey sparingly, only when needed
final _formKey = GlobalKey<FormState>();

Form(
  key: _formKey,
  child: Column(children: [...]),
)
```

## State Management

### Choose the Right Solution

Pick state management based on your needs:

```dart
// ✅ Good - setState for simple, local state
class Counter extends StatefulWidget {
  @override
  State<Counter> createState() => _CounterState();
}

class _CounterState extends State<Counter> {
  int _count = 0;

  void _increment() {
    setState(() {
      _count++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Text('Count: $_count');
  }
}

// ✅ Good - Provider for shared state
class CounterProvider extends ChangeNotifier {
  int _count = 0;
  
  int get count => _count;
  
  void increment() {
    _count++;
    notifyListeners();
  }
}

// Usage
ChangeNotifierProvider(
  create: (_) => CounterProvider(),
  child: MyApp(),
)
```

### Avoid setState Pitfalls

```dart
// ❌ Bad - Modifying state without setState
_count++;

// ❌ Bad - async operations in setState
setState(() async {
  await fetchData(); // Don't do this!
});

// ✅ Good - async before setState
Future<void> _loadData() async {
  final data = await fetchData();
  setState(() {
    _data = data;
  });
}

// ✅ Good - Check if mounted
Future<void> _loadData() async {
  final data = await fetchData();
  if (mounted) {
    setState(() {
      _data = data;
    });
  }
}
```

## Performance Optimization

### Use ListView.builder for Long Lists

```dart
// ❌ Bad - Creates all items at once
ListView(
  children: items.map((item) => ItemWidget(item)).toList(),
)

// ✅ Good - Lazy loading
ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) {
    return ItemWidget(items[index]);
  },
)
```

### Optimize Images

```dart
// ✅ Good - Specify dimensions
Image.network(
  'url',
  width: 100,
  height: 100,
  cacheWidth: 100,
  cacheHeight: 100,
)

// ✅ Good - Use cached_network_image
CachedNetworkImage(
  imageUrl: 'url',
  placeholder: (context, url) => CircularProgressIndicator(),
  errorWidget: (context, url, error) => Icon(Icons.error),
)
```

### Avoid Unnecessary Rebuilds

```dart
// ❌ Bad - Entire widget rebuilds
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer<CounterProvider>(
      builder: (context, counter, child) {
        return Column(
          children: [
            Text('Count: ${counter.count}'), // Only this needs to update
            ExpensiveWidget(), // But this rebuilds too!
          ],
        );
      },
    );
  }
}

// ✅ Good - Only rebuild what changes
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Consumer<CounterProvider>(
          builder: (context, counter, child) {
            return Text('Count: ${counter.count}');
          },
        ),
        const ExpensiveWidget(), // Doesn't rebuild
      ],
    );
  }
}
```

## Error Handling

### Handle Async Errors

```dart
// ✅ Good - Proper error handling
Future<void> fetchData() async {
  try {
    final response = await http.get(Uri.parse('url'));
    if (response.statusCode == 200) {
      // Process data
    } else {
      throw Exception('Failed to load data');
    }
  } on SocketException {
    // No internet connection
    showSnackBar('No internet connection');
  } on HttpException {
    // Server error
    showSnackBar('Server error');
  } catch (e) {
    // Unknown error
    showSnackBar('An error occurred: $e');
  }
}
```

### Use Result/Either Pattern

```dart
// ✅ Good - Type-safe error handling
class Result<T> {
  final T? data;
  final String? error;
  
  Result.success(this.data) : error = null;
  Result.failure(this.error) : data = null;
  
  bool get isSuccess => data != null;
  bool get isFailure => error != null;
}

Future<Result<User>> fetchUser() async {
  try {
    final user = await api.getUser();
    return Result.success(user);
  } catch (e) {
    return Result.failure(e.toString());
  }
}

// Usage
final result = await fetchUser();
if (result.isSuccess) {
  print(result.data);
} else {
  print(result.error);
}
```

## Navigation Best Practices

### Use Named Routes

```dart
// ✅ Good - Centralized route management
class AppRoutes {
  static const home = '/';
  static const profile = '/profile';
  static const settings = '/settings';
}

MaterialApp(
  initialRoute: AppRoutes.home,
  routes: {
    AppRoutes.home: (context) => HomePage(),
    AppRoutes.profile: (context) => ProfilePage(),
    AppRoutes.settings: (context) => SettingsPage(),
  },
)

// Navigate
Navigator.pushNamed(context, AppRoutes.profile);
```

### Pass Data Correctly

```dart
// ✅ Good - Pass data via constructor
class DetailsPage extends StatelessWidget {
  final User user;
  
  const DetailsPage({
    Key? key,
    required this.user,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Text(user.name);
  }
}

// Navigate with data
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => DetailsPage(user: user),
  ),
);
```

## Testing Best Practices

### Write Testable Code

```dart
// ❌ Bad - Hard to test
class LoginPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: () async {
        final result = await http.post(/* login */);
        // Handle result
      },
      child: Text('Login'),
    );
  }
}

// ✅ Good - Separated logic, easy to test
class LoginService {
  Future<Result<User>> login(String email, String password) async {
    // Login logic
  }
}

class LoginPage extends StatelessWidget {
  final LoginService loginService;
  
  const LoginPage({required this.loginService});

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: () => _handleLogin(context),
      child: Text('Login'),
    );
  }
  
  Future<void> _handleLogin(BuildContext context) async {
    final result = await loginService.login(email, password);
    // Handle result
  }
}
```

### Widget Testing

```dart
// ✅ Good - Test user interactions
testWidgets('Login button triggers login', (tester) async {
  final mockService = MockLoginService();
  
  await tester.pumpWidget(
    MaterialApp(
      home: LoginPage(loginService: mockService),
    ),
  );
  
  await tester.enterText(find.byType(TextField).first, 'test@example.com');
  await tester.enterText(find.byType(TextField).last, 'password');
  await tester.tap(find.text('Login'));
  await tester.pumpAndSettle();
  
  verify(mockService.login('test@example.com', 'password')).called(1);
});
```

## Code Quality

### Use Linter Rules

Enable strict linting in `analysis_options.yaml`:

```yaml
include: package:flutter_lints/flutter.yaml

linter:
  rules:
    - prefer_const_constructors
    - prefer_const_literals_to_create_immutables
    - avoid_print
    - avoid_unnecessary_containers
    - prefer_final_fields
    - use_key_in_widget_constructors
    - always_declare_return_types
    - prefer_single_quotes
```

### Follow Naming Conventions

```dart
// ✅ Good naming
class UserProfile {}        // PascalCase for classes
const maxRetries = 3;       // camelCase for variables
void fetchUserData() {}     // camelCase for functions
final apiUrl = 'url';       // camelCase for constants

// File names
user_profile.dart          // snake_case for files
user_profile_widget.dart   // descriptive names
```

## Dependency Management

### Use Dependency Injection

```dart
// ✅ Good - Using get_it for DI
final getIt = GetIt.instance;

void setupDependencies() {
  getIt.registerSingleton<ApiService>(ApiService());
  getIt.registerFactory<UserRepository>(
    () => UserRepository(getIt<ApiService>()),
  );
}

// Usage
class HomePage extends StatelessWidget {
  final userRepo = getIt<UserRepository>();
  
  @override
  Widget build(BuildContext context) {
    return FutureBuilder(
      future: userRepo.getUsers(),
      builder: (context, snapshot) { /* ... */ },
    );
  }
}
```

## Security Best Practices

### Never Hardcode Secrets

```dart
// ❌ Bad
const apiKey = 'sk_live_123456789';

// ✅ Good - Use environment variables
import 'package:flutter_dotenv/flutter_dotenv.dart';

final apiKey = dotenv.env['API_KEY'];
```

### Validate Input

```dart
// ✅ Good - Always validate user input
TextFormField(
  validator: (value) {
    if (value == null || value.isEmpty) {
      return 'Please enter some text';
    }
    if (!RegExp(r'^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$').hasMatch(value)) {
      return 'Please enter a valid email';
    }
    return null;
  },
)
```

## Accessibility

### Add Semantic Labels

```dart
// ✅ Good - Accessible widgets
Semantics(
  label: 'Profile picture',
  child: CircleAvatar(
    backgroundImage: NetworkImage(user.avatarUrl),
  ),
)

// Use semantic widgets
IconButton(
  icon: Icon(Icons.favorite),
  tooltip: 'Add to favorites',  // Important!
  onPressed: () {},
)
```

## Documentation

### Document Complex Code

```dart
/// Fetches user data from the API and caches it locally.
///
/// Throws [NetworkException] if the network request fails.
/// Throws [CacheException] if caching fails.
///
/// Returns a [User] object on success.
Future<User> fetchAndCacheUser(String userId) async {
  // Implementation
}
```

## Summary Checklist

Before you commit, check:

- [ ] Used `const` constructors where possible
- [ ] Extracted large widgets into smaller ones
- [ ] Handled errors properly
- [ ] Added tests for critical functionality
- [ ] Followed naming conventions
- [ ] No hardcoded strings or magic numbers
- [ ] Optimized for performance (ListView.builder, image sizes)
- [ ] Added accessibility labels
- [ ] Documented complex logic
- [ ] Ran `flutter analyze` with no issues
- [ ] Formatted code with `flutter format`

## Resources

- [Effective Dart](https://dart.dev/guides/language/effective-dart)
- [Flutter Performance Best Practices](https://docs.flutter.dev/perf/best-practices)
- [Flutter Code Organization](https://codewithandrea.com/articles/flutter-project-structure/)

---

*Last updated: October 2025*