---
alias: WPO
---

> [!quote] MDN
> Web performance refers to how quickly site content **loads** and **renders** in a web browser, and how well it responds to user interaction.
> 
> It is the objective measurement and perceived user experience of a website or application.

## Why

- Good web performance is important for accessibility, and correlates powerfully with the overall effectiveness of the website.
- Improving web performance by reducing download and render times of a site leads to better conversion rates and user retention.
- Building web apps with performance in mind is an integral part of the user experience.

## Optimization

- The major areas of performance optimization:
    - **Reducing overall load time**: correlates with latency, file size, number of files and other factors
        - Reducing file size and the number of HTTP requests, and utilizing preloading can be a good general strategy.
    - **Making sites usable as soon as possible**: involves prioritizing parts of the website so that users can interact with content quickly, and loading other assets in the background or when they are needed (lazy loading).
        - This aspect of performance is measured by the Time To Interactive (TII) metric.
    - **Smoothness & interactivity**: utilizing best practices to give smooth animations/transitions a smooth feel improves perceived performance.
    - **Perceived performance**: matters as much, or perhaps more than, any objective measurement.
        - Providing a quick response / feedback and regular status updates (e.g. via a loading animation) improves perceived performance.
        - Tips for improving perceived performance: 
            - Minimizing initial load
            - Reducing content reflows
            - Using progressive enhancement
            - Avoiding font file delays
        - Some metrics can be helpful indicators of perceived performance:
            - First paint
            - First Contentful Paint (FCP)
            - First Meaningful Paint (FMP)
            - Largest Contentful Paint (LCP)
            - Speed index
            - Time to interactive
    - **Performance measurements**: include both actual (objectively measured) and perceived (subjectively experienced) speeds.
        - Tools that can help measure and improve performance:
            - **PageSpeed Insights / WebPageTest** - websites for getting useful performance reports
            - **Network & Performance Monitor** (Firefox) - browser built-in tools 
            - **Performance API** - to build custom tools
## Multimedia

- For the average website, multimedia accounts for 75% of its bandwidth. 
- It's important to consider data usage, and device memory usage of users.
    - Downloaded images are stored in device memory.

### Images

- [[Lazy Loading]] images can greatly improve performance.
- Other strategies for optimizing images:
    - **Using an optimal format**
    - **Compression**
    - **Serving optimal sizes**
        - Serving lower resolution images for smaller screens and vice versa.
- Images added using `<img>` have a higher loading priority than ones using CSS `background-image`. So, it's important to use `<img>` / `<picture>` for content images.
    - Loading priority can also be controlled using the experimental `fetchPriority` attribute.
        - An example use case can be a carousel where the first image has higher priority than subsequent ones.
- As part of a good UX design, it's important to consider reflow / layout shifts when loading multimedia.
    - Setting the `width` and `height` attributes on an image can reserve space in the layout to avoid shifts when the image finally loads.
    - Once the image has loaded, the image's intrinsic aspect ratio is used, instead of the aspect ratio from the attributes. Even if the attribute dimensions are not accurate, the image is displayed in its correct aspect ratio.
- For `background-image` images, it's important to add a `background-color` value so if there is any overlaid content, it's still readable before the image has loaded.

### Video

- To better optimize video delivery:
    - Compress all videos.
    - Prioritize `<source>` order - from smallest to largest.
    - Ensure `loop`ing background videos have `autoplay` set.
        - Additionally, set `muted` for mobile and `playsinline` for Safari.
    - Remove audio for video that doesn't need audio (e.g. looping hero videos).
        - Audio consumes bandwidth. Remove it if it's not needed.
    - Control preloading using `preload`.
    - Consider streaming.
## Performance Optimizations

![Rendering Process](rendering.png)

### HTML

- Use `srcset` to provide different resolutions for images.
- Use `<picture>` to provide different sources for multimedia.
- Lazy load images: `loading="lazy"`.
- `<iframe>`s are expensive. Use them sparingly.
    - Utilize `loading="lazy"` similar to images.
- Preload high-priority resources using `<link>` with `rel="preload"`.

### CSS

- Remove unnecessary styles.
- Preload critical assets such as CSS files, fonts and media.
- Keep style modular to optimize for render blocking.
    - Split CSS into separate modules and use the `media` attribute to load only what is needed.

```html
<link rel="stylesheet" href="main.css" />

<link rel="stylesheet" href="print.css" media="print" />

<link rel="stylesheet" href="mobile.css" media="screen and (max-width: 480px)" />
```

- Minify and compress CSS files.
- Avoid writing super-specific and complex selectors.
- Utilize CSS sprites.
- Reduce unnecessary animations.
    - If needed, use CSS animations.
        - Performance can be further improved by animating on the GPU.
    - Avoid using properties that, when animated, trigger a reflow (and therefore a repaint).
- Pre-optimize element changes using the `will-change` CSS property.

#### Fonts

> [!important]
> A font is only loaded when it is applied to an element using `font-family`.

- Preload essential fonts.
    - Use `rel="preconnect"` to make an early connection to an external font provider.
- Load only the glyphs needed using the `unicode-range` `@font-face` descriptor.

### JavaScript

- Write less JavaScript. 
    - Consider not using a framework for fairly static experiences.
- Clean up unused code.
- Split code into modules and load each part on demand.
- Take advantage of built-in browser features.
    - e.g. Form validation
