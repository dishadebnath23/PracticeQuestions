Practice Questions – Day 12  
Angular & React



============================================================
REACT
============================================================

1. Create UserProfile component  
Accept name, email, city as props  
Display them in a card

Approach:
- Create functional component
- Receive props
- Display using JSX

------------------------------------------------------------

Follow-up: Props vs State

Props:
- Read-only
- Passed from parent

State:
- Mutable
- Managed inside component

------------------------------------------------------------

Follow-up: Can props be modified?

No.

Props are immutable.

============================================================

2. Build a counter component  
Increment  
Decrement  
Reset

Approach:
- Use useState
- Update state on button clicks

------------------------------------------------------------

Follow-up: Why should state updates be immutable?

Reasons:
- Predictable behavior
- Proper re-rendering
- Performance optimization

------------------------------------------------------------

Follow-up: What happens if state is updated directly?

Problems:
- UI may not update
- React cannot detect change

============================================================

3. Use useEffect to  
Fetch data on component load  
Clean up timer on unmount

Approach:
- Use empty dependency array for load
- Return cleanup function for unmount

------------------------------------------------------------

Follow-up: Dependency array use cases

- Empty → runs once
- With values → runs on change
- No array → runs on every render

------------------------------------------------------------

Follow-up: How to avoid infinite loops?

- Use dependency array correctly
- Avoid updating state unnecessarily inside useEffect

============================================================

4. Render a list of products using map()  
Ensure proper keys

------------------------------------------------------------

Follow-up: Why keys are important?

Keys:
- Help React identify elements
- Improve performance
- Enable efficient re-rendering

------------------------------------------------------------

Follow-up: Why index should not be used as key?

Reasons:
- Causes UI bugs
- Incorrect re-rendering when list changes

============================================================

5. Create SearchBox and ProductList  
Search filters product list

Approach:
- Lift state to common parent
- Pass data and handlers as props

------------------------------------------------------------

Follow-up: What is lifting state up?

Lifting state up:
- Moving shared state to common parent
- Allows multiple components to sync

------------------------------------------------------------

Follow-up: Alternatives to lifting state?

Alternatives:
- Context API
- Redux
- Zustand

============================================================

6. Explain and implement useMemo and useCallback

useMemo:
- Memoizes computed values

useCallback:
- Memoizes functions

------------------------------------------------------------

Follow-up: Difference between useMemo and useCallback

useMemo:
- Caches value

useCallback:
- Caches function

------------------------------------------------------------

Follow-up: When should you NOT use them?

Avoid when:
- No performance issue
- Premature optimization

============================================================

7. Implement theme toggle using Context API

Approach:
- Create ThemeContext
- Provide theme value
- Consume using useContext

------------------------------------------------------------

Follow-up: Context API vs Redux

Context API:
- Simple state sharing
- Small to medium apps

Redux:
- Complex state management
- Large applications

------------------------------------------------------------

Follow-up: When is Context API not recommended?

Not recommended when:
- Frequent state updates
- Very large global state

============================================================

15. Create controlled login form  
Validate on submit  
Show error messages

Approach:
- Use useState
- Handle onChange
- Validate on submit

------------------------------------------------------------

Follow-up: Controlled vs Uncontrolled components

Controlled:
- React manages form state

Uncontrolled:
- DOM manages form state

------------------------------------------------------------

Follow-up: How form validation differs from Angular?

Angular:
- Built-in validation framework

React:
- Manual validation
- More flexibility

------------------------------------------------------------
