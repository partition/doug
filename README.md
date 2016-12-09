# doug
Inject your dagger dependencies without modules.

Motivation
======

Dagger2's authors advice to not use it for unit testing. While this is a pretty good advice, using Dagger2 makes sense in some particular cases, like Android Instrumentation Tests. Doug aims to remove the clutter code needed to mock your dependencies using Dagger. And yeah, you can now mock stuff that's wired using the ```@Inject``` annotation rather than a ```@Provides``` method.

How to use it
==========

Simple as that.

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
