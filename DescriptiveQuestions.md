1. What is the difference between Hot Reload and Hot Restart?
Ans - Hot Reload is like page refresh to view UI or data changes. 
      When running the flutter app from terminal we can use 'r' to perform Hot Reload
    - Hot Restart is starting the app from start again. It's a complete restart.
   
2. What are the different ways we can create a custom widget?
Ans - We can create a new file and create a widget which can either be State Less or State Full.
    - Example:

```dart
class CustomAppBar extends StatelessWidget with PreferredSizeWidget {
  final String title;
  final List<Widget>? actions;
  final bool isHomeScreen;

  const CustomAppBar({Key? key, this.actions, this.isHomeScreen = false, required this.title}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return AppBar(
      elevation: 4,
      actions: actions,
      title: Text(title),
      leading: IconButton(icon: const Icon(Icons.arrow_back), onPressed: () => (isHomeScreen ? exit(0) : Navigator.pop(context))),
    );
  }

  @override
  Size get preferredSize => const Size.fromHeight(kToolbarHeight);
}

```

4. How can I access platform(iOS or Android) specific code from Flutter?
Ans - We can access Native code by using Method Channel on both the Platforms.

5. What do you know about eventloop and what is the relationship with isolates?
Ans - Eventloop I don't know.
    - But Isolates are like threads in Dart which are used to perform long running operations.
    - Isolates are used with Sender Port and Receiver Port.
