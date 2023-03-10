# Optimizing Spring Contexts for JUnit and Mockito Tests

As I was trying to speed up our test suite, I made some interesting discoveries about how Spring's contexts are handled during testing.

Spring attempts to reuse contexts from the cache for efficiency, but there are scenarios where a cached context might not be suitable to be used for a test. For example when a tests defines a `@SpyBean` or `@MockBean` within the test class.  
These annotations add new beans to the context, requiring Spring to create a new one, which can be costly and should be avoided whenever possible.

To improve the situation, consider the following:
- Move the `@SpyBean` and `@MockBean` annotations to a superclass that's common to all tests. This will initialize the beans once and allow the context to be reused.
- Avoid using mocks entirely. While this can be more difficult, especially when dealing with external dependencies, it can greatly improve the timings and quality of integration tests.