- Minify and compress files.
- For critical JS, use `<link>` with `rel="preload"` or `rel="modulepreload"` for modules to ensure JS is fetched without blocking rendering.

```html
<head>
  ...
  <link rel="preload" href="important-js.js" as="script" />
  <link rel="modulepreload" href="important-module.js" />
  ...
</head>

<!-- Can be includeded wherever in the page -->
<script src="important-js.js"></script>
```

- For non-critical JS, consider deferring its loading / execution using `async` and `defer`.
- For essential animations, use CSS over JS.
- To optimize event performance, remove event listeners that are no longer needed.
    - The less event listeners there are to keep track of, the better the performance.
- Minimize [[DOM]] manipulation.
    - For better performance, batch DOM changes together.
- Remove unnecessary elements from the UI (the DOM tree).
- Optimize loops.
- Take advantage of async JS, WebGPU and web workers to run code off the main thread.

## Core Web Vitals

- **Largest Contentful Paint (LCP)**
    - Measures the render time of the largest content element visible within the viewport.
    - This could be an image, video, text block, or any other element that takes up a significant portion of the screen.
    - A good LCP score is considered to be 2.5 seconds or less.

- **Cumulative Layout Shift (CLS)**
    - Analyzes the stability of the page layout and how much the content shifts unexpectedly during the page load.
    - Calculates the sum of all individual layout shift scores that occur during the entire page load.
    - A good CLS score is considered to be 0.1 or less

- **Interaction to Next Paint (INP)**
    - Measures the delay between a user's action (like a click or touch) and the browser's response. 
    - Introduced as a replacement for FID 
    - Google recommends an INP of 100 milliseconds or less.

### Other Metrics

- **First Input Delay (FID)**:
    - Measures the time it takes for a page to respond to the first user interaction, such as a click or tap.
    - Captures the delay between the user's action and the browser's response to that action.
    - A good FID score is considered to be 100 milliseconds or less.
- **Time to First Byte (TTFB)**:
    - Measures the time it takes for the browser to receive the first byte of the response from the server after making an HTTP request.
    - Provides an indication of the server's responsiveness and the efficiency of the backend infrastructure.
    - A lower TTFB value generally indicates better server performance.
- **First Contentful Paint (FCP)**:
    - Measures the time it takes for the browser to render the first piece of content from the DOM, such as text, image, or SVG.
    - Represents the point at which the user starts seeing content on the screen.
    - A good FCP score is typically considered to be within 1 to 2 seconds.
- **Speed Index**:
    - Calculates the average time at which visible parts of the page are displayed during the loading process.
    - Provides a single metric that represents the visual progression of page load.
    - A lower Speed Index value indicates faster rendering and better user perception of speed.
- **Time to Interactive (TTI)**:
    - Measures the time it takes for a page to become fully interactive and capable of responding to user input reliably.
    - Considers factors such as network activity, DOM changes, and event handlers.
    - A good TTI score means the page is ready for user interaction without delays or jankiness.
- **Total Blocking Time (TBT)**:
    - Measures the total amount of time that a page is blocked from responding to user input, such as clicks or scrolls.
    - Captures the duration between First Contentful Paint (FCP) and Time to Interactive (TTI).
    - A lower TBT value indicates a more responsive and usable page.
- **Page load time**:
    - Measures the total time it takes for a web page to load and display all its content, including images, scripts, and stylesheets.
    - Provides an overall indication of the page's loading performance.
    - A faster page load time generally leads to a better user experience.
- **Bounce rate**:
    - Indicates the percentage of visitors who leave a website after viewing only one page, without interacting further with the site.
    - A high bounce rate may suggest that users are not finding what they are looking for or are dissatisfied with the website's performance or content.

---

## Keep Learning

- CDNs
- Compression
- Caching
- [[CSS]] sprites
- Load balancing
- Pre-fetching / Preloading
- Lazy-loading images
- Code-splitting
- Core Web Vitals
- Critical Rendering Path

---
## Further

### Books 📚

- Designing for Performance (Lara Hogan)

- High Performance Web Sites (Steve Souders)

- Even Faster Web Sites (Steve Souders)

- Responsible JavaScript (Jeremy Wagner)

- Time Is Money (Tammy Everts)

### Learn 🧠

- [Developing for Web Performance (LinkedIn Learning)](https://www.linkedin.com/learning/developing-for-web-performance)
### Reads 📄

- [A Guide to Optimizing JavaScript Files](https://www.sitepoint.com/optimizing-javascript-files/)

- [Frontend Performance Best Practices](https://roadmap.sh/best-practices/frontend-performance)

- [Getting started with Web Performance 🚀 (HTMHell)](https://www.htmhell.dev/adventcalendar/2023/14/)

- [Psychology of Speed: A Guide to Perceived Performance](https://calibreapp.com/blog/perceived-performance)

- [Why does speed matter?](https://web.dev/why-speed-matters/)

### Resources 🧩

- [davidsonfellipe/awesome-wpo](https://github.com/davidsonfellipe/awesome-wpo#readme)

- [The Psychology of Web Performance](https://support.speedcurve.com/docs/psychology-of-web-performance)

#### Tools ⚙

- [PageSpeed Insights](https://pagespeed.web.dev/)

- [WebPageTest](https://www.webpagetest.org/)

### Videos 🎥

![Master Core Web Vitals in One Hour (YouTube)](https://www.youtube.com/watch?v=_ZCpE0AaXjM) 