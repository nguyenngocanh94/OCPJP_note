# java.io package
* Đoạn code 1, về System.in.read
```java
System.out.print("Type a character: ");
int val = 0;
try {
// sẽ trả về kiểu bytes (0->255)
// và nó cũng chỉ đọc được 1 char thôi
val = System.in.read();
} catch(IOException ioe) {
System.err.println("Cannot read input " + ioe);
System.exit(-1);
}
System.out.println("You typed: " + val);
```
* Đoạn code 2: set out stream cho System
```java
try{
            PrintStream ps = new PrintStream("log.txt");
            System.setOut(ps);
            System.out.println("Test output to System.out");
        } catch(Exception ee){
            ee.printStackTrace();
        }
```