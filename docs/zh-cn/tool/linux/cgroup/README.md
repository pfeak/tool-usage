# CGroup

&emsp;&emsp;cgroup 的全称为 control group，中文翻译为“控制组”。主要用于控制进程组对某种资源的使用，这些资源包括但不限于：内存、CPU、I/O 和 网络 等。

&emsp;&emsp;2006 年，Google 工程师在开源社区发起了一个用来管理和限制进程资源使用的项目，名为“process containers”，2007 年，Linux 内核团队将其改名为 cgroup 纳入到 Linux 内核 feature 项目中。在 2008 年 1 月发布的 Linux 2.6.24，这一功能被合并到了内核中。到 Linux 4.5 版本内核，CGroup v2 被合并到内核，这是一次在使用方式上的重大更新。

&emsp;&emsp;docker、k8s 资源控制也是依赖这个机制。