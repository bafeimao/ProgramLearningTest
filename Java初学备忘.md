```java
public class PrimaryTypes {
    public static void main(String[] args) {
        boolean a=1<2;
        boolean b=1>2;
        System.out.println(a || (10/0<2));
                //或或做了优化只要第一个为true则输出不计算第二个，或则会两个都计算，一般用或或
        System.out.println(a | (10/0>1));
    }
}
```
Ctrl + ALT +L reformat code