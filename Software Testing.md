---
alias: Testing
---

## Type of Testing

### Unit Testing

- Test specific low level units of functionality in isolation from other units.
    - Typically functions or classes.
- More unit tests are written compared to other types.

```jsx
import React from 'react';
import { render } from '@testing-library/react';
import MyComponent from './MyComponent';

test('renders the correct data', () => {
    const { getByText } = render(<MyComponent data="test data" />);
    expect(getByText('test data')).toBeInTheDocument();
});

test('renders the default data when no prop is provided', () => {
    const { getByText } = render(<MyComponent />);
    expect(getByText('Default Text')).toBeInTheDocument();
});
```

### Integration Testing

- Ensure the individual pieces of the application work well together.
- Focuses on catching flaws in interactions between integrated units or components.
- Strikes a balance between unit and end-to-end tests, providing confidence in how components work together.
- More integration tests are written compared to E2E tests.

```jsx
// ParentComponent.js
function ParentComponent({ data }) {
    return <ChildComponent data={data} />;
}

// ParentComponent.test.js
import React from 'react';
import { render } from '@testing-library/react';
import ParentComponent from './ParentComponent';

test('renders the correct data from the child component', () => {
    const { getByText } = render(<ParentComponent data="test data" />);
    expect(getByText('test data')).toBeInTheDocument();
});

test('renders the default data from the child component when no prop is provided', () => {
    const { getByText } = render(<ParentComponent />);
    expect(getByText('Default Child Data')).toBeInTheDocument();
});
```

### End to End (E2E) Testing

- Ensure application works well from the user's perspective.
- Ensures proper communication with other systems, interfaces, and databases.
- Takes more time and can be expensive in terms of efficiency, time, and money.
- Less E2E tests are written compared to other types.

```jsx
// App.jsx
function App() {
    const [count, setCount] = useState(0);
    
    return (<div>
        <h1>Counter App</h1>
        <p data-testid="count">Count: {count}</p>
        <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>);
}

export default App;
```

```js
// e2e.test.js
import { test, expect } from '@playwright/test';

test('counter increments when the button is clicked', async ({ page }) => {
    // Navigate to the app
    await page.goto('http://localhost:3000');
    
    // Check the initial count
    const countElement = page.locator('[data-testid="count"]');
    await expect(countElement).toHaveText('Count: 0');
    
    // Click the increment button
    await page.click('text=Increment');
    
    // Check if the count has been incremented
    await expect(countElement).toHaveText('Count: 1');
    
    // Click the increment button again
    await page.click('text=Increment');
    
    // Check if the count has been incremented again
    await expect(countElement).toHaveText('Count: 2');
});
```

### Mock Testing

- Involves creating simulated objects or functions to replace real dependencies in tests.
- Allows to test a specific piece of code without worrying about how other parts of the system work.
- Replaces real objects that code depends on with fake objects (called mocks) that simulate the behavior of the real ones.
    - These objects can be used to control what happens during the test. 
        - You can make them return specific values or behave in certain ways.
 
- Useful for:
    - Isolating components for true unit testing
    - Simulating API calls and responses
    - Testing different scenarios and edge cases

- **Stubs** are simple mocks that return pre-programmed responses.

```java
/* --- Code --- */
public interface Temperature {
    double getTemperature();
}

public class WeatherService {
    private Temperature t;

    public WeatherService(Temperature t) {
        this.t = t;
    }

    public String getWeatherDescription() {
        double t = t.getTemperature();
        if (t < 0) return "Freezing";
        if (t < 15) return "Cold";
        if (t < 25) return "Warm";
        return "Hot";
    }

    public boolean isTemperatureAboveThreshold(double threshold) {
        return t.getTemperature() > threshold;
    }
}

/* --- Test --- */
@Test
public void testWeatherDescription() {
    // Create a stub
    Temperature t = new Temperature() {
        @Override
        public double getTemperature() {
            return 20.0; // Always return 20 degrees
        }
    };

    WeatherService service = new WeatherService(t);
    assertEquals("Warm", service.getWeatherDescription());
}
```

- **Mocks** are more sophisticated than stubs, these can be programmed with expectations about how they should be called.

```java
@Test
public void testIsTemperatureAboveThresholdWithMock() {
    // Create a mock for Temperature
    Temperature mockTemp = mock(Temperature.class);
    
    // Set up the mock behavior
    when(mockTemp.getTemperature()).thenReturn(30.0);

    WeatherService service = new WeatherService(mockTemp);

    assertTrue(service.isTemperatureAboveThreshold(25.0));
    
    // Verify that getTemperature was called exactly once
    verify(mockTemp, times(1)).getTemperature();
}
```

