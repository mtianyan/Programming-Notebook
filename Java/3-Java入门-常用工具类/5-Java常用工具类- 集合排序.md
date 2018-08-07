Java工具类中提供了两种方法来排序：

`java.util.Collections.sort(java.util.List)`

`java.util.Collections.sort(java.util.List, java.util.Comparator)`

```java
package cn.mtianyan.sort;

public class Cat implements Comparable{
    private String name; //名字
    private int month; //年龄
    private String species;//品种

    @Override
    public String toString() {
        return "[姓名：" + name + ", 年龄：" + month + ", 品种：" + species + "]";
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getMonth() {
        return month;
    }

    public void setMonth(int month) {
        this.month = month;
    }

    public String getSpecies() {
        return species;
    }

    public void setSpecies(String species) {
        this.species = species;
    }

    public Cat(String name, int month, String species) {
        this.name = name;
        this.month = month;
        this.species = species;
    }

    @Override
    public int compareTo(Object o) {
        return this.month-((Cat)o).month;
    }
}
```

```java
package cn.mtianyan.sort;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class CatTest{
    public static void main(String[] args) {
        List<Cat> list = new ArrayList<>();
        // 定义宠物猫对象
        Cat huahua = new Cat("花花", 12, "英国短毛猫");
        Cat fanfan = new Cat("凡凡", 3, "中华田园猫");
        Cat huahua02 = new Cat("花花二代", 2, "英国短毛猫");
        list.add(huahua);
        list.add(fanfan);
        list.add(huahua02);
        System.out.println("排序前宠物猫信息");
        for (Cat cat: list) {
            System.out.println(cat);
        }

        // 执行排序操作
        Collections.sort(list); // Cat必须实现Comparable接口，并实现其方法
        System.out.println("按年龄从大到小排序之后宠物猫信息");
        for (Cat cat: list) {
            System.out.println(cat);
        }
    }
}
```

使用Collection.sort方法来进行排序，被排序对象必须实现Comparable接口，并重写compareTo方法

```java
 @Override
    public int compareTo(Object o) {
        return this.month-((Cat)o).month;
    }
```

将此对象与指定的对象进行比较以进行排序。 返回一个负整数，零或正整数，分别对应该对象小于，等于或大于指定对象。

比如猫的例子，第一个12与第二个3进行比较。12-3=9是大于的。
下图提示语有错误: 应该为从小到大。

