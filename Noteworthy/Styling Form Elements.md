- **Inheritance**: In some browsers, form elements don't inherit font styles by default. Expected behavior can be accomplished using:
```css
select,
button,
input,
textarea {
    font-family: inherit;
    font-size: 100%;
}
```

- **`box-sizing`**: Form elements use different `box-sizing` rules for different elements across browsers.
