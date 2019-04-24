# select
select可以通过多个case来监听多个chan通道的I/O事件，用于触发不同的业务逻辑。

```Go
import (
	"strconv"
	"time"
)

func main() {
	//创建两个无缓冲通道
	read := make(chan int64)
	send := make(chan int64)

	//启动协程，每2秒钟后向read通道写入数据
	//模拟收到客户端发来的消息
	go func() {
		for {
			read <- time.Now().Unix()
			time.Sleep(time.Second)
		}
	}()

	//再启动一个协程，每2秒钟向send通道写入数据
	//模拟向客户端发送数据
	go func() {
		for {
			send <- time.Now().Unix()
			time.Sleep(2 * time.Second)
		}
	}()

	//由于select一定case的条件成立，执行完case中的逻辑就会退出select
	//所以这里写一个死循环，每次select退出就马上再启动select，用于不断的监听通道I/O事件
	for {
		//监听多个通道的I/O事件
		select {
		case t := <-send: //如果通道send内成功读出了数据
			ts := strconv.FormatInt(t, 10)
			//将通道内的数据发往客户端
			println("向客户端发送消息：", ts)
		case t := <-read: //如果通道read内成功读出了数据
			ts := strconv.FormatInt(t, 10)
			//处理从客户端收到的消息
			println("收到客户端发来的消息：", ts)
		}
	}
}
```