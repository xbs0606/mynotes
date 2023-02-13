# TreeSet

> TreeSet是Set集合接口实现类之一，它是一个特殊集合【这个集合不仅可以排重而且可以对存储到集合中的数据提供升序排序】，在以往开发中可以利用TreeSet这个特性对需要排序数据进行操作.
> 从Java8开始List集合专门提供方法sort方法，List集合也可以调用集合提供Sort方法进行对数据排序操作，但是不能排重，所以学习TreeSet的目的为类接触可以排序接口
>
> 在API文档中有说明：基于 TreeMap 的 NavigableSet 实现。使用元素的自然顺序Comparable 对元素进行排序，或者根据创建 set 时提供的 自定义排序Comparator 进行排序，具体取决于使用的构造方法。
> Set集合系列主要实现都是依赖于Map集合，HashSet底层实现是HashMap，TreeSet底层实现是TreeMap，在Java8之前TreeSet底层实现的结构【二叉树+Hash表】，从Java8开始之后将底层实现的结构【红黑树+Hash表】
>
TreeSet中的使用API可以完全参考Set集合即可，其余API文档中提供方法自行查看

```java
public class TreeSetDemo {
    public static void main(String[] args) {
//向TreeSet中存储系统提供数据类型
        TreeSet<Integer> set = new TreeSet<>();
        set.add(100);
        set.add(20);
        set.add(17);
        set.add(1);
        set.add(6);
        set.add(88);
        set.add(66);
        set.add(33);
        set.add(77);
        set.add(1);
//存储数据中提供两个1进行存储 ---》 自动排重和排序操作【默认是升序】
        System.out.println(set);
    }
}
```

> [1, 6, 17, 20, 33, 66, 77, 88, 100]

## comparable接口-自然排序接口

> 官方文档说明:此接口**强行对实现它的每个类的对象进行整体排序。这种排序被称为类的自然排序，类的 compareTo 方法被称为它的自然比较方法,【间接的说明Comparable接口是一个自然排序接口，对与实现接口类会提供排序操作，这个排序操作需要完成compareTo这个方法**
> **当前调用TreeSet集合的无参构造方法时，就要求向TreeSet中存储的数据必须实现Comparbale实现Comparbale接口就需要实现接口中给提供方法**

实现comparable接口就需要实现接口中的方法

int compareTo（T o）比较此对象与指定对象的顺序
> compareTo这个方法使用接口上泛型作为方法参数泛型，所以在实现Comparable的时候需要指定接口中泛型是什么类型，这样可以避免不必要向下转型，泛型T如何赋值，Comparbale提供谁进行比较这个类型就是谁
> Comparable提供compareTo方法对数据进行比较时遵守的原则 比较此对象与指定对象的顺序。如果该对象小于、等于或大于指定对象，则分别返回负整数、零或正整数。
> compareTo这个方法的返回值类型时int类型，这个方法返回值是一个数字
>
> ps:compareTo这个方法不建议理解为比较方法，理解为交换方法即通过这个方法的得到返回值决定如何进行数据交换【存储】
> 之前有接触过一些排序的操作，例如冒泡、选择这些手写排序，但是这些排序中都会有一个必要的操作

深入理解

