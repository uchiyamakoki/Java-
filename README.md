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


  
  
  
  
  
  
  
 
 



