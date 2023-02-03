# String为什么是不可变的？

## String为什么是不可变的？
因为String类中有一个byte[ ]数组，这个byte[ ] 数组采用了final修饰，因为数组一旦创建长度不可变，并且被final修饰的引用一旦指向某个对象后，不可再指向其它对象，所以String是不可变的。

即 "abc" 无法变成 "abcd"

## StringBuilder / StringBuffer 为什么是可变的呢？

因为StringBuilder（非线程安全） / StringBuffer（线程安全） 内部实际上是一个byte[ ] 数组，这个byte [ ] 数组没有被final修饰，StringBuffer / StringBuilder 的初始化容量是16，当存满之后会进行扩容，底层调用了数组拷贝方法System.arraycopy( )，是这样扩容的。所以StringBuilder / StringBuffer 适合用于字符串频繁的拼接操作。

