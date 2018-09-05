# chan 的实例

- 实现多并发,但是没有解决协程什么时候把消息读完了
```go
package main

import (
	"fmt"
	"time"
)

func worker(i int, c chan int) {
	//使用range读取信道里的消息
	for n := range c{
		fmt.Printf("position: %d, info chan: %c\n", i, n)
	}
}
func createWork(i int) chan<- int {
	c := make(chan int)
	go worker(i, c)
	return c
}

func main() {
	var channels [10]chan<- int
	//新建10个信道
	for i := 0; i < 10; i ++ {
		//创建协程,用来不断的读消息
		channels[i] = createWork(i)
	}
	for i := 0; i < 10; i++ {
		channels[i] <- 'A' + i
	}
	fmt.Println("------------小写--------")
	for i := 0; i < 10; i++ {
		channels[i] <- 'a' + i
	}
	time.Sleep(time.Millisecond)
}
//没有解决如何判断什么时候读取了
```

- 实现多并发,并实现用信道通知外面我已经完毕了,无需再用time.Sleep了
> 不要使用共享内存来通信,直接使用通信共享内存
```go
package main

import (
	"fmt"
)
type worker struct {
	in chan int
	done chan bool
}
func doWorker(i int, w worker) {
	//使用range读取信道里的消息
	for n := range w.in {
		fmt.Printf("position: %d, info chan: %c\n", i, n)
		//在此开一个go 协程,用于发消息
		go func() {
			w.done <- true
		}()
	}
}
func createWork(i int) worker {
	w := worker{
		in: make(chan int),
		done: make(chan bool),
	}
	go doWorker(i, w)
	return w
}

func main() {
	var workers [10] worker
	//新建10个信道
	for i := 0; i < 10; i ++ {
		//创建协程,用来不断的读消息
		workers[i] = createWork(i)
	}
	for i, worker := range workers {
		worker.in <- 'A' + i
	}
	fmt.Println("------------小写--------")
	for i, worker := range workers {
		worker.in <- 'a' + i
	}
	//上面一口气发完所有的数据.然后自己再处理done
	for _, worker := range workers {
		<- worker.done
		<- worker.done
	}
}

```

- 上面的代码改良版本
```go
package main

import (
	"fmt"
)
type worker struct {
	in chan int
	done chan bool
}
func doWorker(i int, w worker) {
	//使用range读取信道里的消息
	for n := range w.in {
		fmt.Printf("position: %d, info chan: %c\n", i, n)
		//在此开一个go 协程,用于发消息
		w.done <- true
	}
}
func createWork(i int) worker {
	w := worker{
		in: make(chan int),
		done: make(chan bool),
	}
	go doWorker(i, w)
	return w
}

func main() {
	var workers [10] worker
	//新建10个信道
	for i := 0; i < 10; i ++ {
		//创建协程,用来不断的读消息
		workers[i] = createWork(i)
	}
	//发消息
	for i, worker := range workers {
		worker.in <- 'A' + i
	}
	//马上处理done的消息
	for _, worker := range workers {
		<- worker.done
	}
	fmt.Println("------------小写--------")
	for i, worker := range workers {
		worker.in <- 'a' + i
	}
	//上面一口气发完所有的数据.然后自己再处理done
	for _, worker := range workers {
		<- worker.done
	}
}

```

- 使用waitGroup解决信道什么时候读完
```go
package main

import (
	"fmt"
	"sync"
)
type worker struct {
	in chan int
	done func()
}
func doWorker(i int, w worker) {
	//使用range读取信道里的消息
	for n := range w.in {
		fmt.Printf("position: %d, info chan: %c\n", i, n)
		//在此开一个go 协程,用于发消息
		w.done()
	}
}
func createWorker(i int, wg *sync.WaitGroup) worker {
	w := worker{
		in: make(chan int),
		done: func() {
			wg.Done()
		},
	}
	go doWorker(i, w)
	return w
}

func main() {
	var wg sync.WaitGroup
	var workers [10] worker
	//新建10个信道
	for i := 0; i < 10; i ++ {
		//创建协程,用来不断的读消息
		workers[i] = createWorker(i, &wg)
	}
	//声明一个系统提供一个waitGroup
	wg.Add(20) //添加多少个任务
	for i, worker := range workers {
	//	wg.Add(1)
		worker.in <- 'A' + i
	}
	fmt.Println("------------小写--------")
	for i, worker := range workers {
	//	wg.Add(1)
		worker.in <- 'a' + i
	}
	wg.Wait()//结束等待
}

```

### 导航
- [目录](../README.md)







