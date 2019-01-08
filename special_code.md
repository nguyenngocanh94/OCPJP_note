## Some special code
### Integer caching
```java
Integer x = new Integer(123);
Integer y = new Integer(123);
System.out.println(x == y);    // false
Integer z = Integer.valueOf(123);
Integer k = Integer.valueOf(123); // same with above
System.out.println(z == k);   // true, vì valueOf đc lôi ra từ IntegerCache(range is -127,128)
```
### Stream operated upon or closed exeption
```java
IntStream temperatures = IntStream.of(-5, -6, -7, -5, 2, -8, -9);
        IntPredicate positiveTemperature = temp -> temp > 0; // #1
        if(temperatures.anyMatch(positiveTemperature)) { // #2
            int temp = temperatures
                    .filter(positiveTemperature)
                    .findAny()
                    .getAsInt(); // #3
            System.out.println(temp);
        }
// throw an IllegalStateException
```
cause by: A Stream should be operated on (invoking an intermediate or terminal stream operation) only once. A Stream implementation may throw IllegalStateException if it detects that the Stream is being reused.
=> chúng ta phải tạo mới stream mỗi lần muốn dùng terminal operation
```java

```
### Stream code
```java
 boolean result = Stream.of("do", "re", "mi3", "fa", "so3", "la", "ti")
                .filter(str -> str.length() >= 3) // #1
                .peek(System.out::println) // #2
                .map(String::toUpperCase)
                .peek(System.out::println) // #2
                .allMatch(str -> str.length() >1); // #3
System.out.println(result);
```
print log:
```log
mi3
MI3
so3
SO3
true
Process finished with exit code 0
```
* allMatch() trong stream return true if stream is empty