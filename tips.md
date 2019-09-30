**MD5生成31位**

在使用MD5加密时，生成的密文长度只有31位，该怎么解决？

代码如下：

```
public static String toMd5(String str) {
        String re = null;
        byte encrypt[];
        try {
            byte[] tem = str.getBytes();
            MessageDigest md5 = MessageDigest.getInstance("md5");
            md5.reset();
            md5.update(tem);
            encrypt = md5.digest();
            StringBuilder sb = new StringBuilder();
            for (byte t : encrypt) {
                sb.append(Integer.toHexString(t & 0xFF));
            }
            re = sb.toString();
        } catch (NoSuchAlgorithmException e) {
            e.printStackTrace();
        }
        return re;
    }
```

比如加密admin，结果如图：



正常的32位加密结果为：21232f297a57a5a743894a0e4a801fc3
而我的代码加密结果为：21232f297a57a5a743894ae4a801fc3

正常的第23位的“0”不见了

问题出在这一句：`Integer.toHexString(t & 0xFF)`

**当`t`为`14`时，十六进制就是`0e`，转化成字符串会忽略掉前导零。**

改一下就行了：

```
String s = Integer.toHexString(t & 0xFF);
if (s.length() == 1) {
    s = "0" + s;
}
```

另外，`md5`不是一种加密算法，是计算消息摘要的，可以用来作数据完整性的校验。
