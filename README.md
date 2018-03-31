# Kodg

Kodg is a generation framework which introduces some interesting features to Java Language.

## Examples

Kodg generates static code for types specification.

### Usage examples

Suppose that you have two classes: `com.a.A` and `com.b.B`, both of them have same methods and you want to access both using same interface:

`com.a.A`
```java
public class A {
    public void publish(File f) {
        ...
    }
}
```

`com.b.B`
```java
public class B {
    public void publish(File f) {
        ...
    }
}
```

Common interface:

`com.Publisher`
```java
public interface Publisher {
    void publish(File f);
}
```

In this context, you could simply invoke `Kodg.type(A.class).as(Publisher.class)` and you will have an instance of `Publisher` that invokes methods of `A`.

However, suppose that now you have a third class:

`com.c.C`
```java
public class C {
    public void publish(Path p) {
        ...
    }
}
```

If try to use `C` as `Publisher` by invoking `Kodg.type(C.class).as(Publisher.class)`, an exception will be raised: `KodgException("Method publish(File) of com.Publisher not found in type com.c.C")`.

To solve this, you need to provide an converter to Kodg: `Kodg.convert(File.class).to(Path.class).with(File::toPath).then().type(C.class).as(Publisher.class)`.

**Note: This is the first stub of project, everything may change and new things will be introduced**
