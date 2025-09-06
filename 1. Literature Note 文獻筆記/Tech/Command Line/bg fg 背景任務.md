---
tags: []
date: 2024-05-09
time: 11:05
---
參考
- [OREILLY Job Control](https://www.oreilly.com/library/view/mac-os-x/0596003706/ch21s08.html)
- [bg和fg指令（整理）以及 Linux中Ctrl+C、Ctrl+D等按键操作&进程相关命令](https://blog.csdn.net/deniece1/article/details/102770363)

如果在跑一個要執行很久的指令，可以先：
1. `ctrl-z` 這會暫停該指令
2. `bg` 把該暫停的指令調到背景**繼續執行**
3. `fg` 可以把該執行中的指令調回前台


若一開始執行時，就想讓他在背景執行的話，在尾端加上`&`
```shell
command ping -i 5 google.com &

sleep 10 &
```





# Job Control

Job control lets you place foreground jobs in the background, bring background jobs to the foreground, or suspend (temporarily stop) running jobs. _tcsh_ provides the following commands for job control. For more information on these commands, see [Section 21.9](https://www.oreilly.com/library/view/mac-os-x/0596003706/ch21s09.html "Built-in tcsh Commands").

`bg`

Put a job in the background.

`fg`

Put a job in the foreground.

`jobs`

List active jobs.

`kill`

Terminate a job.

`notify`

Notify when a background job finishes.

`stop`

Suspend a background job.

`Ctrl-Z`

Suspend the foreground job.

Many job control commands take _jobID_ as an argument. This argument can be specified as follows:

`%` _`n`_

Job number _n_.

`%` _`s`_

Job whose command line starts with string _s_.

`%?` _`s`_

Job whose command line contains string _s_.

`%%`

Current job.

`%`

Current job (same as preceding).

`%+`

Current job (same as preceding).

`%-`

Previous job.