> "CompareTo这方法会返回三个值 正整数、 负整数 和 0"
>
> 一般来说自定义类中提供比较属性基本上都是系统类型，就可以通过两个数据之间记性“差值计算”从而得到 正整数、 负整数 和 0
> Student类为例 需要比较是年龄 --》年龄的属性是 int类型
> 用两个int类型进行相减 得到结果就是 正整数、 负整数 和 0 正好满足了CompareTo方法需求
> 谁减谁可以得到什么结果，如果不是基本数据类型时引用类型减也不能计算？
> 不用担心引用类型问题，基本上能用来比较的引用类型都实现Comparable，所以比较引用类型调用这个引用类型中对应CompareTo方法就可以
> "需要区分当前对象和传入对象"
> "调用CompareTo方法的就是当前对象使用【this表示】"
> "对CmpareTo方法参数赋值的就是传入对象使用【other表示】"
>
> "由此就可以得到一个万能公式：
> "当前对象 - 传入对象 【得到排序结果就是升序】" ---》 正整数
> "传入对象 - 当前对象 【得到排序结果就是降序】" ---》 负整数
> "切记：TreeSet的排重机制并不是equals和HashCode，而是实现排序
> 接口中CompareTo或Compare方法的返回值，只要返回值为0，TreeSet就会认为是同一个对象，进行排重操作"
> 当前使用万能公式做计算时，如果遇到得到0时，出现排重效果，建议在得到0时在提供一个排序条件操作，或者使用List中sort方法排序修改Student类进行年龄属性排序操作使用这个公式进行排序时会面临到问题：
> 问题1：此时排序数据类型时自定义类Student
> 我们是不能使用 Student - Student 也不可能Student.CompareTo(Student)
> 对自定义对象排序时，排序时*自定义对象的属性*，将当前公式变形为"当前对象.属性 - 传入对象.属性 【得到排序结果就是升序】" ---》正整数
> "传入对象.属性 - 当前对象.属性 【得到排序结果就是降序】" ---》负整数
> 问题2：此时排序数据类型时系统类型Integer
> "当前对象 - 传入对象 【得到排序结果就是升序】" ---》 正整数
> "传入对象 - 当前对象 【得到排序结果就是降序】" ---》 负整数
> 问题3: 如果遇到是引用类型无法使用减号进行计算时
> "当前对象.compareTo(传入对象) 【得到排序结果就是升序】" ---》正整数
> "传入对象.compareTo(当前对象) 【得到排序结果就是降序】" ---》负整数

## Comparator接口【自定义排序接口】（重点掌握【重要】）

> 除了TreeSet集合中可以使用Comparable接口进行自然排序之外，还有一个更加灵活方便的接口Comparator，在系统API文档中说明：强行对某个对象 collection 进行整体排序 的比较函数。可以将Comparator 传递给 sort 方法（如 Collections.sort 或Arrays.sort），从而允许在排序顺序上实现精确控制。还可以使用Comparator 来控制某些数据结构（如有序 set或有序映射 ）的顺序，或者为那些没有自然顺序 的对象 collection 提供排序。
> **综上所述：Comparator接口不仅可以对TreeSet提供排序操作，而且
可以针对Java系统API提供sort方法进行自定义排序操作**

Comparator接口中的核心比较方法：

int  compare(T o1 , T o2)比较用来排序的两个参数

> compare这个方法和Comparable接口中compareTo方法是一个道理也是返回 正整数、负整数和0 代表对象 大于 小于和等于
> 刚刚在Comparable中提供万能公式可以直接使用在Comparator
>
> "这里是需要注意的是：
> "Comparator接口中compare方法有两个参数,两个参数谁是当前对象，谁是传入对象"
> "compare方法中第一个参数 即 o1 就是当前对象即this"
> "compare方法中第二个参数 即 o2 就是传入对象即other"
> "由此就可以得到一个万能公式：
> "当前对象 - 传入对象 【得到排序结果就是升序】" ---》 正整数
> "传入对象 - 当前对象 【得到排序结果就是降序】" ---》 负整数
> "切记：TreeSet的排重机制并不是equals和HashCode，而是实现排序接口中CompareTo或Compare方法的返回值，只要返回值为0，TreeSet就会认为是同一个对象，进行排重操作"
> 当前使用功能公式做计算时，如果遇到得到0时，出现排重效果，建议在得到0时在提供一个排序条件操作，或者算着List中sort方法排序使用这个公式进行排序时会面临到问题：
> 问题1：此时排序数据类型时自定义类Student我们是不能使用 Student - Student 也不可能Student.CompareTo(Student)对自定义对象排序时，排序时自定义对象的属性，将当前公式变形为：
> "当前对象.属性 - 传入对象.属性 【得到排序结果就是升序】" ---》正整数
> "传入对象.属性 - 当前对象.属性 【得到排序结果就是降序】" ---》负整数
> 问题2：此时排序数据类型时系统类型Integer
> "当前对象 - 传入对象 【得到排序结果就是升序】" ---》 正整数
> "传入对象 - 当前对象 【得到排序结果就是降序】" ---》 负整数
> 问题3: 如果遇到是引用类型无法使用减号进行计算时
> "当前对象.compareTo(传入对象) 【得到排序结果就是升序】" ---》正整数
> "传入对象.compareTo(当前对象) 【得到排序结果就是降序】" ---》负整数

## 实现Compare接口的两种方式：

* 提供一个比较原则实现comparator接口

