# Tools

## Groovy

Grooy is a jvm based script language. It can directly run java code. Plusing it's own syntax sugar, it becomes a great lab for java programming.

For writing a java programm, you must cope with various tools such as IDE, build file, jar, jvm. It's borning and hindering us to write small code snippet with java.

Here grooy comes to help. Personaly, I use grooy as a java without compile and build.

### Install

You can use great tool `sdk` to install and mantains groovy.

### Grab
All you need to know is the way to fetch dependecies of other library. Groovy make it simple, all you need to do is add following lines at the head of groovy file:

```groovy
@Grab("com.google.code.gson:gson:3.1.8")
```

Then you can import and using the library.

## Junit4

I am not sure which is best place for Junit4: tools or libraries.

But it is used so much and it deserves a place in tools.

###Basic Usage

Add @Test to each method you can test.
Add @Before and @After for fixture.
Add @BeforeClass and @AfterClass for one class fixture.

###Parameterized Usage
```java
import org.junit.runners.Parameterized.Parameters;
import org.junit.runners.Parameterized.Parameter;
import org.junit.experimental.runners.*;
```

#### Specify test data generator
Using @Parameters to specify a static method to generate test data.
If each instance only have one value, it can return Iterable<YouDateType>

otherwise it should return Collection<Object[]>

#### Receive test data instance.
Using @Parameter and @Parameter{1}, etc to denote variables to receive test data.

Then in test method you can access variable you marked with @Parameter.

You can also use constructor method to receive test data instance without @Parameter
