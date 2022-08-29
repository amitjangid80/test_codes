1. Refactor the code below so that the children will wrap to the next line when the display width is
   small for them to fit.

Ans - Refactored code

```dart
class LongStringWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Wrap(
      children: [
        Chip(label: Text('I')),
        Chip(label: Text('am')),
        Chip(label: Text('looking')),
        Chip(label: Text('for')),
        Chip(label: Text('a')),
        Chip(label: Text('job')),
        Chip(label: Text('and')),
        Chip(label: Text('I')),
        Chip(label: Text('need')),
        Chip(label: Text('a')),
        Chip(label: Text('job')),
      ],
    );
  }
}
```

2. News API Ans -

```dart
class News {
   String? author;
   String? content;
   String? date;
   String? id;
   String? imageUrl;
   String? readMoreUrl;
   String? time;
   String? title;
   String? url;

   News({
      required this.author,
      required this.content,
      required this.date,
      required this.id,
      required this.imageUrl,
      required this.readMoreUrl,
      required this.time,
      required this.title,
      required this.url,
   });

   factory News.fromJson(Map<String, dynamic> newsJson) => News(
      author: newsJson['author'],
      content: newsJson['content'],
      date: newsJson['date'],
      id: newsJson['id'],
      imageUrl: newsJson['imageUrl'],
      readMoreUrl: newsJson['readMoreUrl'],
      time: newsJson['time'],
      title: newsJson['title'],
      url: newsJson['url'],
   );
}

Future<List<News>> getAllNewsCategory() async {
   const String api = 'https://inshorts.deta.dev/news?category=all';
   final response = await http.get(Uri.parse(api));

   printLog('response status code is: ${response.statusCode}');
   printLog('response body is: ${response.body}');

   if (response.statusCode == 200) {
      final List<News> newsList =
      jsonDecode(response.body)['data'].map<News>((newsJson) => News.fromJson(newsJson)).toList();

      return newsList;
   }

   return [];
}
```

3. Identify the problem in the following code block and correct it.
Ans - The problem is the loop will take too long to complete and the print statement will be printing the last value of the loop.
    - The solution is to use Isolates so the UI is not stuck.

```dart
isolateFunction() async {
   final receivePort = ReceivePort();

   await Isolate.spawn(longOperationMethod, receivePort.sendPort);

   receivePort.listen((counting) {
      debugPrint('$counting! items I print the value!');
   });
}

longOperationMethod(SendPort sendPort) {
   var counting = 0;

   for (var i = 1; i < 1000000000; i++) {
      counting += i;
   }

   sendPort.send(counting);
}
```
