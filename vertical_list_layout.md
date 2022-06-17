# Vertical ListView layout

### Task

1. Fix the errors in the provided code to render a vertical layout of 3 indpendent `ListView`s, as shown in this video -

https://user-images.githubusercontent.com/19492893/174288598-788b0d12-6875-43e0-8794-25538f3e3b5a.mp4

2. Figure out *why* this problem arises, and gain an in-depth understanding of [fluttter layout constraints](https://docs.flutter.dev/development/ui/layout/constraints). Include this explaination in the video you send to us.


### Code 

Run the following code -

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(),
        body: Column(
          children: [
            for (int i = 0; i < 3; i++)
              Column(
                children: [
                  Text(
                    "Set ${i}",
                    style: Theme.of(context).textTheme.headline6,
                  ),
                  Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: ListView(
                      children: [
                        for (int j = 0; j < 100; j++)
                          Center(
                            child: Text("{${i}, ${j}}"),
                          ),
                      ],
                    ),
                  ),
                ],
              ),
          ],
        ),
      ),
    );
  }
}
```

It should give you the following error - 

```
======== Exception caught by rendering library =====================================================
The following assertion was thrown during performResize():
Vertical viewport was given unbounded height.

Viewports expand in the scrolling direction to fill their container. In this case, a vertical viewport was given an unlimited amount of vertical space in which to expand. This situation typically happens when a scrollable widget is nested inside another scrollable widget.

If this widget is always nested in a scrollable widget there is no need to use a viewport because there will always be enough vertical space for the children. In this case, consider using a Column instead. Otherwise, consider using the "shrinkWrap" property (or a ShrinkWrappingViewport) to size the height of the viewport to the sum of the heights of its children.

The relevant error-causing widget was: 
  ListView ListView:file:///Users/dev/Projects/dara/dara-client/lib/main_null_safe.dart:26:28
When the exception was thrown, this was the stack: 
#0      RenderViewport.computeDryLayout.<anonymous closure> (package:flutter/src/rendering/viewport.dart:1375:15)
#1      RenderViewport.computeDryLayout (package:flutter/src/rendering/viewport.dart:1436:6)
#2      RenderBox.performResize (package:flutter/src/rendering/box.dart:2384:12)
#3      RenderObject.layout (package:flutter/src/rendering/object.dart:1866:9)
#4      RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:116:14)
#5      RenderObject.layout (package:flutter/src/rendering/object.dart:1887:7)
#6      RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:116:14)
#7      RenderObject.layout (package:flutter/src/rendering/object.dart:1887:7)
 [84 more...]
The following RenderObject was being processed when the exception was fired: RenderViewport#45b67 NEEDS-LAYOUT NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
...  needs compositing
...  parentData: <none> (can use size)
...  constraints: BoxConstraints(0.0<=w<=376.7, 0.0<=h<=Infinity)
...  size: MISSING
...  axisDirection: down
...  crossAxisDirection: right
...  offset: ScrollPositionWithSingleContext#57249(offset: 0.0, range: null..null, viewport: null, ScrollableState, AlwaysScrollableScrollPhysics -> ClampingScrollPhysics -> RangeMaintainingScrollPhysics, IdleScrollActivity#881ef, ScrollDirection.idle)
...  anchor: 0.0
RenderObject: RenderViewport#45b67 NEEDS-LAYOUT NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
  needs compositing
  parentData: <none> (can use size)
  constraints: BoxConstraints(0.0<=w<=376.7, 0.0<=h<=Infinity)
  size: MISSING
  axisDirection: down
  crossAxisDirection: right
  offset: ScrollPositionWithSingleContext#57249(offset: 0.0, range: null..null, viewport: null, ScrollableState, AlwaysScrollableScrollPhysics -> ClampingScrollPhysics -> RangeMaintainingScrollPhysics, IdleScrollActivity#881ef, ScrollDirection.idle)
  anchor: 0.0
...  center child: RenderSliverPadding#5e63a NEEDS-LAYOUT NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
...    parentData: paintOffset=Offset(0.0, 0.0)
...    constraints: MISSING
...    geometry: null
...    padding: EdgeInsets.zero
...    textDirection: ltr
...    child: RenderSliverList#4696d NEEDS-LAYOUT NEEDS-PAINT
...      parentData: paintOffset=Offset(0.0, 0.0)
...      constraints: MISSING
...      geometry: null
...      no children current live
====================================================================================================

======== Exception caught by rendering library =====================================================
The following assertion was thrown during performLayout():
RenderBox was not laid out: RenderViewport#45b67 NEEDS-LAYOUT NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
'package:flutter/src/rendering/box.dart':
Failed assertion: line 1982 pos 12: 'hasSize'


Either the assertion indicates an error in the framework itself, or we should provide substantially more information in this error message to help you determine and fix the underlying cause.
In either case, please report this assertion by filing a bug on GitHub:
  https://github.com/flutter/flutter/issues/new?template=2_bug.md

The relevant error-causing widget was: 
  ListView ListView:file:///Users/dev/Projects/dara/dara-client/lib/main_null_safe.dart:26:28
When the exception was thrown, this was the stack: 
#2      RenderBox.size (package:flutter/src/rendering/box.dart:1982:12)
#3      RenderViewport.performLayout (package:flutter/src/rendering/viewport.dart:1453:39)
#4      RenderObject.layout (package:flutter/src/rendering/object.dart:1887:7)
#5      RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:116:14)
#6      RenderObject.layout (package:flutter/src/rendering/object.dart:1887:7)
#7      RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:116:14)
#8      RenderObject.layout (package:flutter/src/rendering/object.dart:1887:7)
#9      RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:116:14)
 [83 more...]
(elided 6 frames from class _AssertionError, class _RawReceivePortImpl, class _Timer, and dart:async-patch)
The following RenderObject was being processed when the exception was fired: RenderViewport#45b67 NEEDS-LAYOUT NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
...  needs compositing
...  parentData: <none> (can use size)
...  constraints: BoxConstraints(0.0<=w<=376.7, 0.0<=h<=Infinity)
...  size: MISSING
...  axisDirection: down
...  crossAxisDirection: right
...  offset: ScrollPositionWithSingleContext#57249(offset: 0.0, range: null..null, viewport: null, ScrollableState, AlwaysScrollableScrollPhysics -> ClampingScrollPhysics -> RangeMaintainingScrollPhysics, IdleScrollActivity#881ef, ScrollDirection.idle)
...  anchor: 0.0
RenderObject: RenderViewport#45b67 NEEDS-LAYOUT NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
  needs compositing
  parentData: <none> (can use size)
  constraints: BoxConstraints(0.0<=w<=376.7, 0.0<=h<=Infinity)
  size: MISSING
  axisDirection: down
  crossAxisDirection: right
  offset: ScrollPositionWithSingleContext#57249(offset: 0.0, range: null..null, viewport: null, ScrollableState, AlwaysScrollableScrollPhysics -> ClampingScrollPhysics -> RangeMaintainingScrollPhysics, IdleScrollActivity#881ef, ScrollDirection.idle)
  anchor: 0.0
...  center child: RenderSliverPadding#5e63a NEEDS-LAYOUT NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
...    parentData: paintOffset=Offset(0.0, 0.0)
...    constraints: MISSING
...    geometry: null
...    padding: EdgeInsets.zero
...    textDirection: ltr
...    child: RenderSliverList#4696d NEEDS-LAYOUT NEEDS-PAINT
...      parentData: paintOffset=Offset(0.0, 0.0)
...      constraints: MISSING
...      geometry: null
...      no children current live
====================================================================================================
```