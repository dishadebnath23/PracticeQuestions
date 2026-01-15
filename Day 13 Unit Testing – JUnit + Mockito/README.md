Practice Questions – Day 13  
Unit Testing – JUnit + Mockito

------------------------------------------------------------

1. Why do we need Mockito when we already have JUnit?

JUnit is used to:
- Write and run test cases
- Assert expected vs actual results

Mockito is used to:
- Mock dependencies
- Isolate the unit being tested
- Avoid calling real external components

JUnit tells us *whether* a test passes or fails,  
Mockito helps us control *how* dependencies behave.

------------------------------------------------------------

Follow-up: What happens if you don’t mock the repository layer?

If repository layer is not mocked:
- Test may hit the real database
- Tests become slow
- Test may fail due to DB or network issues
- Unit test turns into integration test

------------------------------------------------------------

Follow-up: Which layers should be mocked?

Generally mocked layers:
- Repository layer
- External API calls
- Third-party services

Not mocked:
- The class under test (service or controller)

============================================================

2. Explain @Mock and @InjectMocks. How do they work together?

@Mock:
- Creates a mock object
- No real implementation is called

@InjectMocks:
- Creates instance of the class under test
- Injects all mocked dependencies into it

Together:
- @Mock creates fake dependencies
- @InjectMocks injects them into service class

------------------------------------------------------------

Follow-up: What happens if @InjectMocks is missing?

If @InjectMocks is missing:
- Service object is not created properly
- Dependencies are null
- Test may throw NullPointerException

------------------------------------------------------------

Follow-up: How are mocks injected internally?

Mockito injects mocks using:
- Constructor injection (first priority)
- Setter injection
- Field injection

============================================================

3. How do you write a unit test for a service layer method?

Steps:
1. Mock dependencies using @Mock
2. Inject mocks using @InjectMocks
3. Define mock behavior using when–thenReturn
4. Call the service method
5. Assert the result
6. Verify interactions if needed

------------------------------------------------------------

Follow-up: Should service unit tests hit the database?

No.

Service unit tests should:
- Not hit database
- Mock repository layer
- Focus only on business logic

------------------------------------------------------------

Follow-up: What exactly should be asserted?

We should assert:
- Returned values
- State changes
- Thrown exceptions
- Important business outcomes

============================================================

4. How do you mock and verify method calls in Mockito?

Mocking:
- Use when().thenReturn() to define behavior

Verification:
- Use verify() to check method calls

------------------------------------------------------------

Follow-up: How do you verify that a method is never called?

Use:
- verify(mock, never()).methodName()

This ensures the method was not executed.

------------------------------------------------------------

Follow-up: How do you verify method arguments?

Mockito provides:
- Argument matchers like any(), eq()
- ArgumentCaptor for capturing arguments

============================================================

5. How do you test exception scenarios using JUnit + Mockito?

Exception scenarios are tested by:
- Mocking dependency to throw exception
- Asserting exception in test case

JUnit provides:
- assertThrows()

------------------------------------------------------------

Follow-up: How do you assert exception message?

Inside assertThrows:
- Capture the exception
- Assert exception.getMessage()

------------------------------------------------------------

Follow-up: How do you test try–catch blocks?

To test try–catch:
- Mock dependency to throw exception
- Call the method
- Assert returned value or behavior inside catch block

------------------------------------------------------------
