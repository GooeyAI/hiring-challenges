# Dart typed JSON

This test will test how well you understand the Dart type system,
as well as your basic JSON syntax knowledge.

Note that we expect you to enable <a href="https://dart.dev/null-safety">sound null-safety</a>;
you will encounter compiler warnings for null safety which you are expected to fix.



### Time expectations

For seasoned flutter developers ~ 30 minutes.

For novice flutter developers ~ 5 hours.



### Code


To start, paste the following code into an editor.

```dart
import 'dart:convert';

void main() {
  String someJson = """{
   "iceCreams": [
      {
         "flavor": "raspberry",
         "color": "red"
      },
      {
         "flavor": "banana",
         "color": "yellow",
      }
   ]
  }""";

  var json = jsonDecode(someJson);

  // (Part 2) should print raspberry
  print(json[0]["flavor"]);

  // (Part 3) how is this even possible?
  print(json["iceCreams"][0].toUpperCase());
}
```



### Part 1

Run the above code. You should immediately see an error that looks like this -

```
Unhandled exception:
FormatException: Unexpected character (at line 10, character 7)
      }
      ^

#0      _ChunkedJsonParser.fail (dart:convert-patch/convert_patch.dart:1405:5)
#1      _ChunkedJsonParser.parse (dart:convert-patch/convert_patch.dart:929:13)
#2      _parseJson (dart:convert-patch/convert_patch.dart:40:10)
#3      JsonDecoder.convert (dart:convert/json.dart:612:36)
#4      JsonCodec.decode (dart:convert/json.dart:216:41)
#5      jsonDecode (dart:convert/json.dart:155:10)
#6      main (file:///code.dart:17:14)
#7      _delayEntrypointInvocation.&lt;anonymous closure> (dart:isolate-patch/isolate_patch.dart:297:19)
#8      _RawReceivePortImpl._handleMessage (dart:isolate-patch/isolate_patch.dart:192:12)
```



### Part 2

(line 20) Change the code so that it prints `raspberry`

```dart
// (Part 2) should print raspberry
print(json[0]["flavor"]);
```

### Part 3


This is a "reverse" coding challenge, in that you need to change the code such that does **not**
*compile*.

If we look at line 23, we see that it calls an undefined method `.toUpperCase()` on a `Map` object.

```dart
print(json["iceCreams"][0].toUpperCase());
```

The thing to note here is that we only discover this issue at *runtime* -

```
Unhandled exception:
NoSuchMethodError: Class '_InternalLinkedHashMap&lt;String, dynamic>' has no instance method 'toUpperCase'.
Receiver: _LinkedHashMap len:2
Tried calling: toUpperCase()
#0      Object.noSuchMethod (dart:core-patch/object_patch.dart:38:5)
#1      main (file:///code.dart:23:30)
#2      _delayEntrypointInvocation.&lt;anonymous closure> (dart:isolate-patch/isolate_patch.dart:297:19)
#3      _RawReceivePortImpl._handleMessage (dart:isolate-patch/isolate_patch.dart:192:12)
```

Imagine a scenario where we have millions of lines of code, doing JSON parsing in some part, and using the parsed object in another. Keeping track of the type of objects can be a challenge.

Fortunately, the dart compiler has got our back!

Tweak this code such that it takes full advantage of the dart static type system, and this class of human error is rendered impossible.

If you do this right, the dart compiler should spit out a *compile-time* error that looks something like this -

```
code.dart:30:31: Error: The method 'toUpperCase' isn't defined for the class 'Map<String, String>'.
 - 'Map' is from 'dart:core'.
Try correcting the name to the name of an existing method, or defining a method named 'toUpperCase'.
  print(json["iceCreams"][0].toUpperCase());
                             ^^^^^^^^^^^
```

