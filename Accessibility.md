---
alias: A11y
---
> [!quote] MDN
> Web accessibility involves ensuring that content remains accessible, regardless of who and how the web is accessed.

- **Web Content Accessibility Guidelines (WCAG)** is a document published by the [[W3C]] that includes a technology-agnostic and international set of guidelines for accessibility conformance.
    - It is based on four main principles:
        - **Perceivable** - available to basic senses (either natively or thru assistive technologies (ATs))
        - **Operable** - interactable through any accessible means
        - **Understandable** - clear and unambiguous content
        - **Robust** - accessible by a wide range of user agents and ATs
- Different operating systems provide a set of special accessibility APIs that expose information useful for ATs.
    - Web browsers utilize these APIs to provide basic accessibility wherever semantic information (excluding styling information, and JavaScript) is used. 
    - Such information is structured into an *accessibility tree*.
    - We can further improve accessibility using features from the WAI-ARIA specification, which add semantic information to the accessibility tree.
- The accessibility tree is created based on the [[DOM]] tree that contains A11y-related information for most HTML elements.
    - Each object in an accessibility tree has four properties:
        - **name**
        - **description**
        - **role**
        - **state**
    - Moreover, the accessibility tree contains information on the types of actions that can be performed with an element.
    - The Accessibility Object Model (AOM) is an initiative (work-in-progress) that aims to create a JavaScript API (similar to the [[CSSOM]]) to allow developers to modify / explore the accessibility tree for an HTML page.
        - These APIs allow developers to provide information to assistive technologies (ATs), and help them better understand the information provided to ATs by browsers.
## HTML

- In addition to the many other benefits (such as [[SEO]]), semantic markup is a good basis for accessibility.
- Use the right element for the right job.
    - This helps take advantage of underlying browser / OS accessibility APIs.
        - e.g. Using a `<button>` instead of a `<div>` for an interaction has the default added benefit of navigation and activation using a keyboard.
- Content structure matters just as much as using the right element for the right purpose.
    - Use the right tag hierarchy, specially with headings.
    - Only have one `<h1>` per page.
- Use clear and unambiguous language.
    - Make sure to avoid using language, characters, abbreviations or acronyms that are likely to get mispronounced by screen readers. 
        - e.g. Write 4 to 8 instead of 4-8, Write February instead of Feb.
- Use the right techniques for content layout.
    - Don't use tables for content layout.
- Use labels that are contextual.
    - Avoid using labels such as "Click Here". Provide more context as these labels tend to be read out in isolation.
    - e.g. `<a href="/accessibility.html">Learn more about accessibility.</a>` ✅
- For media elements such as images, a descriptive alternative text should be provided.
    - If an `alt` text is not provided, screen readers will read out loud the image source URL. 
    - To avoid this for decorative images, 
        - an empty `alt` text should be provided, or
        - alternatively, a `role` attribute of `presentation` value should be specified to ensure screen readers skip reading out the alternative text.

```html
<img src="/path/to/image.png" alt="..." />

<img src="/path/to/image.png" alt="..." title="..." />

<img src="/path/to/image.png" aria-labelledby="img-label" />

<p id="dino-label">Image Description...</p>
```

- There is mixed reader support for implicitly associating a `<figcaption>`  to a `<figure>`. 
    - Using attributes, such as `aria-describedby`, creates this association.

```html
<figure>
  <img
    src="/path/to/image.png"
    alt="..." 
    aria-describedby="image-desc" />
  <figcaption id="image-desc">Image Description...</figcaption>
</figure>
```

- UI controls, such as buttons, links and form controls, can be manipulated using keyboards by default.
    - Even though it's possible to build keyboard accessibility into any element, it's not advised to do so. It's better to use the right element for the right job.
- When using hyperlinks, leave clear signposts in link text when linking to external and/or non-HTML resources.

```html
<a href="link-to-video-stream"> Watch video (opens in new tab) </a>

<a href="link-to-download-item" download="default-save-filename">
    Download report (PDF, 5MB)
</a>
```

- Skip links (or skipnav) should be implemented to bypass repetitive content, such as navigation options, and to link to the main content on the page.
- Space should be added between interactive content and UI controls that are place in close proximity to each other.
    - This helps people who suffer from fine motor control issues.
## CSS

- It's not recommended to change default styles so much that they no longer look or behave as expected.
    - Select sensible text styles, such as font sizes and line heights.
        - Text color should also contrast well with its background color.
            - A high contrast ratio helps anyone using a device with a glossy screen to better read content in a bright environment, such as sunlight.
    - Headings should stand out, and list should look like lists.
    - There are recognized styling conventions, such as a dotted underline in the case of `<abbr>`, that we shouldn't significantly deviate from.
    - Feedback is essential when interacting with UI controls.
        - Even if slightly changed to match creative/brand needs, default feedback mechanisms like UI state styles (focus, hover, active), and pointer cursors should still remain.
- Using `visibility: hidden` or `display: none` hides content from screen readers.
- Users might want to override styles with their own custom styles for a variety of reasons: 
    - to make text bigger, 
    - to increase the contrast ratio.
## JavaScript


## WAI-ARIA

- 
## Screen Readers

- 
## More

- AOM (Accessibility Object Model)
- Keyboard
## Tools

- [Sa11y](https://sa11y.netlify.app/)

---
## Further

### Books 📚

- [Accessibility for Everyone](https://app.thestorygraph.com/books/16d6fe85-ae9f-438c-ae5c-cd8a9bfb50cb)

- A Web for Everyone (Sarah Horton)

- Form Design Patterns (Adam Silver)

- Inclusive Components (Heydon Pickering)
### Learn 🧠

- [A11y - web.dev](https://web.dev/learn/accessibility/)

- [Deque University](https://dequeuniversity.com/)
### Podcasts 🎙

<iframe style='margin-bottom: .5rem; display: block; height: 170px; width: 100%; border: 1px solid #edae49; border-radius: .75rem; box-sizing: content-box' src='https://podverse.fm/embed/player?episodeId=aY5Uf5C8sqG' title='Podverse Embed Player' class='pv-embed-player'>JS Party - 10 A11y Mistakes to Avoid</iframe>

### Reads 📄

- [How to Create a "Skip to Content" Link | CSS-Tricks](https://css-tricks.com/how-to-create-a-skip-to-content-link/)

- [Inclusive Design & A11y (Smashing Newsletter)](https://mailchi.mp/smashingmagazine/420-inclusive-design-and-accessibility)
### Resources 🧩

- [A Complete Guide To Accessible Front-End Components (Smashing Magazine)](https://www.smashingmagazine.com/2021/03/complete-guide-accessible-front-end-components/)

- [brunopulis/awesome-a11y](https://github.com/brunopulis/awesome-a11y#readme)

- [Checklist - The A11Y Project](https://www.a11yproject.com/checklist/)