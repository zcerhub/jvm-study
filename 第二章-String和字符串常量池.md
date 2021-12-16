常量池中存在类、方法、接口中的常量，在编译期已经确定。字符串常量也保存在常量池。

#### 实例1

```
        String s0="kvill";
        String s1="kvill";
        String s2="kv" + "ill";
        System.out.println( s0==s1 );
        System.out.println( s0==s2 );
```

结果展示：

```
true
true
```

- 字符串保存在常量池中，有且只有一份。所以s0==s1返回true
- 字符串常量之间的运算结果仍旧是字符串常量（操作数都必须为字符串常量）。所以s0==s2返回true

#### 实例2

```
        String s0="kvill";
        String s1=new String("kvill");
        String s2="kv" + new String("ill");
        System.out.println( s0==s1 );
        System.out.println( s0==s2 );
        System.out.println( s1==s2 );
```

结果展示：

```
false
false
false
```

- new创建为字符串变量，而字符串变量保存在堆上。所以s0==s1为false
- 字符串常量和字符串变量结果为字符串变量结果仍旧为字符串变量。所以s0==s2为false
- 字符串变量s1、s2指向两个不同的字符串。所以s1==s2为false

#### 实例3

String.intern检查常量池中是否有该字符串变量的内容，如果没有，否则将该字符串变量的内容拷贝到常量池并返回常量池中的引用值。如果有，直接返回常量池中的引用值。

```
        String s0= "kvill";
        String s1=new String("kvill");
        String s2=new String("kvill");
        s2=s2.intern(); //把常量池中“kvill”的引用赋给s2
        System.out.println( s0==s1.intern() );
        System.out.println( s0==s2 );
```

结果展示：

```
true
true
```

- 常量池中已经存在"kvill"，s1.intern指向常量池中的引用，所以s0==s1.intern()、s0==s2为true

  

#### 参考文献

- [Java提高篇——理解String 及 String.intern() 在实际中的应用](https://www.cnblogs.com/Qian123/p/5707154.html)

