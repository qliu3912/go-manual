# 通道（chan）
chan全称channel，从字面上就可以理解为"通道"，类似于一个队列的作用

多协程并发读写chan类型的变量时，保证读写按队列进行，防止读到脏数据。

##### 使用`chan<-`往通道里写入数据

##### 使用`<-chan`从通道里读取数据

##### chan有带缓冲和不带缓冲两种类型：

* 无缓冲的channel在写入数据后就锁住，直到数据被读出之后才能继续往里面写入新数据
* 有缓冲的channel只要缓冲队列没有用满，就可以继续写入新数据到队列尾部，直到队列用满才会被锁住写入

#### 无缓冲通道的例子：
```Go
import "time"

func main() {
	//创建一个只能存放int类型的数据，并且无缓冲的channel
	ch := make(chan int64)

	//启动一个协程
	go func() {
		//写一个死循环阻塞协程，用于不断尝试读取通道中的数据
		for {
			//读取通道中的数据，读出来之后通道会打开锁，让新数据写入
			d := <-ch
			//如果成功读取到了数据
			if d > 0 {
				//打印数据
				println("读取数据", d)
			}
			//延迟5秒钟后再尝试读取通道里的数据，是为了让通道中的数据存在5秒钟后再读取
			//可以看到写协程也会等待数据读取后才能成功写入
			time.Sleep(5 * time.Second)
		}
	}()

	//写一个死循环阻塞main()，防止进程退出
	//同时每秒不断的往通道里写入当前时间
	for {
		//取得当前时间戳
		now := time.Now().Unix()

		println("准备写入数据", now)
		//往通道里写入数据
		ch <- now
		println("成功写入数据", now)
		println()

		//等待时间走一秒再循环，防止循环太快取出来的时间都是同一秒
		time.Sleep(time.Second)
	}

}
```
##### 打印结果：
```
准备写入数据 1521449512
读取数据 1521449512
成功写入数据 1521449512

准备写入数据 1521449517
读取数据 1521449517
成功写入数据 1521449517
```
通过以上结果可以看出，虽然写操作每秒都在进行而读操作每5秒才进行一次，但读出来的时间相隔5秒，说明写协程被通通道阻塞了5秒钟才能写入一次数据。

#### 有缓冲通道的例子：
```Go
import "time"

func main() {
	//创建一个只能存放int类型的数据，有3个缓冲队列的channel
	ch := make(chan int64, 3)

	go func() {
		for {
			d := <-ch
			if d > 0 {
				println("读取数据", d)
			}
			time.Sleep(5 * time.Second)
		}
	}()

	for {
		now := time.Now().Unix()

		println("准备写入数据", now)
		ch <- now
		println("成功写入数据", now)
		println()
		time.Sleep(time.Second)
	}

}
```
##### 打印结果：
```
//下面的打印表明，协程启动后连续写入3秒钟的数据
//中间读协程还没开始读数据
准备写入数据 1521449821
成功写入数据 1521449821

准备写入数据 1521449822
成功写入数据 1521449822

准备写入数据 1521449823
成功写入数据 1521449823

//当下面这条数据写入时，由于上面3条数据把通道队列塞满了
//所以之后的数据全部要等待读出一条才能写入一条
准备写入数据 1521449824
读取数据 1521449821 //注意这个地方读的是之前写入的第一条数据
成功写入数据 1521449824

准备写入数据 1521449826
读取数据 1521449822 //依然是在读队列头部的数据，并不是最新写入到尾部的数据
成功写入数据 1521449826

准备写入数据 1521449831
读取数据 1521449823
成功写入数据 1521449831

准备写入数据 1521449836
读取数据 1521449824
成功写入数据 1521449836
```