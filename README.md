# Titanic for Android

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