```java
import java.util.Comparator;
//提供一个类实现Comparator接口
public class SortGZ implements Comparator<Student2> {
    @Override
    public int compare(Student2 o1, Student2 o2) {
        return o2.getAge()-o1.getAge();
    }
}
```

* 使用匿名内部类或lambda表达式实现

```java
public static void main(String[] args) {
//调用TreeSet中具备Comparator接口方法,参数赋值就是实现Comparator接口的对象
//匿名内部类版本
    TreeSet<Student2> treeSet = new TreeSet<>(new
    Comparator<Student2>() {
    @Override
        public int compare(Student2 o1, Student2 o2) {
            return o1.getAge() - o2.getAge();
        }
    });
}
```

## 总结Comparable和Comparator接口

> 现在Java而言不仅只有TreeSet能排序，List集合也可以排序，Map集合也可以排序，合理规划使用排序即可，Comparable这个接口值专门针对TreeSet集合进行排序而设计一个接口，它的局限性在于它只适合自定义类存储在TreeSet进行使用，其他位置提供Sort方法是不使用Comparable作为参数，Comparator属于自定义排序接口，使用比较广泛，除了在TreeSet中可以使用之外，List集合中提供Sort和JavaAPI中提供其他Sort方法基本上都是使用Comparator参数类型，所以这两个接口建议优先掌握Comparator接口【使用广泛】，其次Comparable

## Set总结

> Set集合是一个接口继承与Collection接口和Iterable接口,Set集合本身具备排重功能和存储无序
> public interface Set<E> extends Collection<E>
> Set集合集合主要的实现类有HashSet、LinkedHashSet和TreeSet，所以Set集合接口是支持多态创建对象
> Set集合中提供可操作集合都是线程不安全，所以面临多线程处理数据的时候
> 除了这种方式之外可以使用Java5开始提供java.util.concurrent包下提供线程集合完全类来进行操作
> HashSet它是Set集合主要实现类，也是实际开发中使用比较广泛的一个类，这个类的主要实现是Hash表，底层实现是创建一个HashMap对象作为HashSet的具体实现，并且向HashSet存储数据时，其实是向HashMap中key值的位置进行数据存储
```java
//构造方法
public HashSet() {
    map = new HashMap<>();
}
//添加数据
public boolean add(E e) {
    return map.put(e, PRESENT)==null;
}

```

> HashSet的默认容量是16，加载因子是0.75，扩容大小是原有一倍在Java8之前HashSet底层主要实现是Hash表【数组+链表】形式，从Java8开始对底层存储进行优化，提供存储和查询效果将原有Hash表进行优化【数组+链表或红黑树】，向Hash表中如果存储数据，某个存储位置中链表长度大达到8的时候【存储了8个数据】，就将链表修改为红黑树，从而提高查询效率
> HashSet存储自定义类对象时，如果需要进行排重操作，需要提供equals和hashcode重写
> LinkedHashSet是HashSet子类，本身不具备任何特殊方法，所有都是来源于Set接口，唯一特点就是提供一个链表来记录存储顺序，开发中是几乎与不用，它操作可有完全仿照HashSet
> TreeSet 是Set集合中一个排序排重的集合，这个集合使用 红黑树+Hash表，当使用TreeSet的无参构造方法创建对象时，向TreeSet集合存数据，这个存储的数据必须实现Comparable接口，也可使用TreeSet的有参构造方法，方法参数是Comparator类型，实现Comparator接口进行存储数据的自定义排序
> 不是只有TreeSet才可以排序，List和Map集合都可以进行排序操作，但是这个俩个集合都会使用到ComparatorCollection集合接口是List和Set集合接口父接口，Collection集合接口继承Iterable接口，所以List和Set集合接口都是支持迭代器操作，因为List和Set集合接口都是Collection集合子接口，所以List和Set集合接口的实现了可以作为Collection集合接口的实现类使用，所以支持多态创建

```java
//Collection集合接口创建对象
Collection <Integer> c1 = new ArrayList<>();
Collection <Integer> c2 = new LinkedList<>();
Collection <Integer> c3 = new Vector<>();
Collection <Integer> c4 = new HashSet<>();
Collection <Integer> c5 = new LinkedHashSet<>();
Collection <Integer> c6 = new TreeSet<>();
```

> 因为Collection是集合接口，所以里面的方法都已经讲解完毕
> **PS：在实际开发中List集合接口中最常用类是ArrayList，Set集合接口中最常用类是HashSet**