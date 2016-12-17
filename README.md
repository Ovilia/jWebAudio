jWebAudio
=========

JavaScript Web Audio library designed for web games with both jQuery version and standard version.

Examples and API available at http://01org.github.com/jWebAudio/ .

License
-------

```
Copyright (C) 2013, Intel Inc. All rights reserved.

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

Get started
===========

This example shows how to play sound instantly when loaded.

jQuery Version
--------------

[jQuery.js][jquery] and [build/jquery.jWebAudio.js][jqueryJWA] should always be included to use the jQuery version.

```html
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js"></script>
<script type="text/javascript" src="build/jquery.jWebAudio.js"></script>
```

In the HTML file, you should add DOM elements to store the sound information. Each element stores one piece of sound information.

```html
<div id="audio">You may not want this to be displayed.</div>
```

If these elements are not expected to be visible, you may add a class name to them and make them invisible using css.

Here is how to play sound instantly when loaded.

```javascript
$('#audio').jWebAudio('addSoundSource', {
    'url': 'resource/a.ogg',
    'preLoad': true,
    'callback': function() {
        $('#audio').jWebAudio('play');
    }
});
```

Standard Version
------------------

[build/standard.jWebAudio.js][njqueryJWA] alone should be included to use the standard version.
```html
<script type="text/javascript" src="build/standard.jWebAudio.js"></script>
```

Standard version uses SoundEngine to add sound source and returns the instance(s) of sound source when added.

```javascript
var engine = new jWebAudio.SoundEngine();
// source may be used later for operations like pause, stop and so on.
var source = engine.addSoundSource({
    'url': 'resource/a.ogg',
    'preLoad': true,
    'callback': function() {
        source.sound.play();
    }
});
```

Examples
========

Add Sound Source
----------------

jQuery version

```javascript
/* Create sound to be used later */
$('#audio').jWebAudio('addSoundSource', {
    'url': 'resource/a.ogg',
    'volume': 90
});
```

Standard Version

```javascript
var engine = new jWebAudio.SoundEngine();
var source = engine.addSoundSource({
    'url': 'resource/a.ogg',
    'volume': 90
});
```

Load
----

jQuery version

```javascript
$('#audio').jWebAudio('load', function() {
    alert('loaded!');
});
```

Standard Version

```javascript
source.load(function() {
    alert('loaded!');
});
```

PreLoad
-------

jQuery version

```javascript
$('#audio').jWebAudio('addSoundSource', {
    'url': 'resource/a.ogg',
    'preLoad': true,
    'callback': function() {
        alert('loaded');
    }
});
```

Standard Version

```javascript
var engine = new jWebAudio.SoundEngine();
var source = engine.addSoundSource({
    'url': 'resource/a.ogg',
    'preLoad': true,
    'callback': function() {
        alert('loaded');
    }
});
```

Play
----

jQuery version

```javascript
$('#audio').jWebAudio.('play');
```

Standard Version

```javascript
source.sound.play();
```

Pause
-----

jQuery version

```javascript
$('#audio').jWebAudio.('pause');
```

Standard Version

```javascript
source.sound.pause();
```

Stop
----

jQuery version

```javascript
$('#audio').jWebAudio.('stop');
```

Standard Version

```javascript
source.sound.stop();
```

Volume
------

jQuery version

```javascript
$('#audio').jWebAudio('options', {
    'volume': parseInt(100)
});
```

Standard Version

```javascript
sound.setVolume(100);
```

Mute
----

jQuery version

```javascript
$('#audio').jWebAudio('options', {
    'muted': true
});
```

Standard Version

```javascript
sound.setMuted(true);
```

Loop
----

Non-multishot sound can be set to loop after certain interval.

jQuery version

```javascript
$('#audio').jWebAudio('addSoundSource', {
    'url': 'resource/a.ogg',
    'loop': true,
    'loopGap': 3 // in seconds, default 0
});
```

Standard Version

```javascript
var engine = new jWebAudio.SoundEngine();
var source = engine.addSoundSource({
    'url': 'resource/a.ogg'
    'loop': true,
    'loopGap': 3 // in seconds, default 0
});
```

Seek
----

jQuery version

```javascript
$('#audio').jWebAudio('seek', 10);
```

Standard Version

```javascript
source.sound.seek(10);
```

Multishot
---------

jQuery version

```javascript
$('#audio').jWebAudio('addSoundSource', {
    'url': 'resource/a.ogg',
    'multishot': true
});
```

Standard Version

```javascript
var engine = new jWebAudio.SoundEngine();
var source = engine.addSoundSource({
    'url': 'resource/a.ogg',
    'multishot': true
});
```

Sound Effects
-------------

jQuery version

```javascript
// Add sound effect
// Returns id of effect
var id = $('#div1').jWebAudio('addEffect', 'telephonize');
// Delete with id
$('#div1').jWebAudio('deleteEffect', id);
// Delete all effects
$('#div1').jWebAudio('clearAllEffects');

// create user-defined sound effect
var id = $('#div1').jWebAudio('addEffect', {
    name: 'myEffect', 
    options: [{
        "type": jWebAudio.Filter.prototype.LOWPASS,
        "frequency": 1000.0
    }, {
        "type": jWebAudio.Filter.prototype.HIGHPASS,
        "frequency": 500.0
    }]
});
```

Standard Version

```javascript
// Add sound effect
// Returns id of effect
var id = sound.addEffect('telephonize');
// Delete with id
sound.deleteEffect(id);
// Delete all effects
sound.clearAllEffects();

// create user-defined sound effect
var id = sound.addEffect(new jWebAudio.Filter(
    'myEffect', 
    [{
        "type": jWebAudio.Filter.prototype.LOWPASS,
        "frequency": 1000.0
    }, {
        "type": jWebAudio.Filter.prototype.HIGHPASS,
        "frequency": 500.0
    }]
));
```

3D Sound Effect
---------------

jQuery version

```javascript
var id = $('#audio').jWebAudio('addEffect', '3d');
effect = $('#audio').jWebAudio('getEffect', id);
effect.node.setPosition(1, 0, 0);
```

Standard Version

```javascript
var id = source.sound.addEffect('3d');
effect = source.sound.getEffect(id);
effect.node.setPosition(1, 0, 0);
```

FFT Analysis
------------

jQuery version

(Not supported)

Standard Version

Set bin numbers:

```javascript
source.sound.analysize(128);
```

Get FFT data:

```javascript
source.sound.fftData
```

Example:

```javascript
function play() {
    source.load(function() {
        source.sound.analysize(128);
        source.sound.play();
        setInterval(function () {
            console.log(source.sound.fftData);
        }, 2000);
    });
}
```

[jquery]: http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js
[jqueryJWA]: https://github.com/01org/jWebAudio/blob/master/build/jquery.jWebAudio.js
[njqueryJWA]: https://github.com/01org/jWebAudio/blob/master/build/standard.jWebAudio.js
[examples]: https://github.com/01org/jWebAudio/blob/master/examples/index.html

