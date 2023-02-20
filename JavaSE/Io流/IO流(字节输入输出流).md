# io流（字节书输出流）

## 介绍

> PS：IO很简单主要记忆的就是IO中进行文件读写操作
>
> Java中IO流的作用：IO流在Java中作用就是将内存中数据写入到磁盘进行存，程序运行时将磁盘中的数据读取到内存中进行处理
> 在Java中在没有学习到IO流之前，在程序中所有处理数据都是在内存中进行存储的【栈和堆】，在内存中存储的好处在于【执行效率高】坏处【数据无法持久存储】
> 内存中存储体现在于【DVD操作系统】：所有数据使用集合存储之后依旧是在内存中进行存储，每次执行程序时，都会在内存从新初始化集合中数据，这样就造成无论你如何修改集合中数据，只要程序重新运行数据使用保持原始状态。
> 所以需要将内存中数据保存到磁盘中进行持久保存【将内存中数据写成文件中内容进行保存操作】，如果**将内存中数据写到磁盘中，就需要使用到IO流【输出流】**，数据存存储在磁盘文件之后，程序运行时需要加载磁盘中文件数据【将磁盘文件中内容读取到内存中进行处理】，如果需要**将磁盘中文件内读取到内存中，就需要使用到IO流【输入流】**
>
什么是IO流？
> I ---》 顾名思义 ---》IN(读取、输入、读入) --》将磁盘中文件内容读取到内存中
> O---》 顾名思义 --》OUT(输出、写出、写入) ---》将内存中数据写入到磁盘文件中
> **IO流就是内存与磁盘【存储设备】之间数据传输通道**
> 硬盘----输入流---->内存
> 内存----输出流---->硬盘
> 在程序中所有的数据都是以流的方式进行传输与保存，程序需要数据时使用输入流读取数据，当程序需要保存数据时使用输出流保存数据
> 除了对数据保存之外，实际在网页中的文件上传与下载操作就是IO流完成
> PS：IO操作属于“长连接”，需要管理这个连接操作，如果不管理这个连接操作，会造成IO流操作会持续在内存中存在，会造成内存浪费，所以在**不使用IO操作下，一定要关闭IO流**

## java中常用的io流

> IO流其实就是建立起内存与硬盘【存设备】之间数据传输通道，通过这个通道可以将数据进行读取与写入操作，这个就是IO流本质
> 可以根据IO流进行简单的分类:
> 根据流的流向：
> 输入流： 把存储在磁盘中数据读取到内存中
> 输出流 : 把内存中数据写入到磁盘中
> 根据流中数据：
> 字节流： 无论是输入还是输出流中数据都是byte类型
> 字符流： 无论是输入还是输出流中数据都是char类型

## 字节输入输出流

> 这个流中数据类型就是byte，这个流既可以进行输入操作【读取】，也可以进行输出操作【写出】

### InputStream【字节输入流】

> InputStream流是所有字节输入流的父类，所有字节输入流都要直接或间接继承InputStream
> 这个流是一个抽象类不能直接创建对象，所以需要使用到这个流的子类来完成对字节输入流操作
>
> **public abstract class InputStream extends Objectimplements Closeable**
>
FileInputSteam【文件字节输入流】
> FileInputStream是InputStream字节入的子类，这个流主要提供是对文件读取操作，这个文件是泛指【指代的是：**所有文档二进制文件（文本文件、音频、视频、压缩包、图片等等）**】，都可以通过FileInputStream进行读取操作，**FileInputSteam是字节输入流所以流中数据是【byte类型】**
>
> 在API文档中提供创建定义
> **public class FileInputStream extends InputStream**
>
> PS：Java中提供原生流【系统API中定义好流】只能对文本文件中内容进行操作即【txt】文件，无法对Office文件记性操作，如果需要对这些文件进行操作需要导入【第三方jar包（别人封装好实现）】
>
> 构造方法
> FileInputStream(File file) 通过一个File对象创建FileInputStream字节输入流对象
> FileInputStream(String name) 通过一个String对象(文件的路径)创建FileInputStream字节输入流对象
> PS：这两个构造方法创建出对象方式是一样的，只是参数不一样，个人选取

核心Api方法
| 返回值类型 | 方法说明                                                                                                             |
| ---------- | -------------------------------------------------------------------------------------------------------------------- |
| int read() | 一次读取一个字节的数据                                                                                               |
| int        | read(byte[] bs) 一次读取参数字节数组长度的数据并存储在字节数组中【常用】                                             |
| int        | read(byte[] bs, int off, int len) 一次读取字节数组长度的数据,根据len读取实际内容长度,并从off位置开始入写到字节数组中 |
| void       | close() IO流式一个长连接,所以需要需要关闭流对象【常用】                                                              |

