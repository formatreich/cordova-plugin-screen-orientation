#cordova-yoik-screenorientation

Cordova plugin to set/lock the screen orientation in a common way for both iOS and Android.  From version 1.0.0 the
interface is based on the [Screen Orientation API](http://www.w3.org/TR/screen-orientation/).

##Install

cordova plugin add net.yoik.cordova.plugins.screenorientation

###Source
https://github.com/yoik/cordova-yoik-screenorientation


##Orientations

__portrait-primary__
The orientation is in the primary portrait mode.

__portrait-secondary__
The orientation is in the secondary portrait mode.

__landscape-primary__
The orientation is in the primary landscape mode.

__landscape-secondary__
The orientation is in the secondary landscape mode.

__portrait__
The orientation is either portrait-primary or portrait-secondary (sensor).

__landscape__
The orientation is either landscape-primary or landscape-secondary (sensor).

##Usage

    screen.lockOrientation('landscape');

    screen.unlockOrientation();

##Events

Both android and iOS will fire the orientationchange event on the window object.
For this version of the plugin use the window object if you require notification.

i.e.

    function init() {
        window.addEventListener("orientationchange", orientationChange, true);
    }

    function orientationChange(e) {
        var orientation="portrait";
        if(window.orientation == -90 || window.orientation == 90) orientation = "landscape";
        document.getElementById("status").innerHTML+=orientation+"<br>";
    }

For this plugin to follow the API events should be fired on the screen object.
iOS does not currently support events on the _screen_ object so custom event
handling will need to be added (Suggestions welcome!).

##iOS Notes

The iOS version is a combination of the cordova JS callback _window.shouldRotateToOrientation_ and the workaround to recheck the orientation as implemented in https://github.com/Adlotto/cordova-plugin-recheck-screen-orientation.

__If you have a custom implementation of the _window.shouldRotateToOrientation_ it will have to be removed for the plugin to function as expected.__

####iOS6

There has been a few cases where the rotation does not change the width of the viewport

Issue [#1](https://github.com/yoik/cordova-yoik-screenorientation/issues/1) @dokterbob

>It seems to be related to having width=device-width, height=device-height in the meta viewport (which is part of the boilerplate phonegap/cordova app). It can be solved by updating the viewport with width=device-height, height=device-width or simply removing width and height altogether.


Pull requests welcome.
