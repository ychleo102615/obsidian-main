---
tags: []
date: 2026-05-18
time: 16:50
---
## Multiple samples


## On/off sounds

## Playing with pitch
```js
import { Howl } from 'howler';
import { random } from 'lodash';
import './reset.css';
import './styles.css';

const button = document.querySelector('.btn');
const sound = new Howl({ src: ['sounds/pop.mp3'] });

button.addEventListener('click', (event) => {
  // Pick a random speed between 75% and 150% on every click:
  sound.rate(random(0.75, 1.5, true));
  sound.play();
```