# Web Audio API
![html5 webaudio](http://www.webmonkey.com/wp-content/uploads/2012/06/HTML5audio1.jpg)

---

## Basics

![input output](https://webaudio.github.io/web-audio-api/images/modular-routing1.png)

----

```js
const context = new AudioContext();
```

![recording studio](https://i.ytimg.com/vi/Q4StEidEyBs/maxresdefault.jpg)

---

## source (input)

![microphone](http://cdn.laboitenoiredumusicien.com/pub/produits/produits/shure/SSE-SM58-LCE-B.png)

----

### WebRTC

```js
navigator.getUserMedia({audio: true, video: false },
  (audioStream) => {
    // here comes audio stream handle
  }, (err) => {
    // here comes the error handle
  });
```

----

```js
const source = context.createMediaStreamSource(stream);
```

----

### Audio tag

![radio](https://www.imobie.com/support/img/ipod-2-ipod.png)

----

```html
<audio src="some-source.mp3"></audio>
```

```js
const audioTag = document.querySelector('audio');
const source = context.createMediaElementSource(audioTag);
```

----

### Oscillator

![Oscillator](http://www.electronicrepairguide.com/images/crystal%20oscillator.jpg)

----

```js
const oscillator = context.createOscillator();
oscillator.type = 'square';
oscillator.frequency.value = 3000; // value in hertz

```

---

## destination (output)

![speakers](http://i.kinja-img.com/gawker-media/image/upload/s--8Mg-aj7e--/184d1v4388rxfjpg.jpg)

----

### speakers

```js
context.destination
```

---

## input output mash-up
![input output](https://webaudio.github.io/web-audio-api/images/modular-routing1.png)

```js
const context = new AudioContext();
const audioTag = document.querySelector('audio');
const source = context.createMediaElementSource(audioTag);

source.connect(context.destination);
```

---

## effects

![effects](http://www.nomadfactory.com/products/magma/img/fullsize/rack_02.jpg)

----

### gain

![gain](https://mdn.mozillademos.org/files/5085/WebAudioGainNode.png)

```js
const gainNode = context.createGain();
gainNode.gain.value = 2;
```

---

## mash-up with effects

```js
const context = new AudioContext();
const audioTag = document.querySelector('audio');
const source = context.createMediaElementSource(audioTag);
const gainNode = context.createGain();

gainNode.gain.value = 2;
source.connect(gainNode);
gainNode.connect(context.destination);
```

---

## full scale studio

![full scale](https://www.w3.org/TR/webaudio/images/modular-routing2.png)

---

## analyzer

![histogram](http://cdn.arstechnica.net/wp-content/uploads/2012/05/recaptcha_histogram2-640x401.png)

----

![analyzer](https://mdn.mozillademos.org/files/12970/fttaudiodata_en.svg)

```js
const analyser = context.createAnalyser();
```

----

```js
analyser.getByteFrequencyData();
```

![](http://spek.cc/osx.png)

----

```js
analyser.getByteTimeDomainData();
```

![](http://courses.media.mit.edu/2011fall/mas630/11.projects/janice/MAS630/Couples_files/example_trend.jpg)

---

## putting it all together
