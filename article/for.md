# for 循环
Go中只有for一种循环，但有以下几种不同的用法：

##### 当型循环
```Go
for i := 0; i < 10; i++ {
    log.Println(i)
    if i < 5 {
        continue //继续下一次循环，不执行下面的代码
    }
    log.Println("退出循环")
    break //退出循环
}
```

##### 遍历，不需要知道s的下标
```Go
s := []string{"a", "b", "c", "d", "e", "f"}
for i, v := range s {
    log.Println(i)  //打印当前遍历到的索引
    log.Println(v)  //打印当前遍历到的值
}

//可以只需要索引
for i := range s {
    log.Println(s[i])  //根据当前遍历到的索引来取值
}

//也可以只需要值
for _, v := range s {
    log.Println(v)  //打印当前遍历到的值
}
```
for range可以遍历array、slice、map等类型