## Tools

- 3 classes of testing tools
    - Testing environment / test runners
        - collect test & run test code
        - e.g. Jest, Vitest, Playwright
    - Test frameworks
        - define / organize individual tests.
        - e.g. Testing Library
    - Assertion libraries
        - create testable claims

- Common testing tools fall into at least 2 of the above classes.

## Patterns

> [!quote]- The Testing Pyramid
> ![The Testing Pyramid](assets/images/testing.testing-pyramid.png)
> **Source**: Google Testing Blog

> [!quote]- The Testing Trophy
> #### "Write tests. Not too many. Mostly integration."
> ![The Testing Trophy|350](assets/images/testing.testing-trophy.jpg)
> **Source**: Kent C. Dodds

### Test-Driven Development (TDD)

- The goal of TDD is code quality.

- **Advantages**
    - Clarified thinking / code design
    - Better communication between developers
    - Better structure / organization of production code
- **Disadvantages**
    - Takes longer initially
    - Bad tests create a fall sense of security

![Red -> Green -> Refactor](assets/images/testing.red-green-refactor.png)
- Good tests should be:
    - ==R==eadable
    - ==I==solated - test run independent of one another
    - ==T==horough - cover all edge cases
    - ==E==xplicit

### Arrange-Act-Assert (AAA)

- A structured approach to writing test cases that ensures clarity and separation of concerns.
- Widely used in unit testing and follows three distinct phases:
    - **Arrange**: Set up the necessary conditions and inputs for the test.
    - **Act**: Execute the functionality being tested.
    - **Assert**: Verify that the outcome is as expected.

```jsx
import { render, screen, fireEvent } from '@testing-library/react';
import Counter from './Counter';

test('increments counter on button click', () => {
    // Arrange
    render(<Counter />);
    
    // Act
    fireEvent.click(screen.getByText('Increment'));
    
    // Assert
    expect(screen.getByText('Counter: 1')).toBeInTheDocument();
});
```

---
## Skill Gap

- BDD
- Mock Tests
    - [Dependency Injection in JavaScript - YouTube](https://www.youtube.com/watch?v=yOC0e0NMZ-E)
    - [Mocking a Database in Node with Jest - YouTube](https://www.youtube.com/watch?v=IDjF6-s1hGk)
    - https://kentcdodds.com/blog/but-really-what-is-a-javascript-mock
    - [Testing Express REST API With Jest & Supertest - YouTube](https://www.youtube.com/watch?v=r5L1XRZaCR0)
- WebDriver protocol
- Smoke Tests
- Regression Tests
- Visual Tests
- API Testing

---
## Further
### Ecosystem 🌳

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

### Learn 🧠

- [Complete Playwright Tutorial (LambdaTest) (YouTube)](https://www.youtube.com/watch?v=wawbt1cATsk)

- [Test-Driven Development (MOOC.fi)](https://tdd.mooc.fi/)

- [Learn Testing (web.dev)](https://web.dev/learn/testing)

- [Rapid Testing with Vitest (VueSchool.io)](https://vueschool.io/courses/rapid-testing-with-vitest)

- [React Testing with Playwright (YouTube)](https://www.youtube.com/watch?v=3NW0Mz943_E)

- [React Testing: Components, Hooks, Custom Hooks, Redux and Zustand (YouTube)](https://www.youtube.com/watch?v=bvdHVxqjv80) ⭐

### Podcasts 🎙

<iframe src='https://podverse.fm/embed/player?episodeId=cIJzdQmqnW1' title='Podverse Embed Player' class='pv-embed-player'>CodeNewbie - Why do I need to test my code? (Jonas Nicklas)</iframe>

<iframe src='https://podverse.fm/embed/player?episodeId=CIW8GYmDGM' title='Podverse Embed Player' class='pv-embed-player'>Syntax - How to Get Better at Debugging</iframe>

### Reads 📄

- [Write tests. Not too many. Mostly integration. (Kent C. Dodds)](https://kentcdodds.com/blog/write-tests)

- [67 Weird Debugging Tricks Your Browser Doesn't Want You to Know (Alan Norbauer)](https://alan.norbauer.com/articles/browser-debugging-tricks)

- [The Cycles of TDD](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html)