This example creates a Material app. Material is a visual design language that is standard on mobile and the web. Flutter offers a rich set of Material widgets.
The main method uses fat arrow (=>) notation, Use fat arrow notation for one-line functions or methods.
The app extends StatelessWidget, which makes the app itself a widget. In Flutter, almost everything is a widget, including alignment, padding, and layout.
The Scaffold widget, from the Material library, provides a default app bar, a title, and a body property that holds the widget tree for the home screen. The widget subtree can be quite complex.
A widget's main job is to provide a build method that describes how to display the widget in terms of other, lower-level widgets.
The body for this example consists of a Center widget containing a Text child widget. The Center widget aligns its widget subtree to the center of the screen.
Tip: When pasting code into your app, indentation can become skewed. You can fix this automatically with the Flutter tools:
Android Studio / IntelliJ IDEA: Right-click the dart code and select Reformat Code with dartfmt.
VS Code: Right-click and select Format Document.
Terminal: Run flutter format <filename>.
---------------
Import new library 

4. Use an external package
In this step, you'll start using an open-source package named english_words, which contains a few thousand of the most used English words plus some utility functions.
You can find the english_words package, as well as many other open source packages, on pub.dartlang.org.
 The pubspec file manages the assets for a Flutter app. In pubspec.yaml, append english_words: ^3.1.0(english_words 3.1.0 or higher) to the dependencies list:
dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^0.1.0
  english_words: ^3.1.0   # add this line
While viewing the pubspec in Android Studio's editor view, click Packages get. This pulls the package into your project. You should see the following in the console:
flutter packages get
Running "flutter packages get" in startup_namer...
Process finished with exit code 0
In lib/main.dart, import the new package:
import 'package:flutter/material.dart';
import 'package:english_words/english_words.dart';  // Add this line.
As you type, Android Studio gives you suggestions for libraries to import. It then renders the import string in gray, letting you know that the imported library is unused (so far).
Next, you'll use the english_words package to generate the text instead of using the string "Hello World".


TIPS 
Tip: "Pascal case" (also known as "upper camel case"), means that each word in the string, including the first one, begins with an uppercase letter. So, "upper camel case" becomes "UpperCamelCase".

IMPORTANT

/////
Stateless widgets are immutable, meaning that their properties can't change—all values are final.

Stateful widgets maintain state that might change during the lifetime of the widget. Implementing a stateful widget requires at least two classes: 1) a StatefulWidget class that creates an instance of 2) a State class. The StatefulWidget class is, itself, immutable, but the State class persists over the lifetime of the widget.
///

Add Icon on ROW to trailing(Al Final)

Widget _buildRow(WordPair pair) {
  final bool alreadySaved = _saved.contains(pair);
  return new ListTile(
    title: new Text(
      pair.asPascalCase,
      style: _biggerFont,
    ),
    trailing: new Icon(   // Add the lines from here...
      alreadySaved ? Icons.favorite : Icons.favorite_border,
      color: alreadySaved ? Colors.red : null,
    ),                    // ... to here.
  );
}

Add interactivity (onTap)

Widget _buildRow(WordPair pair) {
  final alreadySaved = _saved.contains(pair);
  return new ListTile(
    title: new Text(
      pair.asPascalCase,
      style: _biggerFont,
    ),
    trailing: new Icon(
      alreadySaved ? Icons.favorite : Icons.favorite_border,
      color: alreadySaved ? Colors.red : null,
    ),
    onTap: () {      // Add 9 lines from here...
      setState(() {
        if (alreadySaved) {
          _saved.remove(pair);
        } else { 
          _saved.add(pair); 
        } 
      });
    },               // ... to here.
  );
}
////

Navigate to a new screen
In this step, you'll add a new page (called a route in Flutter) 
@override
  Widget build(BuildContext context) {
    //final wordPair = new WordPair.random(); // Delete these...
    //return new Text(wordPair.asPascalCase); // ... two lines.

    return new Scaffold(
      // Add from here...
      appBar: new AppBar(
        title: new Text('App test Flutter List&Navigator'),
        actions: <Widget>[
          // Add 3 lines from here...
          new IconButton(icon: const Icon(Icons.list), onPressed: _pushSaved),
        ], // ... to here.
      ),
      body: _buildSuggestions(),
    ); // ... to here.
  } // ... to this line.

  Widget _buildRow(WordPair pair) {
    final alreadySaved = _saved.contains(pair);
    return new ListTile(
      title: new Text(
        pair.asPascalCase,
        style: _biggerFont,
      ),
      trailing: new Icon(
        alreadySaved ? Icons.favorite : Icons.favorite_border,
        color: alreadySaved ? Colors.red : null,
      ),
      onTap: () {
        // Add 9 lines from here...
        setState(() {
          if (alreadySaved) {
            _saved.remove(pair);
          } else {
            _saved.add(pair);
          }
        });
      }, // ... to here.
    );
  }


void _pushSaved() {
    Navigator.of(context).push(
      new MaterialPageRoute<void>(
        builder: (BuildContext context) {
          final Iterable<ListTile> tiles = _saved.map(
                (WordPair pair) {
              return new ListTile(
                title: new Text(
                  pair.asPascalCase,
                  style: _biggerFont,
                ),
              );
            },
          );
          final List<Widget> divided = ListTile
              .divideTiles(
            context: context,
            tiles: tiles,
          )
              .toList();

          return new Scaffold(         // Add 6 lines from here...
            appBar: new AppBar(
              title: const Text('Saved Suggestions'),
            ),
            body: new ListView(children: divided),
          );                           // ... to here.
        },
      ),
    );
  }
}


////

Change the UI using Themes
change an app's theme by configuring the ThemeData class. This app currently uses the default theme, but you'll change the app's primary color to white.

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Startup Name Generator',
      theme: new ThemeData(          // Add the 3 lines from here... 
        primaryColor: Colors.white,
      ),                             // ... to here.
      home: new RandomWords(),
    );
  }
}

////

Top Flutter-compatible packages

https://pub.dartlang.org/flutter/



https://codelabs.developers.google.com/codelabs/first-flutter-app-pt2/#5

https://codelabs.developers.google.com/codelabs/flutter-firebase/index.html#0

https://medium.com/flutter-community/building-a-chat-app-with-flutter-and-firebase-from-scratch-9eaa7f41782e

