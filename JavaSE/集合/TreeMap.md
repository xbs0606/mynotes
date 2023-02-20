# TreeMap

> TreeMap集合是Map集合实现类之一，TreeMap集合提供排序操作，TreeMap集合排序操作和TreeSet道理相同的，需要提供Comparator和Comaprable接口，根据使用TreeMap中构造方法决定说那个那个接口来实现排序操作
>> 在官方的API文档中的介绍：基于红黑树（Red-Black tree）的NavigableMap 实现。该映射根据其键的自然顺序进行排序，或者根据创建映射时提供的 Comparator 进行排序，具体取决于使用的构造方法.
>
> TreeMap集合的排序点在于存储的键值key，将要排序数据存储到key中就可以进行排序操作
> 当调用无参构造方法创建TreeMap对象时，使用Comparable进行的比较操作
> TreeMap() 使用键的自然顺序构造一个新的、空的树映射。
> 当调用有参构造方法创建TreeMap对象时，使用Comparator进行的比较操作
>> TreeMap(Comparator comparator) 构造一个新的、空的树映射，该映射根据给定比较器进行排序。

## 定义

```java
public class TreeMapDemo {
    public static void main(String[] args) {
        TreeMap<Integer, String> treeMap = new TreeMap<>();

        treeMap.putIfAbsent(1,"01");
        treeMap.putIfAbsent(24,"01");
        treeMap.putIfAbsent(41,"01");
        treeMap.putIfAbsent(454,"35");
        treeMap.putIfAbsent(3,"01");
        System.out.println(treeMap);

        TreeMap<Integer, String> treeMap1 = new TreeMap<>(new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
//                return o2-o1;//降序排序
                return o1-o2;//升序排序
            }
        });

        treeMap1.putIfAbsent(1,"01");
        treeMap1.putIfAbsent(24,"01");
        treeMap1.putIfAbsent(41,"01");
        treeMap1.putIfAbsent(454,"35");
        treeMap1.putIfAbsent(3,"01");
        treeMap1.putIfAbsent(10,"01");
        treeMap1.putIfAbsent(23,"01");
        treeMap1.putIfAbsent(45,"01");

        treeMap1.forEach(new BiConsumer<Integer, String>() {
            @Override
            public void accept(Integer integer, String s) {
                System.out.println(integer+"+"+s);
            }
        });
    }
}

```

> TreeMap集合排序的时候也是会对key值进行排重操作，这个排重操作依据是提供Comparable和Comparator接口中方法实现时，如果结果为0，就会进行排重操作

## Collections工具类

> Collections工具类类似于Arrays工具类，Collections工具类是为了给Collection集合提供便捷操作工具类，虽然Collection集合已经提供很多方法了，但是Collections工具类也提供一些操作方法，弥补开发时所需要自行定义方法
> Collections工具类提供方法大部分都是给Collection集合使用，极少部分是给Map集合使用

```java
    public static void main(String[] args) {
        ArrayList<Integer> arrayList = new ArrayList<>();

//       1. 批量添加元素
        Collections.addAll(arrayList,1,2,3,4,5,6,10,20,45,0,12);

//       2.排序，针对list
        Collections.sort(arrayList);//默认升序
//            自定义排序1.实现comparable 2.实现comparator
        Collections.sort(arrayList,Collections.reverseOrder());
        Collections.sort(arrayList, new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o1-o2;
            }
        });
//        但是从java8开始list结合接口提提供sort方法，所以可以直接调用list.sort方法进行排序

//        3.将list，map，set集合转成线程安全的集合
        List<Integer> list = Collections.synchronizedList(new ArrayList<Integer>());
        Set<Integer> set = Collections.synchronizedSet(new HashSet<Integer>());
        Map<Integer, String> map = Collections.synchronizedMap(new HashMap<Integer, String>());

//        4. 使用二分法查找【要提前排序数组】，找到->下标;找不到->负数
        System.out.println(Collections.binarySearch(arrayList, 1));

//        5.交换list储存元素的位置，位置参数是下标
//        形参1是需要交换的列表，形参二是要交换的下标，形参三是另一个要交换的下标
        Collections.swap(arrayList,0,2);
//        [0, 1, 2, 3, 4, 5, 6, 10, 12, 20, 45]
//        [2, 1, 0, 3, 4, 5, 6, 10, 12, 20, 45]

//        6.打乱顺序
        Collections.shuffle(arrayList);

//        7.填满集合 注意这里的集合要有值，不然是替换不了的
        Collections.fill(arrayList,1);
    }
```

## Collection集合和Map集合的总结

> Collection是Java集合框架中根接口也是List和Set集合的父接口，Collection集合接口也继承Iterable接口所有Collection系的集合都支持迭代器进行遍历操作，在**Collection集合接口中常用的就是List和Set接口**，List和Set接口中常用的实现类集合**ArrayList【允许存储重复数据并且使用数组实现】**和**HashSet【不允许存储重复数据并且使用Hash表实现】**
> Map集合本身没是不在Collection范围内容，它是一个独立的集合，Map提供一种【键值对】即key-value的形式进行数据存储操作，在存储数据时要求key值必须是唯一的，value值可以不唯一，在**Map集合接口中主要使用实现类是HashMap**
> PS：List集合使用**ArrayList** 、Set集合使用**HashSet**、Map集合使用**HashMap**
>