<details>
  <summary>1. 执行一条 select 语句，期间发生了什么？</summary>

MySQL 的架构共分为两层:Server 层负责建立连接、分析和执行 SQL;存储引擎层负责数据的存储和提取。支持 InnoDB、MyISAM.

  ![image](https://github.com/user-attachments/assets/c1747949-e352-4c6f-b375-1f544568d0ac)

</details>

<details>
  <summary>2. InnoDB 行格式有哪些？</summary>

![image](https://github.com/user-attachments/assets/ee4169b5-1c09-4f4c-9a2f-0fb81a91f336)
「变长字段长度列表」中的信息之所以要逆序存放，是因为这样可以使得位置靠前的记录的真实数据和数据对应的字段长度信息可以同时在一个 CPU Cache Line 中，这样就可以提高 CPU Cache 的命中率。

</details>

<details>
  <summary>3. MySQL索引有哪些？</summary>

![image](https://github.com/user-attachments/assets/6d7a45d2-105b-4108-a9ce-6d3ae431470b)

</details>

<details>
  <summary>4. 什么时候需要 / 不需要创建索引？</summary>

![image](https://github.com/user-attachments/assets/0e8ce04a-3d19-46c0-9385-6c8146c4e214)

</details>

<details>
  <summary>5. 有什么优化索引的方法？</summary>

- 前缀索引优化；
- 覆盖索引优化；
- 主键索引最好是自增的；（非自增：页分裂。页分裂还有可能会造成大量的内存碎片，导致索引结构不紧凑，从而影响查询效率。）
- 防止索引失效；

</details>

<details>
  <summary>6. 事务有哪些特性？</summary>

- 持久性是通过 redo log （重做日志）来保证的；
- 原子性是通过 undo log（回滚日志） 来保证的；
- 隔离性是通过 MVCC（多版本并发控制） 或锁机制来保证的；
- 一致性则是通过持久性+原子性+隔离性来保证；

</details>

<details>
  <summary>7. 并行事务会引发什么问题？</summary>

- 脏读：如果一个事务「读到」了另一个「未提交事务修改过的数据」，就意味着发生了「脏读」现象。
- 不可重复读：在一个事务内多次读取同一个数据，如果出现前后两次读到的数据不一样的情况，就意味着发生了「不可重复读」现象。
- 幻读：在一个事务内多次查询某个符合查询条件的「记录数量」，如果出现前后两次查询到的记录数量不一样的情况，就意味着发生了「幻读」现象。

</details>

<details>
  <summary>8. 事务的隔离级别有哪些？</summary>

- 读未提交（read uncommitted），指一个事务还没提交时，它做的变更就能被其他事务看到；
- 读提交（read committed），指一个事务提交之后，它做的变更才能被其他事务看到；
- 可重复读（repeatable read），指一个事务执行过程中看到的数据，一直跟这个事务启动时看到的数据是一致的，MySQL InnoDB 引擎的默认隔离级别；
- 串行化（serializable ）；会对记录加上读写锁，在多个事务对这条记录进行读写操作时，如果发生了读写冲突的时候，后访问的事务必须等前一个事务执行完成，才能继续执行；
![image](https://github.com/user-attachments/assets/65b1ed1d-1dc8-4b69-ab3b-9e9d364a2272)

</details>

<details>
  <summary>8. Read View 在 MVCC 里如何工作的？</summary>

![image](https://github.com/user-attachments/assets/cc660ff3-c0da-49e1-ae3b-5b37f9bbb824)

</details>

<details>
  <summary>9. 可重复读和读提交工作原理？</summary>

- 「读提交」隔离级别是在每个 select 都会生成一个新的 Read View，也意味着，事务期间的多次读取同一条数据，前后两次读的数据可能会出现不一致，因为可能这期间另外一个事务修改了该记录，并提交了事务。
- 「可重复读」隔离级别是启动事务时生成一个 Read View，然后整个事务期间都在用这个 Read View，这样就保证了在事务期间读到的数据都是事务启动前的记录。

</details>

<details>
  <summary>10. mysql有哪些锁？</summary>

![image](https://github.com/user-attachments/assets/6da011c0-63a8-4f14-9c94-23b311babf17)

</details>

<details>
  <summary>11. mysql如何加锁？</summary>

![image](https://github.com/user-attachments/assets/adf69eb0-a476-4cc4-8625-41195a1e6abf)
![image](https://github.com/user-attachments/assets/0533c88f-a47a-48b7-9054-16101dbc6439)

</details>

<details>
  <summary>12. 简述 RPC 的调用过程</summary>

- 客户端调用本地代理（Stub）：客户端程序调用本地的代理方法，代理方法负责封装远程调用的参数。
- 序列化请求：本地代理将参数序列化为网络可传输的格式。
- 发送请求：代理将序列化后的数据通过网络协议发送给远程服务器。
- 服务器接收并反序列化：服务器端的代理收到请求并将其反序列化为实际参数。
- 服务器调用实际服务：服务器端代理调用实际的服务函数，完成业务逻辑。
- 序列化返回值：服务函数完成后，将返回值序列化。
- 服务器发送响应：服务器代理通过网络将返回值传回客户端。
- 客户端反序列化并继续执行：客户端收到响应，代理函数将其反序列化为可用格式，返回给客户端程序。

</details>
