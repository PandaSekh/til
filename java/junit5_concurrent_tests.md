# Running JUnit 5 Tests Concurrently

To reduce tests running times I tried to run them in parallel. I had a bit of success with Gradle, but I wanted to decide which test to run in parallel and which sequentially test-by.test. JUnit 5 offers a more fine-grained approach to running tests concurrently compared to Gradle.  
Here's how to enable concurrent execution for JUnit5 tests:

1. Enable Concurrent Execution
To enable concurrent execution of JUnit 5 tests, set the `junit.jupiter.execution.parallel.enabled property` to `true`.  
This can be done in the junit properties files or in the Gradle build script if you're running tests using Gradle. Here's an example of how to do it using Gradle:

```
test {
    useJUnitPlatform()
    systemProperty 'junit.jupiter.execution.parallel.enabled', 'true'
}
```

2. Add the `@Execution` Annotation
Next, you need to add the @Execution` annotation to each test class or superclass that should be run concurrently. This annotation takes an ExecutionMode parameter, which can be set to CONCURRENT to indicate that the tests should be run concurrently.

```
@Execution(ExecutionMode.CONCURRENT)
public class MyConcurrentTest {
    // test methods...
}
```

3. Use Resource Locks (Optional)
If you have tests that access a shared resource, such as a database, you may need to use resource locks to prevent concurrent access to that resource. To do this, you can use the @ResourceLock annotation, which allows you to specify the name of the resource and the access mode (read-only or read-write).

```
@ResourceLock(value = "DATABASE", mode = ResourceAccessMode.READ_WRITE)
public class MyConcurrentDatabaseTest {
    // test methods...
}
```