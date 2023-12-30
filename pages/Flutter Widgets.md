tags:: [[Flutter]]

- # Flutter Widgets
	- In [[Flutter]], widgets are the basic building blocks used to create user interfaces. They are essentially reusable components that can be combined to create complex UI layouts. Widgets describe how their visual elements should be rendered on the screen, and they can represent anything from a simple button to an entire screen layout.
	- Two types of Flutter Widgets
		- **Stateless Widgets**
			- These are immutable widgets that don't change their state during the runtime of an app. They are used for UI elements that don't need to change dynamically, such as text, icons, or simple containers.
			- Example of a stateless widget
			  ```dart
			  import 'package:flutter/material.dart';
			  
			  class MyStatelessWidget extends StatelessWidget {
			    const MyStatelessWidget({Key? key}) : super(key: key);
			  
			    @override
			    Widget build(BuildContext context) {
			      return Container(
			        padding: const EdgeInsets.all(8),
			        color: Colors.blue,
			        child: Center(
			          child: Text('Hello world!', style: Theme.of(context).textTheme.headline4),
			        ),
			      );
			    }
			  }
			  ```
		- **Stateful Widgets**
			- These widgets can maintain state and update their appearance based on changes in data or user interactions. They are used for dynamic elements like forms, animations, or screens that update based on user input.
			- Example of a stateful widget
			  ```dart
			  import 'package:flutter/material.dart';
			  
			  class MyStatefulWidget extends StatefulWidget {
			    const MyStatefulWidget({Key? key}) : super(key: key);
			  
			    @override
			    State<MyStatefulWidget> createState() => _MyStatefulWidgetState();
			  }
			  
			  class _MyStatefulWidgetState extends State<MyStatefulWidget> {
			  
			    int _counter = 0;
			  
			    void _incrementCounter() {
			      setState(() {
			        _counter++;
			      });
			    }
			  
			    @override
			    Widget build(BuildContext context) {
			      return Scaffold(
			        appBar: AppBar(title: Text('Stateful Widget')), 
			        body: Center(
			          child: Text('My count: $_counter', 
			                    style: Theme.of(context).textTheme.headline4),
			        ),
			        floatingActionButton: FloatingActionButton(
			          onPressed: _incrementCounter,
			          tooltip: 'Increment',
			          child: Icon(Icons.add),
			        ),
			      );
			    }
			  }
			  ```
	- Flutter's widget system is highly flexible and allows for the creation of complex and customizable user interfaces. Widgets can be nested, combined, and customized to build intricate UI designs, making Flutter a powerful framework for building cross-platform applications with expressive and performant user interfaces.