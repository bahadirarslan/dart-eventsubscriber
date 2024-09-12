# EventSubscriber

[![Pub Package](https://img.shields.io/pub/v/eventsubscriber.svg?style=flat-square)](https://pub.dev/packages/eventsubscriber)

A Flutter widget that rebuilds for every new [Event].

 The `EventSubscriber` widget will be notified and will rebuild when one or more [Event]'s occurs, allowing some changing aspect of an observed object to be displayed in your Flutter user interface.

 Note: run the included Example project to see a working example.

---

### Contents
- [Usage](#usage)
- [See also](#seealso)
- [Dependencies](#dependencies)
- [Examples](#example)
  - [Simple Example](#simple-example)
  - [Using Arguments (EventArgs)](#using-arguments)
- [Requesting Features and Reporting Bugs](#features-and-bugs)

---

 ## [Usage](#usage)

 The Flutter `EventSubscriber` Widget requires that one or more `Event`'s being subscribed to is specified, along with a `builder` (`handler`) that returns a child Widget.

```dart
// example ...
EventSubscriber(
  events: [myCount.valueChangedEvent],
  builder: (context, args) => Text('${myCount.value}'),
),
```

## [See Also](#seealso)

[Event] - A Dart package that broadcasts events to interested subscribers.

## [Dependencies](#dependencies)

- [Flutter][flutter] - This Dart package has a dependency on the `Flutter` framework.
- [Event] - Supports the creation of lightweight custom Dart Events, that allow interested subscribers to be notified that something has happened. Provides a notification mechanism across independent packages/layers/modules.

## [Example](#example)


```dart
import 'package:flutter/material.dart';
import 'package:event/event.dart';
import 'package:eventsubscriber/eventsubscriber.dart';

// An example domain model of a simple Counter
// Normally in its own module/package
// Included here inline for illustration purposes
class Counter {
  int value = 0;
  var valueChangedEvent = Event(); // declare Event

  void increment() {
    value++;
    // Broadcast that the value has changed
    valueChangedEvent.broadcast();
  }
}

//////////////////////

// Create the domain model
var myCount = Counter();

// Flutter application
// The Count domain value will increment when the button is pressed.
// The updated domain value will be automatically updated in the UI.
void main() => runApp(
      MaterialApp(
        home: Column(
          children: <Widget>[
            // Subscribe to the 'valueChanged' domain event
            EventSubscriber(
              events: [myCount.valueChangedEvent],
              builder: (context, args) => Text(myCount.value.toString()),
            ),
            FlatButton(
              child: Text('Increment'),
              // Increment the domain value
              onPressed: () => myCount.increment(),
            )
          ],
        ),
      ),
    );

```

## [Requesting Features and Reporting Bugs](#Features-and-bugs)

Please enter feature requests and report bugs at the [issue tracker][tracker].

[tracker]: https://github.com/aryehof/dart-eventsubscriber/issues
[eventnotifier]: https://pub.dev/packages/eventnotifier
[flutter]: https://flutter.dev/
[event]: https://pub.dev/packages/event