提供FileInputStreamAPI使用

```java
public class FlieInputStreamAPITest {
    public static void main(String[] args) {
//        1.创建对象【可以传两种参数1.file类型 2.String类型】
//        FileInputStream inputStream = new FileInputStream(new File("src/com/qf/day09/fileTest"));
//        FileInputStream fileInputStream = new FileInputStream("src/com/qf/day09/fileTest");

//        因为你传入得这个文件的路径可能是不存在的，因此有可能找不到文件，所以会有编译时异常Unhandled exception:java.io.FileNotFoundException
//        使用try-catch进行处理 ---> 特殊用途
//        throws处理 --》 开发通用

//        使用try-catch抛出异常
        FileInputStream fis= null;

        try {
            fis=new FileInputStream("src/com/qf/day09/fileTest/1.txt");

//            1.在编译时 调用read方法可能出现Unhandled exception: java.io.IOException->也要抛出
//            int read = fis.read();
//            System.out.println("一次只能读取一个字节"+(char) read);

            byte[] rd = new byte[20];
//            2.一次性读到数组中
//            fis.read(rd);
//            System.out.println(Arrays.toString(rd));//[101, 108, 108, 111, 32, 119, 111, 114, 108, 100, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
//
//            System.out.println(new String(rd));

            fis.read(rd,0,11);//off:从第几个字符开始读，len一次读多长
            System.out.println(new String(rd));//hello world


        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
//          因为无论有没有报错，finally都会执行，因此，我们可以利用这一特性，对创建的IO流进行资源的释放
            if (Objects.nonNull(fis)){
                try {
//                    在编译时会有一个Unhandled exception: java.io.IOException的异常
                    fis.close();//释放流，这是一个必做的操作
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }
        @Test
    public void Test01(){
            FileInputStream fis =null;

            try {
                fis =new FileInputStream("src/com/qf/day09/fileTest/2/4176.txt");

                byte[] bytes = new byte[1024];
                int len;

//                while (true){
//                    if (fis.read(bytes)==-1){
//                        break;
//                    }
//                    System.out.println(new String(bytes));
////                    会发现，已经将文件打印完了，后面还会有字符？
////                    因为如果读取的文件的大小没超过数组的长度，在读完后，会将数组后的空位输出出来
////                    如果读的数据超过了呢，会接着读并将文件覆盖，因此就导致了读完文件后剩下的数组空间残留的字节还会出来
//                }

//                解决办法
                while ((len= fis.read(bytes))!=-1){
                    /*
                    * 参数1，读到什么数组里
                    * 参数2，从什么地方卡开始读
                    * 参数2，读到哪不读了
                    * */
                    System.out.println("这次len的值"+len);
                    System.out.println(new String(bytes,0,len));
                }
            } catch (FileNotFoundException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            }finally {
                if (Objects.nonNull(fis)){
                    try {
                        fis.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            }

        }
}
```

> 当调用read方法读取文件中内容时，是按照bs数组的长度进行读取，然后写入到bs数组中，这是一次读取
> 下一次循环读取时，也会按照bs数组的长度进行读取，然后是覆盖写入到bs数组中，即不会清除原有数组中存的内容而是直接覆盖进新读取到文件内容到数组
> 例如：现在读取文件大小是 4063字节 存储数据数组的大小1024字节
> 第一次读取时 4063-1024 --》剩余字节 3039 但是读取到 1024字节内容
> 第二次读取时 3039-1024 --》剩余字节 2015 但是读取到 1024字节内容
> 第二次读取时 2015-1024 --》剩余字节 991 但是读取到 1024字节内容
> 第四次读取时 读取字节是991 并没有填充满1024 --》 实际读取991个字节
> 991个字节覆盖到byte数组中之后 会剩余33个字节没有进行覆盖内容
> 所以通过new String方式打印数组内容时，就会将33个没有覆盖内容数据打印出来
> read(byte[] bs)这个方法的返回值不仅可以返回读取到文件末尾-1值而且这个方法还可以返回读取到实际文件内容长度的实际值.

### OutputStream字节输出流

