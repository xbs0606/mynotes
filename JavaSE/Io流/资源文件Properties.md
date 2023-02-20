# 1

## 使用流实现对properties文件的读写操作

```java
package com.qf.day10;

import java.io.*;
import java.util.Properties;

/**
 * @author zxq
 * @version V1.0
 * @Date 2023/2/17 14:49
 * @Description: ${描述}
 * 使用流实现对properties文件的读写操作
 */
public class PropertiesReadWrite {
    public static void main(String[] args) {
        System.out.println(propertiesRead("01"));
        System.out.println(propertiesRead("02"));
    }

    private static void propertiesWrite() {
        BufferedReader br = null;
        BufferedWriter bw = null;
        try {
            br = new BufferedReader(new InputStreamReader(System.in));
            bw = new BufferedWriter(new FileWriter("src/com/qf/day10/fileTest/2/config.properties"));
            Properties properties = new Properties();


            while (true) {
                System.out.println("请输入key值:（over结束）");
                String Key = br.readLine();

                if (Key.equals("over")) {
                    break;
                }

                System.out.println("请输入value值:");
                String value = br.readLine();

                properties.setProperty(Key, value);

            }
            properties.store(bw, "this is test");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {

            try {
                br.close();
                bw.close();
            } catch (IOException e) {
                e.printStackTrace();
            }

        }
    }

    private static String propertiesRead(String key){
        Properties properties = new Properties();

        try {
            properties.load(new FileInputStream("src/com/qf/day10/fileTest/2/config.properties"));
        } catch (IOException e) {
            System.out.println("加载不到文件"+e.getMessage());//getMessage方法就是简略描述错误，系统给你描述的。
        }

        return properties.getProperty(key);
    }
}

```

## 总结

> 总结Properties核心方法：
> 1.创建对象---》new Properties();
> 2.存储key和value键值对 ---》setProperty(key,value) 
> 3.创建Properties文件 ---》 store(字节或字符输出流对象，"文件内容注释")
> 4.读取Properties文件 ---》 load(字节或字符输入流对象)
> 5.获取value值 ---》 getProperty(key)
> 