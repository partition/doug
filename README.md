# doug
Inject your dagger dependencies without modules.
![alt text](http://www.rantlifestyle.com/wp-content/uploads/2014/12/7-Doug-Stamper.jpg)

Beware
=======
This stuff is in the PoC state.
Before you ever think about using it please check this page: https://google.github.io/dagger/testing.html

1. Likely that you don't have to use Dagger in your unit tests at all.
2. You shouldn't really mock stuff out in your instrumentation/end-to-end/functional/acceptance tests. Use fakes instead.


Motivation
======

Dagger2's authors advice to not use it for unit testing. While this is a pretty good advice, mocking Dagger2-driven injections makes sense in some particular cases, like Android Instrumentation Tests. Doug aims to remove the clutter code needed to mock your dependencies using Dagger.

And yeah, you can now mock stuff that's wired using the ```@Inject``` annotation rather than a ```@Provides``` method.

How to use it
==========

Simple as that.

```java
public class Greeter {
  @Inject
  Greeter() { }
}
```

```java

@Inject
Greeter greeter;

@Mock
Greeter greeterMock;

@Test
public void should_be_mocked() {
  DaggerComponent component = DaggerComponent.create();
  
  Doug.mock(component, greeterMock);

  component.inject(this);

  assertThat(greeter).isSameAs(greeterMock);
}
```
