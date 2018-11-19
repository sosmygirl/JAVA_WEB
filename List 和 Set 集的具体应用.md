# List 和 Set 集的具体应用


1 **容器的分类**
集合框架由一组用来操作对象的接口组成。不同接口描述不同类型的组。

> 映射是一种特殊的集，它是一对（pair）集，每个对表示一个元素到两一个元素的单向映射，如：
> ip地址到DNS的映射，关键字到数据库的映射，字典（词到定义的映射）等
| 类型         | 特点                                                                                 |
| ---------- | ---------------------------------------------------------------------------------- |
| Collection | 对象之间没有指定的顺序，允许重复元素                                                                 |
| Set        | 对象之间没有指定的顺序，不允许重复                                                                  |
| List       | 对象之间有指定的顺序，允许重复，引入了位置下标                                                            |
| Map        | 接口用于保存关键字（key）和数值（value）的集合，集合中每个对象加入时都提供key和Value。Map 接口既不继承 Set 也不继承 Collection。 |
|            | List、Set、Map共同的实现基础是Object数组                                                       |

![](https://d2mxuefqeaa7sj.cloudfront.net/s_E05518B4CDADCCBCA21441F45EAA6E32BBFF8EA5C98D58AA4E614087A5A57893_1538323238288_1.jpg)

![](https://d2mxuefqeaa7sj.cloudfront.net/s_E05518B4CDADCCBCA21441F45EAA6E32BBFF8EA5C98D58AA4E614087A5A57893_1538323254817_2.jpg)


除了四个历史集合类外，Java 2 框架还引入了六个集合实现，如下表所示。

| **接口** | **实现**     | **历史集合类**  |
| ------ | ---------- | ---------- |
| Set    | HashSet    |            |
|        | TreeSet    |            |
| List   | ArrayList  | Vector     |
|        | LinkedList | Stack      |
| Map    | HashMap    | Hashtable  |
|        | TreeMap    | Properties |

2  Collection 
2.1 常用方法 

  [方法](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html)
  Collection是List和Set 的父类
  集合只能是对象，集合中元素不能是基本数据类型。
  Collection接口支持如添加和去除等基本操作。除去操作的是集合元素中的一个实例。

2.2 迭代器 [Iterator](https://docs.oracle.com/javase/8/docs/api/java/util/Iterator.html)

  可以不考虑集合的类型进行遍历集合，能够安全的在遍历期间remove() 元素.
    Collection collection = new ArrayList();
    collection.add("1");
    collection.add("2");
    collection.add("3");
    collection.add("4");
    
    Iterator iterator = coollection.Iterator();//得到一个迭代器
    iterator.next();//返回一个element
    iterator.hasNext();//boolean
    iterator.isEmpty();//boolean 
    iterator.remove();//每次next后只能使用一次remove
    
## 3 [List 列表](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)

The List interface provides a special iterator, called a ******ListIterato**[r](http://ListIterator没有当前元素;它的光标位置总是位于调用previous（）返回的元素和调用next（）返回的元素之间。), that allows element insertion (插入)and replacement（替换），bidirectional access （双向访问）。
两种 搜索 方法 two methods to search for a specified object。
List ：**提供基于索引的对成员的随机访问**

| **实现**     | **操作特性**                                | **成员要求**          |
| ---------- | --------------------------------------- | ----------------- |
| ArrayList  | 提供快速的基于索引的成员访问，对尾部成员的增加和删除支持较好          | 成员可为任意Object子类的对象 |
| LinkedList | 对列表中任何位置的成员的增加和删除支持较好，但对基于索引的成员访问支持性能较差 | 成员可为任意Object子类的对象 |

## Map 

Map<K, V> 键值(Key-Value)对映射,描述了没有重复的键值对映射，map中key没有重复的，key映射唯一的value值
set of keys：

    Set key = map.keySet();

Set 集合没有重复的元素

collection of values

    Collection value = map.vlues();

values 可以相同

set of key-value mappings

    Set set = map1.entrySet();

代码：

    package com.fs.pojo04;
    
    import java.util.HashMap;
    import java.util.Map;
    
    public class MapTest {
        public static void main(String[] args) {
            Map map1 = new HashMap();
            Map map2 = new HashMap();
            map1.put("1", "a01");
            map1.put("2", "a02");
            map2.put("10", "b11");
            map2.put("11", "b12");
            //去键值为"1"的value
            System.out.println("map1.get(\"1\")" + map1.get("1"));
            System.out.println("map1.remove(\"1\")" + map1.remove("1"));
            System.out.println("map1.remove(\"1\")" + map1.remove("1"));
            //将map2全部放到map1中
            map1.putAll(map2);
            System.out.println(map1);
            map2.clear();
            System.out.println("map2.isEmpty(): " + map2.isEmpty());
            System.out.println("map1.size(): "+map1.size());
            System.out.println("map1.keySet(): "+map1.keySet());
            System.out.println("map1.values(): "+map1.values());
            System.out.println("map1.entrySet(): "+map1.entrySet());
            System.out.println("map1是否包含键值 \"11\": " + map1.containsKey("11"));
            System.out.println("map1是否包含值 \"012\": " + map1.containsValue("a01"));
        }
    }
    

结果

    map1.get("1")a01
    map1.remove("1")a01
    map1.remove("1")null
    {11=b12, 2=a02, 10=b11}
    map2.isEmpty(): true
    map1.size(): 3
    map1.keySet(): [11, 2, 10]
    map1.values(): [b12, a02, b11]
    map1.entrySet(): [11=b12, 2=a02, 10=b11]
    map1是否包含键值 "11": true
    map1是否包含值 "012": false

HashMap，LinkedHashMap和TreeMap的区别

- HashMap的存入顺序和输出顺序无关
-  LinkedHashMap 保留了键值对的存入顺序
- TreeMap则是对Map中的元素进行排序

在实际的使用中，一般使用HashMap或LinkedHashMap来存放元素，速度快，存好后，再用TreeMap来排序


    package com.fs.pojo04;
    
    import java.util.*;
    
    public class MapSortTest {
        public static void main(String[] args) {
            Map map1 = new HashMap();
            LinkedHashMap map2 = new LinkedHashMap();
    
            //map中装入随机的键值对
            Random r = new Random();
    
    
            for (int i = 0; i < 10; i++) {
                int number = r.nextInt(100);
                map1.put(number, "第" + i + "个放入的元素" + number+"\n");//Map没有按照放入的顺序排序
                map2.put(number, "第" + i + "个放入的元素" + number+"\n");//Map通过放入的顺序排序
    
            }
            System.out.println("map1未排序：" + map1.entrySet());
            System.out.println("map2未排序：" + map2.entrySet());
            //用TreeMap 的compareTo 排序
            Map sortedMap1 = new TreeMap(map1);
    
            System.out.println("map1排序后：" + sortedMap1.entrySet());
            System.out.println("map2排序后：" + new TreeMap<>(map2).entrySet());
    
        }
    }
    /*
    * map1未排序：[64=第2个放入的元素64
    , 16=第8个放入的元素16
    , 82=第5个放入的元素82
    , 2=第7个放入的元素2
    , 50=第9个放入的元素50
    , 71=第1个放入的元素71
    , 72=第6个放入的元素72
    , 41=第0个放入的元素41
    , 59=第4个放入的元素59
    , 28=第3个放入的元素28
    ]
    map2未排序：[41=第0个放入的元素41
    , 71=第1个放入的元素71
    , 64=第2个放入的元素64
    , 28=第3个放入的元素28
    , 59=第4个放入的元素59
    , 82=第5个放入的元素82
    , 72=第6个放入的元素72
    , 2=第7个放入的元素2
    , 16=第8个放入的元素16
    , 50=第9个放入的元素50
    ]
    map1排序后：[2=第7个放入的元素2
    , 16=第8个放入的元素16
    , 28=第3个放入的元素28
    , 41=第0个放入的元素41
    , 50=第9个放入的元素50
    , 59=第4个放入的元素59
    , 64=第2个放入的元素64
    , 71=第1个放入的元素71
    , 72=第6个放入的元素72
    , 82=第5个放入的元素82
    ]
    map2排序后：[2=第7个放入的元素2
    , 16=第8个放入的元素16
    , 28=第3个放入的元素28
    , 41=第0个放入的元素41
    , 50=第9个放入的元素50
    , 59=第4个放入的元素59
    , 64=第2个放入的元素64
    , 71=第1个放入的元素71
    , 72=第6个放入的元素72
    , 82=第5个放入的元素82
    ]
    * */
    


TreeMap中是根据键（Key）进行排序的。而如果我们要使用TreeMap来进行正常的排序的话，Key 中存放的对象必须实现**Comparable** 接口。

**Comparator 接口**

    package com.fs.pojo03;
    
    import java.util.Comparator;
    
    public class SortedStuName implements Comparator<Student> {
        @Override
        public int compare(Student stu1, Student stu2) {
            int n = stu1.getName().compareTo(stu2.getName());
            if (n==0){
                return  new Integer(stu1.getAge()).compareTo(new Integer(stu2.getAge()));
    
            }
            return n;
        }
    }
    

**实现compareble接口**

    package com.fs.pojo03;
    
    import java.util.HashMap;
    
    public class Student implements Comparable<Student> {
        private String name;
        private int age;
    
    
        public Student() {
        }
    
        public Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        @Override
        public int compareTo(Student s) {
            //return this.age>s.age?1:this.age<s.age?-1:0;
           int n =  Integer.valueOf(this.age).compareTo(Integer.valueOf(s.age));
            if (n==0){
                return this.name.compareTo(s.name);
            }
            return n;
        }
    
        @Override
        public int hashCode() {
            return name.hashCode()+age;
        }
        @Override
        public boolean equals(Object o) {
            if (!(o instanceof Student)) {
                throw new ClassCastException("类型不匹配");
            }
            Student stu = (Student) o;
            return this.name.equals(stu.name) && this.age == stu.age;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public int getAge() {
            return age;
        }
    
        public void setAge(int age) {
            this.age = age;
        }
    }
    


    package com.fs.pojo03;
    
    import java.util.*;
    
    public class MapTest {
        public static void main(String[] args) {
            HashMap<Student, String> map = new HashMap<>();
            map.put(new Student("lisi01",21), "北京");
            map.put(new Student("lisi01",21), "上海");//覆盖第一个值
            map.put(new Student("lisi02",23), "深圳");
            map.put(new Student("lisi04",22), "武汉");
            map.put(new Student("lisi03", 24), "天津");
            Set<Student> set = map.keySet();
            Iterator<Student> it = set.iterator();
            System.out.println("------没有顺序--------");
            while (it.hasNext()) {
                Student stu = it.next();
                String s = map.get(stu);
                System.out.println(stu.getName()+"..."+stu.getAge()+"..."+s);
            }
            TreeMap<Student, String> map2 = new TreeMap<Student, String>();
            map2.put(new Student("lisi01",21), "北京");
            map2.put(new Student("lisi01",21), "上海");//覆盖第一个值
            map2.put(new Student("lisi02",23), "深圳");
            map2.put(new Student("lisi04",22), "武汉");
            map2.put(new Student("lisi03", 24), "天津");
            Set<Student> sortedStu = map2.keySet();
            Iterator<Student> sortedIt = sortedStu.iterator();
            System.out.println("--------按年龄排序----------");
            while (sortedIt.hasNext()) {
                Student next = sortedIt.next();
                String v = map2.get(next);
                System.out.println(next.getName() + "..." + next.getAge() + "..." + v);
            }
    
    
            TreeMap<Student, String> mapSortedByName = new TreeMap<Student, String>(new SortedStuName());
            mapSortedByName.put(new Student("lisi01",21), "北京");
            mapSortedByName.put(new Student("lisi01",21), "上海");//覆盖第一个值
            mapSortedByName.put(new Student("lisi02",23), "深圳");
            mapSortedByName.put(new Student("lisi04",22), "武汉");
            mapSortedByName.put(new Student("lisi05",22), "武汉");
            mapSortedByName.put(new Student("lisi05",21), "武汉");
            mapSortedByName.put(new Student("lisi03", 24), "天津");
            Set<Student> sortedStu2 = mapSortedByName.keySet();
            Iterator<Student> sortedIt2 = sortedStu2.iterator();
            System.out.println("--------按名字排序----------");//名字相同按年龄排序
            while (sortedIt2.hasNext()) {
                Student next = sortedIt2.next();
                String v = mapSortedByName.get(next);
                System.out.println(next.getName() + "..." + next.getAge() + "..." + v);
            }
        }
    }
    /*
    * ------没有顺序--------
    lisi01...21...上海
    lisi02...23...深圳
    lisi04...22...武汉
    lisi03...24...天津
    --------按年龄排序----------
    lisi01...21...上海
    lisi04...22...武汉
    lisi02...23...深圳
    lisi03...24...天津
    --------按名字排序----------
    lisi01...21...上海
    lisi02...23...深圳
    lisi03...24...天津
    lisi04...22...武汉
    lisi05...21...武汉
    lisi05...22...武汉
    * */


| **Collection/Map** | **接口**    | **成员重复性**       | **元素存放顺序（Ordered/Sorted）**                  | **元素中被调用的方法**        | **基于那中数据结构来实现的**   |
| ------------------ | --------- | --------------- | ------------------------------------------- | -------------------- | ------------------ |
| HashSet            | Set       | Unique elements | No order                                    | equals() compareTo() | Hash 表             |
| LinkedHashSet      | Set       | Unique elements | Insertion order                             | equals() compareTo() | Hash 表和双向链表        |
| TreeSet            | SortedSet | Unique elements | Sorted                                      | equals() compareTo() | 平衡树（Balanced tree） |
| ArrayList          | List      | Allowed         | Insertion order                             | equals()             | 数组                 |
| LinkedList         | List      | Allowed         | Insertion order                             | equals()             | 链表                 |
| Vector             | List      | Allowed         | Insertion order                             | equals()             | 数组                 |
| HashMap            | Map       | Unique keys     | No order                                    | equals() compareTo() | Hash 表             |
| LinkedHashMap      | Map       | Unique keys     | Key insertion order/Access order of entries | equals() compareTo() | Hash 表和双向链表        |
| HashTable          | Map       | Unique keys     | No order                                    | equals() compareTo() | Hash 表             |
| TreeMap            | SortedMap | Unique keys     | Sorted in key order                         | equals() compareTo() | 平衡树（Balanced tree） |


