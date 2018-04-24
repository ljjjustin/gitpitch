# Online Debug

工作交接

---

### Agenda

- 调试工具
  * pdb
  * tcpdump
  * lsof
  * strace

---
### pdb
- 前提
  * 熟悉项目的源代码
  * 结合日志进行定位

- 设置断点
  * 考虑线上部署架构
  * 考虑进程数目

---
### gdb
- 功能
  * 调试已经启动的程序
  * 动态的修改程序的参数和行为

- 适用条件
  * 底层使用C语言实现的程序

---
### tcpdump

- 功能
  * 抓包
  * 分析异常网络流量

- 试用环境
  * 所有linux/unix系统

- 不方便的地方
  * 流量大，需要很多过滤条件才能找到关注的包
  * 升级版：[tracedump](http://mutrics.iitis.pl/)

---
### lsof

- 功能
  * 列举文件描述符
  * 强大的过滤
    - 按进程
    - 按用户
    - 按类型：TCP、UDP。。
    - 按端口
- 有趣的应用
  - 恢复以删除的文件

---
### strace
- 功能
  * 统计和跟踪应用程序的系统调用
  * 了解程序的运行原理和实际运行状态
  * 强大的过滤条件
    - file, network, ipc, signal, memory

- 适用条件
  * 所有支持ptrace的操作系统

---
### htop
- 功能
  * 功能更强大的top
  * 可以和strace、lsof、kill结合起来

---
### dstat
- 功能
  * 查看系统的各项性能指标

---
### iostat
- 功能
  * I/O之系统的监控工具

---
### Thanks!
