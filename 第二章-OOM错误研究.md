jvm内存区域中只有程序计数器不会抛出OutOfMemoryError（OOM），其它的内存都会触发OOM。

### 样例展示

jvm参数：

```
-Xms20M -Xmx20M -Xmn10M -XX:+HeapDumpOnOutOfMemoryError  
```

| 参数名称 | 含义         | 默认值            | 描述                                                         |
| -------- | ------------ | ----------------- | ------------------------------------------------------------ |
| -Xms     | 初始堆大小   | 物理内存1/64(<1G) | 内存空闲区域小于40(MinHeapFreeRatio)时，内存会增大至-Xmx的值 |
| -Xmx     | 堆的最大值   | 物理内存1/4(<1G)  | 内存空闲区域大于70(MaxHeapFreeRatio)时，内存会减小至-Xms的值 |
| -Xmn     | 年轻代的大小 |                   | eden+2*survivor的值。整个堆=年轻代+老年代+元空间。增大年轻代的大小意味减小老年代的大小。Sun官方推荐为整个堆的3/8 |

代码展示：

```
public class JvmStudyApplication {

    static class OOMObject { }

    public static void main(String[] args) {
        List<OOMObject> list = new ArrayList<OOMObject>();
        while (true)
        {
            list.add(new OOMObject());
        }
    }

}
```

结果展示：

```
java.lang.OutOfMemoryError: Java heap space
Dumping heap to java_pid98564.hprof ...
Heap dump file created [30181525 bytes in 0.097 secs]
Exception in thread "main" java.lang.OutOfMemoryError: Java heap space
	at java.util.Arrays.copyOf(Arrays.java:3210)
	at java.util.Arrays.copyOf(Arrays.java:3181)
	at java.util.ArrayList.grow(ArrayList.java:265)
	at java.util.ArrayList.ensureExplicitCapacity(ArrayList.java:239)
	at java.util.ArrayList.ensureCapacityInternal(ArrayList.java:231)
	at java.util.ArrayList.add(ArrayList.java:462)
	at com.example.jvmstudy.JvmStudyApplication.main(JvmStudyApplication.java:18)
```

#### Mat分析

之后再详细介绍



参考文献：

- [MAT从入门到精通（二）](https://zhuanlan.zhihu.com/p/57347496)
- [JVM系列三:JVM参数设置、分析](https://www.cnblogs.com/redcreen/archive/2011/05/04/2037057.html)

