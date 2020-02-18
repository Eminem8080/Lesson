## 1.Kotlin 的 @JvmStatic 和 @JvmField 注解

常用在伴生对象或者伴生方法（即java中的静态对象宇方法）

```kotlin
class TestStatic {
    private val otherField = 0

    companion object {
        val BIG_INTEGER = BigInteger.ONE

        fun method() {
            println("call method")
        }
    }
}
```

静态方法和静态变量会被放在 `companion object` 当中，成为伴生方法和伴生常量。而这时候，会发现在 Java 中调用它们的方式会不一样，如下：

```kotlin
public static void main(String[] args) {
    TestStatic.Companion.method();
    BigInteger bigInteger = TestStatic.Companion.getBIG_INTEGER();
}
```

如果要使转换后的 Kotlin 代码在 Java 上调用起来和以前的习惯一样，则需要分别使用 `@JvmStatic` 和 `@JvmField` 注解，才能使它们暴露为静态方法或静态字段，如下：

```kotlin
 @JvmField val BIG_INTEGER = BigInteger.ONE

    @JvmStatic fun method() {
        println("call method")
    }
```

这样 Java 对 Kotlin 的调用习惯就和以前一样了

```java
public static void main(String[] args) {
    TestStatic.method();
    BigInteger bigInteger = TestStatic.BIG_INTEGER;
}
```

关于这一点，在《Android Kotlin 指南》的文档中有提到，分别如下：

伴生函数：

在 “companion object” 中的公共函数必须用使用 @JvmStatic 注解才能暴露为静态方法。

如果没有这个注解，这些函数仅可用作静态 Companion 字段上的实例方法。

伴生常量：

在 companion object 中的公共、非 const 的属性 实际上为常量 必须用 @JvmField 注解才能暴露为静态字段。

如果没有这个注解，这些属性只能作为静态 Companion 字段中奇怪命名的 ‘getters’ 实例。而只使用 @JvmStatic 而不是 @JvmField 的话，会将奇怪命名的 ‘getters’ 移到类的静态方法中，但仍然是不正确的。

