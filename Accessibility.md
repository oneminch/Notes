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

<img src="/path/to/image.png" alt="..." />

<img src="/path/to/image.png" aria-labelledby="img-label" />

<p id="dino-label">Image Description...</p>
```


## Forms

## ARIA

## CSS Guide

- UI States
- Colors

## JavaScript Guide

## Screen Readers

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

- [brunopulis/awesome-a11y](https://github.com/brunopulis/awesome-a11y#readme)

- [Checklist - The A11Y Project](https://www.a11yproject.com/checklist/)