![](http://myphoto.mtianyan.cn/20180807222610_d3M100_Screenshot.jpeg)

#### 名字字符串排序

```java
 @Override
    public int compareTo(Object o) {
        return ((Cat)o).name.compareTo(this.name);
    }
```

```java
  // 定义宠物猫对象
        Cat huahua = new Cat("aa", 12, "英国短毛猫");
        Cat fanfan = new Cat("bb", 3, "中华田园猫");
        Cat huahua02 = new Cat("cc", 2, "英国短毛猫");
```

运行结果:

![](http://myphoto.mtianyan.cn/20180807223126_wY6uvb_Screenshot.jpeg)

### Collections.sort(List list, Comparator<T> comparator)

```java
package cn.mtianyan.sort;

public class CatTwo {
    private String name; //名字
    private int month; //年龄
    private String species;//品种

    @Override
    public String toString() {
        return "[姓名：" + name + ", 年龄：" + month + ", 品种：" + species + "]";
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getMonth() {
        return month;
    }

    public void setMonth(int month) {
        this.month = month;
    }

    public String getSpecies() {
        return species;
    }

    public void setSpecies(String species) {
        this.species = species;
    }

    public CatTwo(String name, int month, String species) {
        this.name = name;
        this.month = month;
        this.species = species;
    }
}
```

```java
package cn.mtianyan.sort;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class CatTwoTest {
    public static void main(String[] args) {
        List<CatTwo> list = new ArrayList<>();
        // 定义宠物猫对象
        CatTwo huahua = new CatTwo("aa", 12, "英国短毛猫");
        CatTwo fanfan = new CatTwo("bb", 3, "中华田园猫");
        CatTwo huahua02 = new CatTwo("cc", 2, "英国短毛猫");
        list.add(huahua);
        list.add(fanfan);
        list.add(huahua02);
        System.out.println("排序前宠物猫信息");
        for (CatTwo cat: list) {
            System.out.println(cat);
        }
        Comparator<CatTwo> comparator = new Comparator<CatTwo>() {
            @Override
            public int compare(CatTwo o1, CatTwo o2) {
                return o1.getMonth() - o2.getMonth();
            }
        };

        Collections.sort(list,comparator);
        System.out.println("排序后宠物猫信息(按月份从小到大)");
        for (CatTwo cat: list) {
            System.out.println(cat);
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180807224006_uKwSO4_Screenshot.jpeg)

#### 字符串名字从大到小

```java
            @Override
            public int compare(CatTwo o1, CatTwo o2) {
//                return o1.getMonth() - o2.getMonth();
                return o2.getName().compareTo(o1.getName());
            }
        };

        Collections.sort(list,comparator);
        System.out.println("排序后宠物猫信息(按名字从大到小)");
```

运行结果:

![](http://myphoto.mtianyan.cn/20180807224152_Z03WhR_Screenshot.jpeg)

```java
package cn.mtianyan.sort;

import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class SortArray {
    public static void main(String[] args) {
        Character [] charArray = new Character[]{'m','t','i','a','n','y','a','n'};
        List<Character> list = Arrays.asList(charArray);

        System.out.println("====Character排序前====");
        for (Character character:list) {
            System.out.print(character+" ");
        }



        System.out.println();
        System.out.println("====Character正序排序后====");
        Collections.sort(list);
        for (Character character:list) {
            System.out.print(character+" ");
        }

        System.out.println();
        System.out.println("====Character逆序排序后====");
        Collections.sort(list,Collections.reverseOrder());
        for (Character character:list) {
            System.out.print(character+" ");
        }

        String [] stringArray = new String[]{"yes","ha","mtianyan","ab"};
        System.out.println();
        List<String> list1 = Arrays.asList(stringArray);
        System.out.println("====String排序前====");
        for (String string:list1) {
            System.out.print(string+" ");
        }
        System.out.println();
        Collections.sort(list1);
        System.out.println("====String正序排序后====");
        for (String string:list1) {
            System.out.print(string+" ");
        }
        Comparator cmp1 = Collections.reverseOrder();
        Collections.sort(list1,cmp1);
        System.out.println();
        System.out.println("====String逆序排序后====");
        for (String string:list1) {
            System.out.print(string+" ");
        }

        Integer[] intArray = new Integer[]{8,6,3,4,7,5,1};
        List<Integer> list2 = Arrays.asList(intArray);
        System.out.println();
        System.out.println("====Integer排序前====");
        for (Integer integer:list2) {
            System.out.print(integer+" ");
        }
        System.out.println();
        System.out.println("====Integer正序排序后====");
        Collections.sort(list2);
        for (Integer integer:list2) {
            System.out.print(integer+" ");
        }
        System.out.println();
        System.out.println("====Integer逆序排序后====");
        Collections.sort(list2,Collections.reverseOrder());
        for (Integer integer:list2) {
            System.out.print(integer+" ");
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180807232345_pX2Qam_Screenshot.jpeg)

```java
package cn.mtianyan.sort;

import java.util.HashSet;
import java.util.Set;
import java.util.concurrent.ConcurrentSkipListSet;

public class SortedMap {
    public static void main(String[] args) {

        Set<String> set =  new HashSet<>();
        set.add("ccc");
        set.add("ddd");
        set.add("eee");
        set.add("aaa");
        set.add("bbb");


        for (String string:set){
            System.out.println(string);
        }
        System.out.println("=============");
        ConcurrentSkipListSet<String> concurrentSkipListSet = new ConcurrentSkipListSet<>();
        concurrentSkipListSet.add("ccc");
        concurrentSkipListSet.add("ddd");
        concurrentSkipListSet.add("eee");
        concurrentSkipListSet.add("aaa");
        concurrentSkipListSet.add("bbb");


        for (String string:concurrentSkipListSet) {
            System.out.println(string);
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180807234858_BrRpYE_Screenshot.jpeg)

https://www.zhihu.com/question/28414001

SortedMap接口的实现类ConcurrentSkipListMap

下一节我们将学习泛型。



