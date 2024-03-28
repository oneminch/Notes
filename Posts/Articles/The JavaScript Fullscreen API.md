---
id: js-fullscreen-api
title: The JavaScript Fullscreen API
description: A Simple Introduction to the JavaScript Fullscreen API
tags:
  - javascript
  - web-apis
image: /content/cover/js-fullscreen-api.png
cover_image: https://raw.githubusercontent.com/oneminch/portfolio/main/public/content/cover/js-fullscreen-api.png
canonical_url: https://minch.dev/blog/js-fullscreen-api
published_on: "2023-10-23"
---

Whenever you want to watch a YouTube video, play a video game or just want to do a focused work in your browser, the fullscreen feature makes the experience even more immersive. This article explains how this particular API works in JavaScript and how you can easily implement one in your projects.

## Introduction

The Fullscreen API allows an element on a page to be viewed in fullscreen. It makes it convenient for users to view web content in full pixel width and height. Aspects of the browser UI and OS, such as status bars, menu bars, as well as any applications on the device that take up screen space, are hidden. It accomplishes this by calling a method on an HTML tag that we want to view in fullscreen mode.

When viewing a video in a browser in fullscreen, it's a `<video>` tag that is actually in fullscreen mode. If the item we are viewing is an image, it's the tag that contains the image (usually the `<img>` tag) that is in fullscreen.

Basically, this API is a simple one to implement. However, it doesn't have one universal way of implementation. The methods used and events fired by the API may vary from browser to browser, especially in older versions of browsers. Inconsistencies as such, which are very common in the programming world, make this API a bit lengthy to write despite its simplicity.

For example, consider the following HTML code:

```html
<video id="intro" controls>
  <source src="intro.webm" type="video/webm" />
  <source src="intro.mp4" type="video/mp4" />
</video>
```

We can then simply call the method `requestFullscreen()` on the video element. The method is applied to an `Element` interface (and its child elements) to present it in fullscreen. This method can also be used to check whether fullscreen is available on this particular element. To exit fullscreen mode, the `exitFullscreen()` method is called on the `Document` interface. As in the case of the previous method, this method can also be used to check if it's supported on the document or in the browser.

```javascript
const el = document.querySelector("#intro");
if (el.requestFullscreen) {
    el.requestFullscreen();
}
...
if (document.exitFullscreen) {
    document.exitFullscreen();
}
```

The `Document` interface has built-in properties that can help us determine:

- If fullscreen mode is available/supported (`document.fullscreenEnabled`).
- Which element in the DOM is in fullscreen mode if fullscreen mode is active (`document.fullscreenElement`).

## Events

Two events are defined by the API:

- `document.onfullscreenerror` - fired on the `Document` whenever an error occurs when trying to enter or exit fullscreen mode.
- `document.onfullscreenchange` - fired whenever there is a change in fullscreen status on the entire `Document`, whether it's entering or exiting fullscreen, or switching tabs while in fullscreen mode.

```javascript
document.addEventListener("fullscreenerror", () => { ... });
...
document.addEventListener("fullscreenchange", () => { ... });
```

## CSS

We can further customize the element when it is in fullscreen mode using CSS. The `:fullscreen` CSS pseudo-class can be used to style an element that is currently in fullscreen mode. As with the case of many pseudo-selectors, we need to consider browser support with CSS, since it is not supported in [all browsers](https://caniuse.com/#feat=mdn-css_selectors_fullscreen).

```css
#intro:-webkit-full-screen {
  ...;
}
#intro:-moz-full-screen {
  ...;
}
#intro:-ms-fullscreen {
  ...;
}
#intro:fullscreen {
  ...;
}
```

## A Detailed Example

```javascript
function toggleFS() {
  /*  
    Checks if there is an element in
    fullscreen mode(including browser support)
  */
  if (
    !document.fullscreenElement &&
    !document.webkitFullscreenElement &&
    !document.mozFullScreenElement &&
    !document.msFullscreenElement
  ) {
    /*  
      Checks if fullscreen is available for the
      selected element and calls the method
      ('else if' blocks ensure browser support)
    */
    if (el.requestFullscreen) {
      el.requestFullscreen();
    } else if (el.webkitRequestFullscreen) {
      el.webkitRequestFullscreen();
    } else if (el.mozRequestFullScreen) {
      el.mozRequestFullScreen();
    } else if (el.msRequestFullscreen) {
      el.msRequestFullscreen();
    }
  } else {
    /*
      Exits fullscreen mode
      ('else if' blocks ensure browser support)
    */
    if (document.exitFullscreen) {
      document.exitFullscreen();
    } else if (document.webkitExitFullscreen) {
      document.webkitExitFullscreen();
    } else if (document.mozCancelFullScreen) {
      document.mozCancelFullScreen();
    } else if (document.msExitFullscreen) {
      document.msExitFullscreen();
    }
  }
}
const el = document.querySelector("#fs-btn");
el.addEventListener("click", toggleFS);
```

The fullscreen API is a very simple and handy tool for developers to apply to their web applications. It makes content more immersive, and help users with smaller screens to view content conveniently on their devices.

## Read More

- [Fullscreen API - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fullscreen_API)
