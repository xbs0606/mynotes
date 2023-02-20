# io流(字符输入输出流)

> 字符输入输出流是专门用于对文本文件进行操作流，用于弥补字节流对文本文件操作时容易出现乱码的为题，所以用字符输入输出流对文本文件进行处理操作
>
## Reader字符输入流

> Reader是字符输入的父类，所有字符输入流都要直接或间接继承与Reader类，因为这个流是字符流，所以流中数据是char，要提供数组也是char类型数组
>
> 根据API文档中描述可以发现
> **public abstract class Reader extends Object implementsReadable, Closeable**
> 提供已知的之类
> BufferedReader, CharArrayReader, FilterReader,InputStreamReader, PipedReader, StringReader
>
> 操作文件FileReader这个类并不是Reader的直接子类，而是间接子类，操作文件FileReader类是继承与InputStreamReader这个类，InputStreamReader这个类是Reader直接之类，可以利用FileReader进行文件操作
>
## FileReader文件字符输入流

> FileReader是Reader的间接子类，FileReader的直接父类是InputStreamReader，InputStreamReader这个类提供文件编码集和缓冲区操作，API文档中也说明【此类的构造方法假定默认字符编码和默认字节缓冲区大小都是适当的】
> 通过流操作文本文件时，文本文件是存在编码集的，在使用FileReader类操作是使用就是默认编码集，这个默认编码集是根据系统进行获取，编码集的目的【提供文件的编码让文件可以达到统一性Unicode(UTF-8)】
> 在使用字节流时，API文档中是没有描述字节流具备缓冲区，但是在使用字符流的时，API文档提供缓冲区的概念，当使用流写出数据时，有一个方法flush方法，这个方法就是专门针对缓冲区进行设计，提供缓冲这个概念可以大大提高，流的使用效率
>
> 在API文档中提供FileReader中定义描述
> **public class FileReader extends InputStreamReader**
>
常用构造方法
| 构造方法                                                                                         |
| ------------------------------------------------------------------------------------------------ |
| FileReader(File file) 通过一个File对象(封装着文件路径)创建一个FileReader对象进行数据读取         |
| FileReader(String fileName) 通过一个String对象(封装着文件路径)创建一个FileReader对象进行数据读取 |

常用API方法
| 方法摘要 | 方法描述                                                                                               |
| -------- | ------------------------------------------------------------------------------------------------------ |
| void     | close() 关闭该流并释放与之关联的所有资源。                                                             |
| int      | read() 读取单个字符。                                                                                  |
| int      | read(char[] cbuf) 读取字符数组长度的内容。(常用)                                                       |
| int      | read(char[] cbuf, int off, int len) 将读取len的长度内容写入到cbuf数组中并且从off的位置开始在数组中写入 |

> PS:直接参考FileInputStream即可，只要将byte数组换char数组就可以了

Writer字符输出流

> Writer字符输入流是所有字符输入流父类，所有字符输入流都要直接或间接继承与Writer，因为这个流是字符流，所以流中数据是char类型，需要提供char类型数组
>
> 根据API文档中描述
> public abstract class Writer extends Object implementsAppendable, Closeable, Flushable
> 它是一个抽象类不能直接创建流对象进行操作，所以需要使用到其子类
> BufferedWriter, CharArrayWriter, FilterWriter,OutputStreamWriter, PipedWriter, PrintWriter,StringWriter
>
> 操作文件的FileWriter这个类不是Writer的直接子类，而是间接子类，但是FileWriter可以完成对文件写出操作
>
FileWriter文件字符输出流
> FileWriter是Writer的间接子类，FileWriter的直接父类是OutputStreamWriter，OutputStreamWriter个类提供文件编码集和缓冲区操作，API文档中也说明【此类的构造方法假定默认字符编码和默认字节缓冲区大小都是适当的】
> 通过流操作文本文件时，文本文件时存在编码集的，在使用FileWriter类操作时使用就是默认编码集，这个默认编码集是根据系统进行获取，编码集的目的【提供文件的编码让文件可以达到统一性Unicode(UTF-8)】
> 在使用字节流时，API文档中是没有描述字节流具备缓冲区，但是在使用字符流的时，API文档提供缓冲区的概念，当使用流写出数据时，有一个方法flush方法，这个方法就是专门针对缓冲区进行设计，提供缓冲这个概念可以大大提高，流的使用效率

常用构造方法
| 常用构造方法                                             |
| -------------------------------------------------------- |
| FileWriter(File file) 构建了一个文件对象FileWriter对象。 |
| FileWriter(File file, boolean append) 构建了一个文件对   |
| 象FileWriter对象。                                       |
| FileWriter(String fileName) 构造给定文件名的FileWriter对 |
| 象。                                                     |
| FileWriter(String fileName, boolean append) 构造         |
FileWriter对象给出一个文件名与一个布尔值，指示是否附加写入
的数据。|
> PS:构建方法中多了一个第二参数，是boolean参数值作用就是提供文件追加写入操作，当设置参数为true时，当前写入文件中数据操作就是追加写入【主要适合：记录日志的工作】，如果是连续写出数据，可以不开启这个操作

