# Mindling 🥚

> A mind you raise from scratch.

Mindling is a tiny neural network you raise by talking to it. It starts as an egg full of noise, and as you feed it your words it slowly learns to speak — hatching into a creature shaped by what you taught it. Everything happens live in your browser, and nothing you type ever leaves your device.

**The catch: it's a real neural network.** Not a scripted pet wearing an AI costume. Every Mindling is an actual character-level net training on your words in real time, with backpropagation written from scratch — no TensorFlow, no PyTorch, no libraries at all. The babble in the speech bubble is genuinely what the model predicts, one letter at a time. You watch it climb from random static, to language-shaped gibberish, to — eventually — your own words echoed back.


## Try it

**Live:** https://happyfaceemoji.github.io/mindling 

Or just open `index.html` in any browser — that's the entire app. One file, no build step, no install.

## How to raise it

- **Feed** — give it your words. It trains on every character; the more you talk to it, the more it sounds like language, and then like you.
- **Rest** — let it sleep. It consolidates everything it's heard and wakes up sharper. Good for helping a young one find its voice.
- **Play** — loosen its tongue. Cranks up how adventurous its speech is, so it says stranger, more surprising things.

It hatches once it's learned enough (about a sentence or two of input). After that it keeps getting sharper the more you raise it, and it remembers you between visits.

## How it actually works

Under the cute box is a one-hidden-layer character-level neural network — a small MLP:

- **Vocabulary:** 33 characters (a–z, space, basic punctuation, newline).
- **Context:** the previous 3 characters, one-hot encoded (99 inputs).
- **Architecture:** 99 → 48 hidden units (tanh) → softmax over 33 characters. About 6,400 parameters.
- **Training:** stochastic gradient descent on cross-entropy loss, with backprop implemented by hand. *Feed* runs a few passes over your recent text; *Rest* runs many passes over everything — epochs, i.e. consolidation.
- **Speaking:** it samples characters one at a time from its own predictions. *Play* raises the softmax temperature — higher temperature means more surprising, less predictable speech.
- **"Understanding"** is just the training loss, inverted and rescaled. **"Sense of your language"** is the live character-frequency distribution it's picking up. Tap *show the machine* to see the raw loss and architecture.
- **Identity:** the creature's colour and form are derived from the statistical signature of your input, so two people grow visibly different creatures from the same starting egg.

Because the model is so small, it trains comfortably in real time — even on a phone. (It's also small enough to run on a ~$5 microcontroller, which is where this is headed. See the roadmap.)

## Design notes

A few choices that make Mindling what it is, rather than just another virtual pet:

- **It learns _you_, honestly.** It only ever trains on what you type. No hidden corpus, no cloud model, no canned responses.
- **It never fakes affection.** Its learning is purely self-supervised — it's never trained to please you or tell you what you want to hear. It's a creature finding its own voice, not a mirror optimised for your approval.
- **No dark patterns.** It can't be neglected to death, and it never guilts you into coming back. The relationship is the point, not a leash.
- **Private by default.** Your Mindling lives entirely in your browser's `localStorage`. Nothing you type is ever sent anywhere.

## Roadmap

This is an early, deliberately small version — built to find out whether raising a mind is actually fun before building more on top of it. Not yet here:

- **A natural lifespan.** Mindlings will eventually age and pass of old age — never from neglect — leaving a keepsake of the mind you grew.
- **More creature forms.** A small set of archetypes, each with parametric variation.
- **A "start a new one" reset.**
- **A physical device.** The same tiny net running on a microcontroller, in a little box on your desk.

## Tech

- A single file: `index.html`. Vanilla JavaScript, Canvas, zero dependencies, no build.
- The neural network, the pixel renderer, persistence, and the page are all inline.
- Fonts: [VT323](https://fonts.google.com/specimen/VT323) + [Silkscreen](https://fonts.google.com/specimen/Silkscreen).

---

Made by [happyfaceemoji](https://github.com/happyfaceemoji). An experiment in raising a mind. · ☕ [Ko-fi](https://ko-fi.com/happyfaceemoji)
