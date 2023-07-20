# AssertJ Test Exception

We can assert exceptions in different ways with AssertJ, but I find this to be the most complete and clear:

```java
assertThatExceptionOfType(MyException.class)
            .isThrownBy(() -> function())
            .withMessage("error message");
```