## 性能监控
为方便用户查看和掌握实例的运行信息，云数据库 MySQL 提供了丰富的性能监控项，用户可登录[云平台控制台][1]，点击导航条【关系型数据库】，进入[云数据库控制台][2]，【管理】-【实例监控】查看。

同时，可以在云监控中[MySQL监控数据接口](/document/api/248/11006)通过云API来获取CDB实例的监控指标。

## 支持监控的实例类型

云平台 MySQL 支持云数据库主实例及只读实例的监控，并为每个实例提供独立的监控视图供查询。

## 监控指标

云平台云监控为云数据库实例（MySQL）提供以下监控指标：

| 指标中文名 | 指标英文名 | 单位 |维度|指标说明|
|---------|---------|---------|---------|
|每秒执行操作数|qps|次/秒|实例维度|数据库每秒执行的SQL数（含insert、select、update、delete、replace），QPS指标主要体现CDB实例的实际处理能力|
|慢查询数|slow_queries|次/分|实例维度|[查看MySQL官方指导][3]|
|全表扫描数|select_scan|次/秒|实例维度|[查看MySQL官方指导][3]|
|查询数|select_count|次/秒|实例维度|Com_select值|
|更新数|com_update|次/秒|实例维度|[查看MySQL官方指导][3]|
|删除数|com_delete|次/秒|实例维度|[查看MySQL官方指导][3]|
|插入数|com_insert|次/秒|实例维度|[查看MySQL官方指导][3]|
|覆盖数|com_replace|次/秒|实例维度|[查看MySQL官方指导][3]|
|总请求数|queries|次/秒|实例维度|所有执行的SQL语句，包括set，show等|
|当前打开连接数|threads_connected|个|实例维度|[查看MySQL官方指导][3]|
|查询使用率|query_rate|%|实例维度|每秒执行操作数QPS/推荐每秒操作数|
|磁盘使用空间|real_capacity|MB|实例维度|仅包括MySQL数据目录，不含binlog、relaylog、undolog、errorlog、slowlog日志空间|
|磁盘占用空间|capacity|MB|实例维度|包括MySQL数据目录和binlog、relaylog、undolog、errorlog、slowlog日志空间|
|发送数据量|bytes_sent|MB/秒|实例维度|[查看MySQL官方指导][3]|
|接收数据量|bytes_received|MB/秒|实例维度|[查看MySQL官方指导][3]|
|容量使用率|volume_rate|%|实例维度|磁盘使用空间/实例购买空间|
|查询缓存命中率|qcache_hit_rate|%|实例维度|[查看MySQL官方指导][3]|
|查询缓存使用率|qcache_use_rate|%|实例维度|[查看MySQL官方指导][3]|
|等待表锁次数|table_locks_waited|次/秒|实例维度|[查看MySQL官方指导][3]|
|临时表数量|created_tmp_tables|次/秒|实例维度|[查看MySQL官方指导][3]|
|innodb缓存命中率|innodb_cache_hit_rate|%|实例维度|[查看MySQL官方指导][3]|
|innodb缓存使用率|innodb_cache_use_rate|%|实例维度|[查看MySQL官方指导][3]|
|innodb读磁盘数量|innodb_os_file_reads|次/秒|实例维度|[查看MySQL官方指导][3]|
|innodb写磁盘数量|innodb_os_file_writes|次/秒|实例维度|[查看MySQL官方指导][3]|
|innodb fsync数量|innodb_os_fsyncs|次/秒|实例维度|[查看MySQL官方指导][3]|
|myisam缓存命中率|key_cache_hit_rate|%|实例维度|[查看MySQL官方指导][3]|
|myisam缓存使用率|key_cache_use_rate|%|实例维度|[查看MySQL官方指导][3]|
|CPU占比|cpu_use_rate|%|实例维度|允许宿主机闲时超用，可能大于100%|
|内存占用|memory_use|MB|实例维度|允许宿主机闲时超用，可能大于购买容量|
|临时文件数量|created_tmp_files|次/秒|实例维度|[查看MySQL官方指导][3]|
|已经打开的表数|opened_tables|个|实例维度|[查看MySQL官方指导][3]|
|提交数|com_commit|次/秒|实例维度|[查看MySQL官方指导][3]|
|回滚数|com_rollback|次/秒|实例维度|[查看MySQL官方指导][3]|
|已创建的线程数|threads_created|个|实例维度|[查看MySQL官方指导][3]|
|运行的线程数|threads_running|个|实例维度|[查看MySQL官方指导][3]|
|最大连接数|max_connections|个|实例维度|[查看MySQL官方指导][3]|
|磁盘临时表数量|created_tmp_disk_tables|次/秒|实例维度|[查看MySQL官方指导][3]|
|读下一行请求数|handler_read_rnd_next|次/秒|实例维度|[查看MySQL官方指导][3]|
|内部回滚数|handler_rollback|次/秒|实例维度|[查看MySQL官方指导][3]|
|内部提交数|handler_commit|次/秒|实例维度|[查看MySQL官方指导][3]|
|InnoDB空页数|innodb_buffer_pool_pages_free|个|实例维度|[查看MySQL官方指导][3]|
|InnoDB空页数|innodb_buffer_pool_pages_total|个|实例维度|[查看MySQL官方指导][3]|
|InnoDB逻辑读|innodb_buffer_pool_read_requests|次/秒|实例维度|[查看MySQL官方指导][3]|
|InnoDB物理读|innodb_buffer_pool_reads|次/秒|实例维度|[查看MySQL官方指导][3]|
|InnoDB读取量|innodb_data_read|Byte/秒|实例维度|[查看MySQL官方指导][3]|
|InnoDB总读取量|innodb_data_reads|次/秒|实例维度|[查看MySQL官方指导][3]|
|InnoDB总写入量|innodb_data_writes|次/秒|实例维度|[查看MySQL官方指导][3]|
|InnoDB写入量|innodb_data_written|Byte/秒|实例维度|[查看MySQL官方指导][3]|
|InnoDB行删除量|innodb_rows_deleted|次/秒|实例维度| [查看MySQL官方指导][3]|
|InnoDB行插入量|innodb_rows_inserted|次/秒|实例维度|[查看MySQL官方指导][3]|
|InnoDB行更新量|innodb_rows_updated|次/秒|实例维度|[查看MySQL官方指导][3]|
|InnoDB行读取量|innodb_rows_read|次/秒|实例维度|[查看MySQL官方指导][3]|
|InnoDB平均获取行锁时间|innodb_row_lock_time_avg|毫秒|实例维度|[查看MySQL官方指导][3]|
|InnoDB等待行锁次数|innodb_row_lock_waits|次/秒|实例维度|[查看MySQL官方指导][3]|
|键缓存内未使用的块数量|key_blocks_unused|个|实例维度|[查看MySQL官方指导][3]|
|键缓存内使用的块数量|key_blocks_used|个|实例维度|[查看MySQL官方指导][3]|
|键缓存读取数据块次数|key_read_requests|次/秒|实例维度|[查看MySQL官方指导][3]|
|硬盘读取数据块次数|key_reads|次/秒|实例维度|[查看MySQL官方指导][3]|
|数据块写入键缓冲次数|key_write_requests|次/秒|实例维度|[查看MySQL官方指导][3]|
|数据块写入磁盘次数|key_writes|次/秒|实例维度|[查看MySQL官方指导][3]|
|主从不同步距离|master_slave_sync_distance|MB|实例维度|主从binlog差距|


有关更多如何使用云数据库监控指标的内容，可以查看云监控 API 中的[读取监控数据接口](/document/api/248/11006)。

> 更多监控指标，敬请期待。

[1]:	http://console.tcecqpoc.fsphere.cn/
[2]:	http://console.tcecqpoc.fsphere.cn/cdb/ "云数据库控制台"
[3]:	http://dev.mysql.com/doc/refman/5.6/en/ "查看MySQL官方指导"

