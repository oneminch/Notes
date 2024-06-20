---
alias: Testing
---

## Learning Roadmap

- **Learning Links**
    - [Testing Fundamentals](https://web.dev/learn/testing) 
    - [React Testing](https://www.perplexity.ai/search/give-me-brief-4d6kGrfTQSi1GsYxYCGUKg) 
    - [E2E Testing with Cypress + React](https://www.youtube.com/watch?v=6BkcHAEWeTU) 
    - [E2E Testing with Playwright + TypeScript](https://www.youtube.com/watch?v=wawbt1cATsk)

- [[Node]] Testing
- Component Testing (React, Vue)
- E2E Testing (React, Vue)

## Bookmarks

- [How to test your apps (The Monthly Dev - YouTube)](https://www.youtube.com/live/CPS58ZK1m0s)

---
## Methodologies

### Test-Driven Development (TDD)

- The goal of TDD is code quality.

- **Advantages**
    - Clarified thinking / code design
    - Better communication between developers
    - Better structure / organization of production code

- **Disadvantages**
    - Takes longer initially
    - Bad tests create a fall sense of security

![Red -> Green -> Refactor](assets/images/tdd.red-green-refactor.png)
- Good tests should be:
    - ==R==eadable
    - ==I==solated - test run independent of one another
    - ==T==horough - cover all edge cases
    - ==E==xplicit

### BDD

## Type of Testing

### Unit Testing

- Test specific low level units of functionality - typically functions.
- More unit tests are written compared to other types.
### Integration Testing

- Ensure the individual pieces of the application work well together.
- More integration tests are written compared to E2E tests.
### End to End (E2E) Testing

- Ensure application works well from the user's perspective.
- Less E2E tests are written compared to other types.
## Tools

- 3 classes of testing tools
    - Testing environment / test runners
        - collect test & run test code
    - Test frameworks
        - define / organize individual tests
    - Assertion libraries
        - create testable claims

- Common testing tools fall into at least 2 of the above classes.

---
## Further
### Ecosystem 🏵

- Jest
- Vitest
- Mocha
- Chai
- QUnit
- Jasmine
- Cypress
- Enzyme
- Playwright
- Testing Library

### Learn

- [Complete Playwright Tutorial (LambdaTest) (YouTube)](https://www.youtube.com/watch?v=wawbt1cATsk)

- [Test-Driven Development (MOOC.fi)](https://tdd.mooc.fi/)

- [Learn Testing (web.dev)](https://web.dev/learn/testing)

### Podcasts 🎙

<iframe src='https://podverse.fm/embed/player?episodeId=cIJzdQmqnW1' title='Podverse Embed Player' class='pv-embed-player'>CodeNewbie - Why do I need to test my code? (Jonas Nicklas)</iframe>

<iframe src='https://podverse.fm/embed/player?episodeId=CIW8GYmDGM' title='Podverse Embed Player' class='pv-embed-player'>Syntax - How to Get Better at Debugging</iframe>

### Reads 📄

- [67 Weird Debugging Tricks Your Browser Doesn't Want You to Know (Alan Norbauer)](https://alan.norbauer.com/articles/browser-debugging-tricks)