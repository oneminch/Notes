## Concepts

- WebRTC - https://www.youtube.com/watch?v=FExZvpVvYxA

## Standardization

- Web standards are the technologies used to build on the web. They exist as long technical documents called ==specifications==, and are created by standards bodies (which are institutions that invite groups of people from different tech companies to come together and agree on how the technologies should work in the best way). The [[W3C]] is the best known body. Others include:
    - **WHATWG**: maintain the living standards of [[HTML]].
    - **ECMA**: publish standard for ECMAScript, which [[JavaScript]] is based on.
    - **Khronos**: publish technologies for 3D graphics, such as WebGL.
- Due to the open nature of web standards, the web remains a freely-available public resource.
- Specifications detail exactly how a technology should work, and are intended for use by software engineers to implement the technologies (usually in web browsers).
    - e.g. HTML Living Standard describes how HTML (elements, and their APIs as well as surrounding technologies) should be implemented.

## Rendering

- **The Flow**
    - HTML document is parsed into a 'content tree'.
    - Using styling information, the 'render tree' is constructed.
        - This contains the nodes with their respective visual attributes, and in the order they will be displayed on the screen.
    - The render tree goes thru the 'layout' process.
        - Each node is given the exact coordinates where it should appear on the screen.
    - In the next step, the render tree is 'painted'.
        - Nodes will be traversed and each one will be painted to the UI.
- For improved UX, this process is done in small chunks of the document. Content is displayed on the screen as soon as possible.

## Roadmap

- **How Browsers Work**
    - **Engines**
    - **Rendering**
    - **Optimization**
- Evergreen Browsers
- Market share
    - Chrome
    - Firefox
    - Safari
    - IE
- Headless Browsers

## Engines

- Webkit
- Blink
- Gecko

## HTTP

- [[HTTP]]

## Internet

## Polyfills

## DevTools

- In the context of JavaScript debugging, a **_breakpoint_** is a point in code where the debugger will automatically pause the execution.
    - The `debugger;` command also pauses code execution when the developer tools are open.
    - An error also paused execution.


---
## Further
### Podcasts 🎙

<iframe style='margin-bottom: .5rem; display: block; height: 170px; width: 100%; border: 1px solid #edae49; border-radius: .75rem; box-sizing: content-box' src='https://podverse.fm/embed/player?episodeId=pRw8fREy9M_' title='Podverse Embed Player' class='pv-embed-player'>CodeNewbie - How do browsers work? (Lin Clark)</iframe>

### Reads 📄

- [How Browsers Work (web.dev)](https://web.dev/howbrowserswork/)

- [Populating the page: how browsers work (MDN)](https://developer.mozilla.org/en-US/docs/Web/Performance/How_browsers_work)

- [Understanding Role of Rendering Engines in Browsers (BrowserStack)](https://www.browserstack.com/guide/browser-rendering-engine)

- [vasanthk/how-web-works](https://github.com/vasanthk/how-web-works#readme)

### Resources 🧩

- [New to the Web Platform](https://web.dev/tags/new-to-the-web/)