# String
String là immutable in Java, một class immutable là class mà instance của nó k bị thay đổi.
### Các ví dụ về String 
```java
String value1 = "70";
String value2 = "70";
String value3 = new Integer(70).toString();
value1 == value2 // true;
value1 == value3 // false
value1.equals(value3) // true
value1 == value3.intern() // true (vì thực chất value 1,2,3 đều trở đến 1 address trong String pool)
```
