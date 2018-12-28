# java.util.stream.Stream
Stream là một class quan trọng của Java 8

### Vấn đề về intermediate operation và terminal operation
Stream có khá nhiều các operation và được chia làm hai loại là intermediate(địa trung hải) và terminal.
Khi bạn invoke(gọi) một intermediate operation thì nó sẽ ko được thực thi ngay lập tức (immediately)(lazy). nó sẽ đc gọi khi terminal operation đc gọi xong.
