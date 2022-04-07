==映射 Map==

​		将对象映射到其他对象的能力是解决编程问题的有效方法。例如，考虑一个程序， 它被用来检查 Java 的 Random 类的随机性。理想情况下，Random 会产生完美的数 字分布，但为了测试这一点，则需要生成大量的随机数，并计算落在各种范围内的数字 个数。Map 可以很容易地解决这个问题。在本例中，键是 Random 生成的数字，而值 是该数字出现的次数：

``

```
Random random = new Random(47);
Map<Integer, Integer> integerMap = new HashMap<>();
for (int i = 0; i < 10000; i++) {
    int r = random.nextInt(20);
    Integer freq = integerMap.get(r);
    integerMap.put(r, freq == null ? 1 : freq + 1);
}
System.out.println(integerMap);
```

Map 与数组和其他的 Collection 一样，可以轻松地扩展到多个维度，只需要创建 一个值为 Map 的 Map

