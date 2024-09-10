<details>
  <summary>1.	简述 slice 的底层原理，slice 和数组的区别是什么？</summary>

![image](https://github.com/user-attachments/assets/835337e7-7f65-47e1-becc-250e6dcaccc1)

</details>

<details>
  <summary>2.	简单介绍 GMP 模型以及该模型的优点：</summary>

![image](https://github.com/user-attachments/assets/137eb9d7-e547-4d3b-ba1a-ec4ec46e76e0)

</details>

<details>
  <summary>3.	简述 Golang 垃圾回收的机制：</summary>

![image](https://github.com/user-attachments/assets/3b8e4c33-7c84-48ad-a998-69fbb3af9501)

</details>

<details>
  <summary>4.	协程与进程、线程的区别是什么？协程有什么优势？</summary>

![image](https://github.com/user-attachments/assets/bed9f7be-3ad8-47d3-869e-3a572d70f791)

</details>

<details>
  <summary>5.	简述 defer 的执行顺序：</summary>

defer 的执行顺序是后进先出（LIFO），即最后定义的 defer 语句会最先执行

</details>

<details>
  <summary>6.	Golang 有哪些优缺点、错误处理有什么优缺点？</summary>

![image](https://github.com/user-attachments/assets/261e7879-d92e-4ee5-a2a3-983efe0869aa)

</details>

<details>
  <summary>7.	两次 GC 周期重叠会引发什么问题，GC 触发机制是什么样的？</summary>

![image](https://github.com/user-attachments/assets/7fbbf679-05ee-474f-9c8d-9d4cfbc9c9c5)

</details>

<details>
  <summary>8.	Golang 的协程通信方式有哪些？</summary>

Goroutine 之间的通信 主要通过 Channel 实现，Channel 是 Go 中用于在多个 Goroutine 之间传递数据的同步机制。Channel 可以是无缓冲或有缓冲的。
其他方式包括使用共享内存，但通常建议通过 Channel 进行协程间通信以避免竞争条件。

</details>

<details>
  <summary>9.	简述 Golang 的伪抢占式调度：</summary>

伪抢占式调度 是指 Go 的调度器不会直接中断正在运行的 Goroutine，而是依赖在特定点（如函数调用、系统调用等）进行调度检查。
如果 Goroutine 运行时间过长，Go runtime 会在这些检查点上将 Goroutine 挂起，并调度其他 Goroutine。

</details>

<details>
  <summary>10. 什么是 Goroutine 泄漏：</summary>

Goroutine 泄漏 是指 Goroutine 启动后没有正常退出且无法被回收，占用内存或系统资源。
这通常是由于 Channel 没有关闭，或 Goroutine 一直在等待某些永远不会发生的事件。

</details>

<details>
  <summary>11. Goroutine 什么时候会被挂起？</summary>
  
![image](https://github.com/user-attachments/assets/9d9bcead-895f-4933-9a70-da507f3482b3)

</details>
