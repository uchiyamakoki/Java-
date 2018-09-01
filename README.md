 # 2018.8.19 JavaSE-
 21、14.21_常见对象(BigDecimal的加减乘除法的使用)<br>
 BigDecimal（使用工具类一般要用构造方法创建对象 一般可以用double或者String）*<br>
 *add(BigDecimal val) 加法<br>
 *subtract（BigDecimal val） 减法<br>
 *mulpitly（BigDecimal val） 乘法<br>
 *divide（BigDecimal val） 除法 *可以小数点后余几位（BigDecimal val，int 位数，BigDecimal.ROUND_HALF_UP） 最后一个参数是取舍规则<br>
  # 2018.8.21 JavaSE-day15
  1、15.01_集合框架(对象数组的概述和使用)
  # 2018.8.26 JavaSE-day16
  1、3、16.03_集合框架(Vector的特有功能)
  
  说到Vector 想到它是List的三个儿子之一，vector的特点是线程安全，但查询效率低，增删也不如linkedlist，底层实现为数组.(1.0出现，集合1.2出现)
  
  拥有获取功能 public Enumeration elements（）
  
  ``` HTML
  Enumeration en=v.elements(); //本质为定义一个类似List迭代器的东西，当然不如后者
 while (en.hasMoreElements()){ //-----hasNext()
            String s= (String) en.nextElement();//-----next()
            System.out.println(s);
        }
```

添加功能则是集合基本模式

  ``` HTML
 Vector v=new Vector();

        v.addElement("hello");//-----add()
        v.addElement("world");
        v.addElement("java");
        for (int x=0;x<v.size();x++){
            String s= (String) v.elementAt(x);//------get()
            System.out.println(s);
        }
```

顺便撤了一个升级原因：安全，效率，简化书写（Vector被淘汰原因，可能淘汰有歧义。）

 # 2018.8.28 JavaSE-day16
  4、16.04_集合框架(LinkedList的特有功能)

今天学的是链表LinkedList，LinkedList底层是链表，所以查询慢，但是相对的增删方便，因此有addFirst，addLast，removeFirst，removeLast等方法；线程方面不安全，所以效率高（一般不安全的好处）。

代码演示：
 ``` HTML
LinkedList link=new LinkedList();

        link.add("hello");
        link.add("world");
        link.addLast("android");
        link.add("java");

        link.addFirst("javaee");
        link.addLast("android");
        System.out.println(link.getFirst());
        System.out.println(link.getLast());
        System.out.println(link);
        System.out.println(link.removeFirst());
        System.out.println(link.removeLast());
```
 # 2018.8.29 JavaSE-day16
 
 5、16.05_集合框架(去除ArrayList集合中的重复字符串元素案例1)
 
 今天是个练习题。一般步骤，创建集合对象，添加元素，创建新集合，遍历旧的集合，添加元素到新集合，同时判断是否重复
  ``` HTML
      ArrayList array=new ArrayList();

        array.add("hello");
        array.add("world");
        array.add("java");
        array.add("world");

        ArrayList newArray=new ArrayList();

        Iterator it=array.iterator();
        while (it.hasNext()){
            String s= (String) it.next();
            if (!newArray.contains(s)){
                newArray.add(s);
            }
        }
        for (int x=0;x<newArray.size();x++){
            String s= (String) newArray.get(x);
            System.out.println(s);
        }
```
# 2018.8.30 JavaSE-day16

7、16.07_集合框架(去除ArrayList集合中的重复字符串元素案例2)

这次是要求基本相同，不同就是不创建新集合。原理是基于选择排序思想。拿0，1,2...索引

 ``` HTML
       ArrayList array=new ArrayList();

        array.add("hello");
        array.add("world");
        array.add("java");
        array.add("world");

        for (int x=0;x<array.size()-1;x++){
            for (int y=x+1;y<array.size();y++){
                if (array.get(x).equals(array.get(y))){
                    array.remove(y); //remove之后长度会变短
                    y--;//所以要y--
                }
            }
        }

        Iterator it=array.iterator();
        while (it.hasNext()){
            String s= (String) it.next();
            System.out.println(s);
        }
```
# 2018.8.30 JavaSE-day16

8、16.08_集合框架(去除ArrayList集合中的重复自定义对象元素案例)

这里主要是contains(s)方法，主要是indexof→equals（），这个方法在s是实体类时，实体类没有重写，用的是Object的，所以需要在实体类里重写equals（）。

 ``` HTML
      ArrayList array=new ArrayList();

        Student s1=new Student("余一",27);
        Student s2=new Student("沈宁",40);
        Student s3=new Student("王珞蓉",35);
        Student s4=new Student("郑紫悦",18);
        Student s5=new Student("徐榕霞",16);
        Student s6=new Student("余一",27);

        array.add(s1);
        array.add(s2);
        array.add(s3);
        array.add(s4);
        array.add(s5);
        array.add(s6);


        ArrayList newArray=new ArrayList();
        Iterator it=array.iterator();
        while (it.hasNext()){
            Student s= (Student) it.next();
            if (!newArray.contains(s)){
                newArray.add(s);
            }
        }
        for (int x=0;x<newArray.size();x++){
            Student s= (Student) newArray.get(x);
            System.out.println(s.getName()+s.getAge());
        }
```

9、16.09_集合框架(用LinkedList实现栈结构的集合代码)

栈特点，先进后出

``` HTML
     LinkedList link=new LinkedList();
        link.addFirst("hello");
        link.addFirst("world");
        link.addFirst("java");

        Iterator it=link.iterator();
        while (it.hasNext()){
            String s= (String) it.next();
            System.out.println(s);
        }
```

10、16.10_集合框架(用LinkedList模拟栈数据结构的集合并测试案例)

思路就是构造方法时其实是新建了一个LinkedL，然后就能在新建功能时使用LinkedList

而get时，使用removeFirst()，返回(getFirst的功能)并remove。所以当然也要判断一下为空。

``` HTML
  MyStack ms=new MyStack();

        ms.add("hello");
        ms.add("world");
        ms.add("java");



        while (!ms.isEmpty()){
            System.out.println(ms.get());
        }

  public class MyStack {

    private LinkedList link;

    public MyStack(){
        link=new LinkedList();
    }

    public void add(Object obj){
        link.addFirst(obj);
    }

    public Object get(){
      // return link.getFirst();
        return link.removeFirst();
    }

    public boolean isEmpty(){
        return link.isEmpty();
    }
}
```

# 2018.8.30 JavaSE-day16
  
11、16.11_集合框架(泛型概述和基本使用)

所谓泛型（创建对象调用方法时才明确，把类型当参数一样传递，当然只能说引用类型）就是像ArrayList<E>后面那个E,主要用于一些集合遍历问题。 array.add（10） 复习一下自动装箱int→Integer
 
原理就像 String[] arr=new String(); str[0]=10 会自动报错的原理，因为明确了元素是字符串

好处：把运行时问题提前到了编译时间；避免了强制类型转换 就之前那种（String）it.next（）这样的；优化了程序设计，解决了黄色警告线
  
 
 