常用API
| 返回值 | 方法概述                                                                                                                                               |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| void   | close() 关闭此流，但要先刷新它。 关闭此流，但要先刷新它。                                                                                              |
| void   | flush() 刷新该流的缓冲。                                                                                                                               |
| void   | write(char[] cbuf) 写入字符数组。                                                                                                                      |
| void   | write(char[] cbuf, int off, int len) 从cbuf数组读取数据并写入到文件中,len是实际写出数据长度,off是从cbuf数组中什么位置开始写出 (使用字符数组时核心方法) |
| void   | write(int c) 写入单个字符。                                                                                                                            |
| void   | write(String str) 写入字符串(非常有用的核心方法)                                                                                                       |
> PS: 在写出数据到文件中时，只有字符流中会提供一个参数为String类型write方法，这个方法可以帮我们便捷将数据写出到文件中，这个方法及其重要FileWriter操作可以完全参考FileOutputStream这个类，基本上是一模一样，只不过将byte类型转换char类型即可
>
提供一个操作案例：使用字符输入输出流进行文本文件的拷贝操作

```java
public class FileCharCopy {
    public static void main(String[] args) {
        Reader reader = null;
        Writer writer = null;

        try {
            reader = new FileReader("src/com/qf/day09/IODemo/1/zls.jpeg");
            writer = new FileWriter("src/com/qf/day09/IODemo/2/zls.jpeg");

            char[] chars = new char[1024];
            int len;

            while ((len = reader.read(chars))!=-1){
                writer.write(chars,0,len);
            }

            writer.flush();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (Objects.nonNull(reader)){
                try {
                    reader.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (Objects.nonNull(writer)){
                try {
                    writer.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

字节流和字符流之间区别
> 字节流和字符流是有本质上区别：
> 1.流中数据是不同，字节流流中的数据是byte而字符流流中数据是char.
> 2 根据流中不同数据类型所以字节流主要处理是二进制文件【图片、音频、视频、压缩包的等等】也可以处理【文本文件】但是容易出现乱码，而字符流主要是处理文本文件提供流，它是无处理二进制文件的
> 3.字节流和字符流之间还有一个很大区别
> 字节流在操作流的过程中是【没有使用缓冲区】，直接对文件本身进行操作
> 字符流在操作流的过程中是【使用了缓冲区】，通过缓冲区进行进行对文件操作
> 什么是缓冲区？
> 缓冲区可以理解为一段特殊区域，某些情况下，如果一个程序频繁的操作一个资源（如文件或数据库），则会出现性能下降的问题，此时为了提升性能，就可以将内存中部分数据读取到一个内存区域中，以后直接从这个区域进行数据去读，这样化就可以提升系统的性能，那么这个提供区域就是“缓冲区”

```java
public class BufferedDemo {
public static void main(String[] args) throws
Exception {
/*
在同等条件下进行操作
创建文件字节输出流和文件字符输出流对象，将数据通过流写入到文
件中
创建了字节和字符文件输出流对象，进行数据书写到文件中并关闭了
流资源，此时外界文件中是可以存在数据
*/
/* OutputStream os = new FileOutputStream(new
File("desc/字节流文件.txt"));
os.write("Hello World".getBytes());
os.close();
Writer writer = new FileWriter(new File("desc/字符
流文件.txt"));
//自有字符流中提供可以将字符串写入到文件中方法
writer.write("Hello world");
writer.close();*/
//------------------------------------------------
-------------------------------------
/*
在同等条件下进行操作
创建文件字节输出流和文件字符输出流对象，将数据通过流写入到文
件中，但是不添加close方法
字节流可以将数据直接写出到磁盘文件中，在没有使用close方法前
提下程序正常结束也可以将流中数据写入到文件中
字符流在没有使用close方法的前提下，程序正常结束是没有办法将
数据写入到文件中的
就是因为 字符流使用 缓冲区技术即使用“缓冲区”
在字符流操作过程中，所有字符都是在“内存中形成”的，在输出前会
将“所有的暂时保存在内存中内容”输出到文件中
使用close这个方法在在关闭流资源自后会将缓冲区中数据输出文件
中，所以字符流就要更加要关闭流资源
但是为了防止忘记书写close方法，并且共缓冲区的利用率，Java对
所有输出流都提供了一个方法flush
flush这个方法可以强制的刷新出缓冲区中数据，所以就算没有关闭
流资源可以将字符流中数据写出到文件中
所以建议在所有写出数据操作中添加flush这个方法
*/
OutputStream os = new FileOutputStream(new
File("desc/字节流文件.txt"));
os.write("Hello World".getBytes());
Writer writer = new FileWriter(new File("desc/字符
流文件.txt"));
//自有字符流中提供可以将字符串写入到文件中方法
```

> 使用字符流还是使用字节流？
> 区分场景而言文本文件使用字符流，二进制文件使用字节流，但是字节流处理场景明显要比字符流多，所以建议优先使用字节流处理数据，如果数据是文本文件在考虑换流操作。
>