> OutputStream字节输出流是所有字节输出的父类，所有字节输入出流都是直接或间接继承OutputStream类
>
> 根据API文档中提供类创建方式
> public abstract class OutputStream extends Object implements Closeable, Flushable
>
> OutputStream是抽象类无法直接创建对象使用，所以需要提供子类来完成对流操作
> 根据现在操作数据原则，将数据从磁盘文件读取到内容，将内存中数据写出到磁盘文件中，始终要处理是File文件，所以**使用子类是FileOutputStream文件字节输出流**

FileOutputStream文件字节输出流

> FileOutputStream文件字节输出流类是OutputStream的子类，这个类主要用用于将内存中存储数据写入到磁盘文件中进行保存操作，这里的文件是泛指【指代是二进制文件（文本文件、音频、视频、图片、压缩包等等）】都可以使用FileOutputStream这个流对象将数据写入到磁盘中
>
> 根据API文档中说明
> public class FileOutputStream extends OutputStream

核心构造方法
| 构造方法                                                                                                                                                                          |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| FileOutputStream(File file) 通过一个File对象(封装的文件路径)创建文件字节输出流对象                                                                                                |
| FileOutputStream(File file, boolean append)通过一个File对象(封装的文件路径)创建文件字节输出流对象,并根据第二个参数的值决定是否是对文件进行追加写入数据 true是追加 false 不追加    |
| FileOutputStream(String name) 通过一个String对象(封装的文件路径)创建文件字节输出流对象                                                                                            |
| FileOutputStream(String name, boolean append)通过一个String对象(封装的文件路径)创建文件字节输出流对象,并根据第二个参数的值决定是否是对文件进行追加写入数据 true是追加 false不追加 |

API核心

| 返回值 | 方法                                                                                                                                       |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| void   | close() 关闭此文件输出流并释放与此流有关的所有系统资源 【常用】                                                                            |
| void   | write(byte[] b) 将以字节数组长度的内容写入到磁盘文件中                                                                                     |
| void   | write(byte[] b, int off, int len) 将实际len长度的内容从数组b中off位置开始写入到磁盘文件中【常用】                                          |
| void   | write(int b) 一次写一个字节的内容写入到磁盘文件中flush() 加快流的流速,强制清空缓冲区中数据【加快输出效果（在使用网络流的时候一定要添加）】 |

FileOutputStream常用API操做

```java
    @Test
    public void Test01() {
//        实例化与FileInputStream同理

        FileOutputStream fos = null;

        try {
            fos = new FileOutputStream("src/com/qf/day09/fileTest/2/3.txt");
//            1.想路径文件写一个字符
            fos.write('a');
            fos.write('b');
//            并不是运行一次就向文件写一次，二十会覆盖之前的内容（会将人家原本的东西清掉）
//            2.一次性写一串
            fos.write("BLACKPINK".getBytes());
//            3.从字节数组中将内容写入到文件中，从off参数提供的位 置读取数据开始写，写len提供长度内容
            /*
            第一个参数是存储数据字节数组
            第二个参数是从字节数组什么位置开始读取和写出数据【默认0（下标）】
            第三个参数实际写出内容长度（一般会配合输入流中read方法获取实际长度进行写出）
            */
            fos.write("BLACKPINK".getBytes(),5,"PINK".length());
            //刷新
            fos.flush();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (fos!=null){
                try {
                    fos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
```

## io流完成图片的拷贝操作

```java
    public static void main(String[] args) {
//        1.创建字节输入输出流的实例化对象
        FileInputStream fis =null;
        FileOutputStream fos =null;

        try {
            fis =new FileInputStream("src/com/qf/day09/IODemo/1/zls.jpeg");
            fos = new FileOutputStream("src/com/qf/day09/IODemo/2/zls.jpeg");

            byte[] bytes = new byte[1024];
            int len;

            while ((len=fis.read(bytes))!=-1){
                fos.write(bytes,0,len);
            }

            fos.flush();
            System.out.println("copy over");

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally{
//            关闭io流，本着先开先关的原则
            if (Objects.nonNull(fis)){
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (Objects.nonNull(fos)){
                try {
                    fos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
```

## 总结

>总结:字节输入输出流在文件进行操作，因为字节流中使用数据类型byte类型主要针对是二进制的文件，所以**字节流主要对的是【图片、音频、视频、压缩包】这类的二进制文件**，在读取和写出文本文件时，会在处理文件时出现一些乱码问题�，所以字节流主要是处理二进制文件而使用，如果处理文件文件的数据就不太建议使用字节流来完成操作，就是因为容易出现乱码问题