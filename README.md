# OCPJP_note
note when reading OCPJP document.
### Enum
* Enum ngầm khai báo public static final
* Enum ngầm kế thừa java.lang.Enum
* khai báo enum trong class thì Enum đó là static
* 2 enum constant cùng giá trị nhưng khác kiểu enum thì equals() trả về false
* enum không hỗ trợ clone

### Interface
* Interface không thể có instance trực tiếp
* Các Interface có thể được kế thừa
* Interface ko thể khai báo instance variable
* Interface có thể khai báo default, static, abtract method
* Có thể nest Interface
* Interface chỉ có thể public hoặc default
* Static method và default method trong interface có nội dung

### Functional interface
Là các interface chỉ khai báo 1 method abtracts duy nhất
```java
@FunctionalInterface
interface Runnable{
    void run();
}
```
Interface ko kế thừa từ Object nhưng ngầm khai báo một số method giống Object, vì vậy Comparator vẫn là functional interface
```java
@FunctionalInterface
public interface Comparator<T>{
    int compare(T o1, T o2);
    boolean equals(Object o);
}
```
### Lambda trong java
```java
@FunctionalInterface
public interface LambdaTest {
    abstract void call(int s);
}
int s = 10;
LambdaTest lamda = (int x) -> {
    System.out.println("Hello world "+x);
    s = 31;
    System.out.println("Hello world "+s);
};

lamda.call(20);
```
Lambda liên quan đến functional interface, cho phép override abtract method ??
* lambda function được xem như nested block, we cannot declare a variable with the same name as a local variable in the enclosing
block.





### Default method trong Interface
```java
public inteface Iterable<T>{
    Iterator<T> iterator();
    default void forEach(Consumer< ? super T> action){
        Objects.requireNonNull(action);
        for (T t : this) {
        action.accept(t);
        }
    }
    default Spliterator<T> spliterator() {
        return Spliterators.spliteratorUnknownSize(iterator(), 0);
    }
}
```
### Generic trong java
```java
public class Linklist<E>{

    @SuppressWarnings("unchecked")
    public Linklist(){}
    public LinkedList(Collection<? extends E> c) {
        this();
        addAll(c);
    }
    public boolean addAll(Collection<? extends E> c) {
        return addAll(size, c);
    }
    ...
}
```
Đoạn code trên vẫn đúng, Generic k đòi contruct phải có Generic

* SuppressWarnings("unchecked") để lúc compiler k bị lỗi sử dụng raw type
* Một số trick
```java
T mem = new T(); // wrong usage - compiler error
T[] amem = new T[100]; // wrong usage - compiler error
class X<T> {
    T instanceMem; // okay
    static T statMem; // wrong usage - compiler error
}

class GenericException<T> extends Throwable { } // wrong usage - compiler error
```
* Generic không nhận kiểu nguyên thủy

### Build in functions
Các build-in functions của java nằm trong java.util.function gồm
* Predicate
    ```java
    // check condition and return boolean. mostly in filter() of java.util.stream Stream
    boolean test(T t);
    eg
    Stream.of("hello", "world").filter(str->str.equals("world")).forEach(System.out::println);
    // print: world
    ```
* Consumer
    ```java
    @FunctionalInterface
    public interface Consumer<T> {
        void accept(T t); //the default andThen method elided
        default Consumer<T> andThen(Consumer<? super T> after) {
            Objects.requireNonNull(after);
            return (T t) -> { accept(t); after.accept(t); };
        }
    }
    Stream.of("hello", "world").forEach(s -> {System.out.println(s);});
    Stream.of("hello", "world").forEach(System.out::println);
    ```
    + Run function with argument and not return.
    + Ví dụ về endThen() method
    ```java
        Consumer<String> consumer1 = System.out::println;
        Consumer<String> consumer2 = System.out::println;
        Consumer<String> consumer3 = System.out::println;

        Stream.of("hello", "world").filter(TestLMD::isString).forEach(consumer1.andThen(consumer2).andThen(consumer3));
    ```
    + Có một kế thừa của Consumer là BiConsumer, tương tự nhưng châp nhận 2 param

* Function
    * Tương tự Consumer nhưng thay vì ko return, Function sẽ return giá trị
    ```java
    Arrays.stream("4, -9, 16".split(", "))
            .map(Integer::parseInt)
            .map(TestLMD::doidau)
            .forEach(System.out::println);

    static String doidau(Integer i){
         return String.valueOf((i < 0) ? -i : i);
    }
    ```
    * andThen() method tương tự Consumer, và có thêm compose()
    ```java
    Function<String, Integer> a1 = Integer::parseInt;
    Function<Integer, Integer> a2 = Math::abs;
    Function andthen = a1.andThen(a2);
    Function compose = a2.compose(a1);

    Arrays.stream("4, -9, 16".split(", "))
            .map(andthen)
            .forEach(System.out::println);
    ```


* Supplier


### Toán tử "Method reference"
 Như ví dụ ở functionalInterface Constumer
 ```java
Stream.of("hello", "world").forEach(System.out::println);
 ```
Toán tử ```:: ``` gọi là method reference, tham chiếu đến một static method và ngầm nhận đối số của lamda
Một ví dụ về ```::```
```java
public class TestLMD {
    public static void main(String []args) {
        Stream.of("hello", "world").filter(TestLMD::isString).forEach(s -> {System.out.println(s);});
    }

    public static boolean isString(String x){
        return x.equals("hello");
    }
}

```
### Vấn đề về Atomic class