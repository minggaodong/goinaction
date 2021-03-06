# Chapter7

## runner
runner 包用于展示如何使用通道来监视程序的执行时间，如果程序运行时间太长，也可以用 runner 包来终止程序。
当开发需要调度后台处理任务的程序的时候，这种模式会很有用。
示例：`chapter7/sample/runner`

## pool
pool 包用于展示如何使用有缓冲的通道实现资源池，来管理可以在任意数量的goroutine之间共享及独立使用的资源。
这种模式在需要共享一组静态资源的情况(如共享数据库连接或者内存缓冲区)下非常有用。
如果goroutine需要从池里得到这些资源中的一个，它可以从池里申请，使用完后归还到资源池里。
示例：`chapter7/sample/pool`

## work
work 包的目的是展示如何使用无缓冲的通道来创建一个 goroutine 池，这些 goroutine 执行并控制一组工作，
让其并发执行。在这种情况下，使用无缓冲的通道要比随意指定一个缓冲区大小的有缓冲的通道好，
因为这个情况下既不需要一个工作队列，也不需要一组 goroutine 配合执行。无缓冲的通道保证两个 goroutine 之间的数据交换。
这种使用无缓冲的通道的方法允许使用者知道什么时候 goroutine 池正在执行工作，而且如果池里的所有 goroutine 都忙，
无法接受新的工作的时候，也能及时通过通道来通知调用者。使用无缓冲的通道不会有工作在队列里丢失或者卡住，所有工作都会被处理。

## 总结
- 可以使用通道来控制程序的生命周期
- **带 default 分支的 select 语句可以用来尝试向通道发送或者接收数据，而不会阻塞。**
- 有缓冲的通道可以用来管理一组可复用的资源。
- 语言运行时会处理好通道的协作和同步。
- 使用无缓冲的通道来创建完成工作的 goroutine 池。
- 任何时间都可以用无缓冲的通道来让两个 goroutine 交换数据，在通道操作完成时一定保证对方接收到了数据。
