---
date: 2020/11/16
comments: true
title: Java多态经典题

tags: 
  - Java基础
  - 小知识点
categories: Java
---



# Java多态经典题



​		之前看过几次多态的题，当时感觉搞清楚了，但是过一段时间感觉又模糊不确定了，所以记录一下，而且后来在项目中有涉及相关的内容，应该会有更深的体会。



**题目：**

```java
package test.经典多态案例;

public class TestDuoTai {
    public static void main(String[] args) {
        A a1 = new A();
        A a2 = new B();
        B b = new B();
        C c = new C();
        D d = new D();

        System.out.println("1--" + a1.show(b) + "  " + System.identityHashCode(a1));      		  // 为什么会向上找
        System.out.println("2--" + a1.show(c));
        System.out.println("3--" + a1.show(d));
        System.out.println("4--" + a2.show(b) + "  " + System.identityHashCode(a2));
        /**(想法1.0)
         多态情况下，a2为A类型的引用，指向B类对象，
         先在B类里找有无该方法，有。但是父类A中没有，于是不能直接用B类的该方法，按照前三个的逻辑先去A类中			找，A类中有show(A obj)，但是A的子类B类中重写了show(A obj)，所以调用B类的该方法
         */

        /**(想法2.0)
         *多态情况下，a2为A类型的引用，指向B类对象，在A类中找有无该方法，没有，但是A类为B类父类，所以调		 *用A类的show(A obj)方法，然后A类的子类B重写了show(A obj)方法，
         * 所以最终调用B类的show(A obj)方法
         * */

        // 只有方法才有多态性！！！

        System.out.println("5--" + a2.show(c));
        System.out.println("6--" + a2.show(d));
        System.out.println("7--" + b.show(b));
        System.out.println("8--" + b.show(c));
        
        // 这里因为B类继承A类，而A类有该方法，且没被B重写，所以B类中隐含有该方法。
        System.out.println("9--" + b.show(d));  


    }
}

class A {
    public String show(D obj) {
        return ("A and D");
    }

    public String show(A obj) {
        return ("A and A");
    }

}

class B extends A {
    public int num1 = 10;

    public String show(B obj) {
        return ("B and B");
    }

    public String show(A obj) {
        return ("B and A");
    }

    /*  子类B中包含了父类A的这两个方法，只是B类重写覆盖了show(A obj)
    public String show(D obj) {
        return ("A and D");
    }

    public String show(A obj) {
        return ("A and A");
    }
     */
}

class C extends B {
}

class D extends B {
}

```



**注意：**对于a2的情况，也就是父类引用指向子类对象的，a2是无法调用A类中没有而B类中有的方法的。也就是对于子类独有的方法，这个父类引用是无法调用的。





运行结果：

> 1--A and A  460141958
> 2--A and A
> 3--A and D
> 4--B and A  1163157884
> 5--B and A
> 6--A and D
> 7--B and B
> 8--B and B
> 9--A and D