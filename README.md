# Titanic for Android

This library is DEPRECATED, as I don't have time to mainatin it anymore. But feel free to go through the code and copy that into your project, it still does its job.

Titanic is an Android experiment reproducing [this effect](http://codepen.io/lbebber/pen/xrwja).

![ScreenShot](titanic.gif)

## How to use

Add a `TitanicTextView` to your layout:
```xml
<com.romainpiel.titanic.TitanicTextView
    android:id="@+id/titanic_tv"
    android:text="@string/loading"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:textColor="#212121"
    android:textSize="70sp"/>
```

To start the animation:
```java
titanic = new Titanic();
titanic.start(myTitanicTextView);
```

You may want to keep track of the titanic instance after the animation is started if you want to stop it.

To stop it:
```java
titanic.cancel();
```

## How does it work?

### Quick version

Titanic is a simple illusion obtained by applying an animated translation on the TextView TextPaint Shader's matrix.

### Less quick version

#### What is a Shader?

A [Shader](http://developer.android.com/reference/android/graphics/Shader.html) is a class defining spans of colors. It is installed in a [Paint](http://developer.android.com/reference/android/graphics/Paint.html). It's usually following a certain strategy, so you have LinearGradient shaders, RadialGradient shaders BitmapShader shaders, etc...

Shader attributes:
- tile mode: how the shader color spans should be repeated on the x and y axis.
- local matrix: can be used to apply transformations on the shader

#### Why are you bugging me with these notions?

Well because it is exaclty what we are using in this experiment.

In [`TitanicTextView`](https://github.com/RomainPiel/Titanic/blob/master/library/src/main/java/com/romainpiel/titanic/library/TitanicTextView.java), we create a BitmapShader containing a wave bitmap.

We set the tile mode to:
- x: `TileMode.REPEAT`. The bitmap is repeated on the x-axis
- y: `Tilemode.CLAMP`. The edge colors are repeated outside the bitmap on the y-axis

We have a `maskX` and a `maskY` variable that will define the position of the shader. So at every `onDraw()` we will take in account these values and translate the shader's local matrix at the right position.

We also have a variable `offsetY` to make the value maskY usable. So when maskY is equal to 0, the wave is at the center of the view.

#### How is it animating?

The animation is based on Android Animator API. I am not going to go through that part. Go read [the documentation](http://developer.android.com/guide/topics/graphics/prop-animation.html) if you need some explanations.

In this experiment there are 2 animations.
- One is moving the wave horizontally from 0 to 200 (the width of the wave bitmap).
- The second one is moving the wave vertically from the bottom half to the top half.

To animate these translations, all we need is to apply an animator on `maskX` and `maskY`. The position of the shader's matrix will be updated automatically in `onDraw()`.

#### I want more examples

Glad you said that. Go check out [Shimmer-android](https://github.com/RomainPiel/Shimmer-android). It's based on the same concept with a `LinearGradient` shader.

## Sample

See the [sample](https://github.com/RomainPiel/Titanic/tree/master/sample) for a common use of this library.

## License
```
Copyright 2014 Romain Piel

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

