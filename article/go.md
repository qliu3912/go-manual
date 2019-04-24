# 启动新协程运行函数 (go)
协程是一个比线程更轻量的概念，Go语言可以通过`go`关键字轻松的启动一个协程来异步执行逻辑。

声明：
```Go
import (
	"log"
	"time"
)

func main() {
	//定义一个匿名函数并赋值给a
	var a = func() {
		defer log.Println("函数a运行结束，退出后本函数所在的协程也会自动中断")
		for i := 0; i < 10; i++ {
			log.Println("函数a：", time.Now().Unix())
			time.Sleep(time.Second)
		}
	}
	//使用go关键字启动函数a，使其在新协程中执行
	go a()

	//定义一个匿名函数并赋值给b
	var b = func() {
		defer log.Println("函数a运行结束，退出后本函数所在的协程也会自动中断")
		for i := 0; i < 5; i++ {
			log.Println("函数b：", i)
			time.Sleep(time.Second)
		}
	}
	//再开启一个新协程执行函数b
	go b()

	//用一个死循环来阻塞main()，防止两个子协程还没执行完就关闭了进程，看不到协程启动后的效果
	for {
		//延迟11秒后break掉for循环，使它退出后结束main()即关闭进程
		time.Sleep(12 * time.Second)
		log.Println("退出进程")
		break
	}
}
```

##### 多个协程启动和执行并非是按代码从上到下定义的顺序来执行。
##### 所有的协程都是平级关系，在一个协程中再启动一个协程，并不会因为父协程退出了导致子协程也退出。
以下是改造自上面的代码，证明协程之间没有父子关系：
```Go
import (
	"log"
	"time"
)

func main() {
	//在新协程中执行一个匿名函数，做为父协程
	go func() {
		defer log.Println("父协程中的函数运行结束，本协程将退出，但子协程(函数a)还会继续执行")
		//定义一个匿名函数并赋值给b
		var a = func() {
			defer log.Println("函数a运行结束，退出后本函数所在的协程也会自动中断")
			for i := 0; i < 10; i++ {
				log.Println("父协程函数：", i)
				time.Sleep(time.Second)
			}
		}
		//在本协程中再开启一个新协程执行函数b
		go a()

		//循环打印证明父协程还存活
		for i := 0; i < 5; i++ {
			log.Println("子协程函数a：", time.Now().Unix())
			time.Sleep(time.Second)
		}
	}()

	//用一个死循环来阻塞main()，防止两个子协程还没执行完就关闭了进程，看不到协程启动后的效果
	for {
		//延迟11秒后break掉for循环，使它退出后结束main()即关闭进程
		time.Sleep(12 * time.Second)
		log.Println("退出进程")
		break
	}
}
```