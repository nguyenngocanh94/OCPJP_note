# java.util.stream.Stream
Stream là một class quan trọng của Java 8

### Vấn đề về intermediate operation và terminal operation
Stream có khá nhiều các operation và được chia làm hai loại là intermediate(địa trung hải) và terminal.
Khi bạn invoke(gọi) một intermediate operation thì nó sẽ ko được thực thi ngay lập tức (immediately)(lazy). nó sẽ đc gọi khi terminal operation đc gọi xong.

Terminal Operations are:
```java
forEach
toArray
reduce
collect
min
max
count
anyMatch
allMatch
noneMatch
findFirst    
findAny
```
Intermediate Operations are:
```java
filter(Predicate<T>)
map(Function<T>)
flatmap(Function<T>)
sorted(Comparator<T>)
peek(Consumer<T>)
distinct()
limit(long n)
skip(long n)
```
The peek() method is useful for debugging: it helps us understand how the elements
are transformed in the pipeline.