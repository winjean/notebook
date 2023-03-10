#distributed transaction

##ACID 
Atomic原子性，Consistency一致性，Isolation隔离性，Durability持久性

###A是原子性(atomic)：
事务中包含的各项操作必须全部成功执行或者全部不执行。
任何一项操作失败，将导致整个事务失败，
其他已经执行的任务所做的数据操作都将被撤销，
只有所有的操作全部成功，整个事务才算是成功完成。  
  
###C是一致性(consistent)：
保证了当事务结束后，系统状态是一致的。
那么什么是一致的系统状态？
例如，如果银行始终遵循着"银行账号必须保持正态平衡"的原则，
那么银行系统的状态就是一致的。
上面的转账例子中，在取钱的过程中，账户会出现负态平衡，
在事务结束之后，系统又回到一致的状态。
这样，系统的状态对于客户来说，始终是一致的。  
  
###I是隔离性(isolated)：
并发执行的事务，彼此无法看到对方的中间状态。
保证了并发执行的事务顺序执行，而不会导致系统状态不一致。
    
###D是持久性(durable)：
保证了事务完成后所作的改动，即使是发生灾难性的失败都会被持久化。
可恢复性资源保存了一份事务日志，如果资源发生故障，可以通过日志来将数据重建起来。  

##CAP理论 zipkin.md
一致性Consistency，可用性Availability，分区容错性Partition tolerance，
分布式系统来说，CAP只能满足其中2条,P是不能放弃的

###C（Consistency）一致性：
分布式数据库的数据保持一致

###A（Availability）可用性：
任何一个节点挂了，其他节点可以继续对外提供服务

###P（Partition tolerance）分区容错性（网络分区）：
一个数据库所在的机器坏了，如硬盘坏了，数据丢失了，
可以新增一台机器，然后从其他正常的机器把备份的数据同步过来.  

##BASE 理论
Basically Available（基本可用），Soft state（软状态），Eventually Consistent（最终一致性）

###BA（Basically Available）基本可用：
在分布式系统出现故障时，允许损失部分可用性（服务降级、页面降级）。
比如系统挂了，在页面上给个提示啥的

###S（Soft state）软状态：
允许分布式系统出现中间状态。而且中间状态不影响系统的可用性。
这里的中间状态是指不同的数据复制data replication之间的数据更新可以出现延时的最终一致性。

###E（Eventually Consistent）最终一致性：
数据复制data replications经过一段时间达到一致性。