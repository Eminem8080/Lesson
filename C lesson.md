# Union 赋值错乱问题

如果定义了几个变量，但是在没有使用之前，就重新赋值，那么前后的值就会有覆盖。具体问题如下所示。

```c
void unitTest(){
    union Data{
        int i;
        float f;
        char str[20];
    };
    union Data data;
    data.i = 10;
    printf("data.i=%d\n", data.i);


data.f = 225.6;
printf("data.f=%f\n",data.f);

strcpy(data.str, "tanksu");
printf("data.str=%s\n", data.str);

//如果直接全部赋值，那么里面的值就有损坏
//如下代码
/**
 * data.i = 10;
   data.f = 220.5;
   strcpy( data.str, "C Programming");
     * 
     * 输出：
     * data.i : 1917853763
       data.f : 4122360580327794860452759994368.000000
       data.str : C Programming
     */
}
```

上面的结果可以看出来：共用体成员之间会相互影响，修改一个成员的值会影响其他成员。

那么这是如何来影响的呢？ 
这个共同体需要的空间长度为20个字节，那么我们填充i，只需要填充前面4个字节，而填充f，则需要前面8个字节，但是如果我填充str，则取药填充20个字节。一句话来说，填充f，会影响i；填充str，则会影响i和f。

那么就可以知道，在我们填充了C Programming字串之后，i只需要前4位的字节，f需要前8位的字节。那么取出来对应的Unicode码对应的字符应该就不是前面赋值给i和f对应的字符了。那么导致的原因也就出来了。
