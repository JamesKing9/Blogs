# TOC

[TOC]

---





# Git flow

Git flow是广泛采用的一种工作流程

![Git flow](C:\Users\Administrator\Pictures\Git flow.jpg)

主要特点有两个：

1. 首先，项目存在两个长期分支：

- 主分支master
- 开发分支dev

前者用于存放对外发布的版本，任何时候在这个分支拿到的，都是稳定的分布版；后者用于日常开发，存放最新的开发版。

2. 其次，项目存在三种短期分支

- 功能分支（feature branch）
- 补丁分支（hotfix branch）
- 预发分支（release branch）

## 实践

正如我们在介绍 Git flow 介绍的，master 分支只是用于产品的发布，在平时的开发中是不会使用它的，而只会使用 dev分支，但是如果我们有了新的功能，一般是会在 dev分支 中在创建一条该功能的分支，所以我们应该这样做。

**创建dev、feature-1分支，并且我们需要转到feature-1分支上**

在 Android Studio 中，我们可以很方便的管理分支，在主界面的右下角，点击Git可以出现当前的分支，默认为 master，我们选中 New Branch，如下图所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4S6QeBelPjU8jMIicxSVjEejLQa7R01nl1Vto4XPxxicTNk3pQv3jyGJjA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

在弹出的对话框中我们输入 feature-1，点击OK，这样我们不仅新建了 feature-1 分支，并且正处于该分支中，接下来按照同样的方法创建dev分支，如果不出意外的话，我们现在应该是处于dev分支上，但是因为我们现在要开发功能1，所以必须转换到feature-1分支上，按照下图的操作，我们能够回到feature-1分支上。

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4S3Qqzf3YgsO37SRrbKFoHg3botPicWlBBEpemaibmO7K0FetDyib0RibrZA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

接下来打开Log，我们应该能够看到如下的情景：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4S0btI8lqdlxxDhRqOHaj8icUqrhmjCe1LFib6rvxIRaYwK7B5LSs8VaMA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

可以看到我们现在有三个分支：master、dev、feature-1，但是AS提示我们应该有四条分支，其实HEAD就是当前活跃分支的游标。形象的记忆就是：你现在在哪儿，HEAD 就指向哪儿，所以 Git 才知道你在那儿！不过 HEAD 并非只能指向分支的最顶端，实际上它可以指向任何一个节点，它就是 Git 内部用来追踪当前位置的标记。我们可以使用下面的图来演示当前分支的情况：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SZvDdqNmpicoYbpVQPyaUxFFPN4O6OIDicwEYM3umxQBibUWDNLQDLs7Yw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

**完成功能1**

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SdasMQCoI0jNbfsP3aRJGx6hKt2n9qufxtO00hBvviblic3UCbrK7iaCRA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

好了，功能1 编写完成，那么就提交吧！老方法：Ctrl+K 进行提交，按照下图填写提交信息，每一次的提交信息最好能够详细并且格式规范，这样以后再查看Log的时候就会比较方便。

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4Sg6nK66EJrGlCjibicLebDXeiatuMUXVZ9p7HZhicAxgQ3vgkVeBxSVdicPw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

点击Commit按钮提交完毕之后，可以看到现在的log图变成了下图：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SiaDXPaYFicdibdRkyOGDFSkKvFxyadBkeL8wTyzbwKnBoj3IOFzhsqfwg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

我们可以打开Log图的右侧，他列出了目前正在被Git跟踪的所有文件，我们选中MainActivity.java，点击上边的第二个按钮Show Diff(显示差异)：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4S5RAlZ7K5obnQC4EeCtrqEYzgjqxGDdsR8PGOxscBAxEiaoAsvsFgYNA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

在弹出的界面中可以显示该文件的 当前版本 和 master分支 中的该文件的差异，我们可以使用Esc快捷键退出该界面，如下图所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SicfF3T8eticFsvPslDAob7emGudBibIF46mj69zBCyXSIcUu346s8ueiag/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)



**将feature-1分支合并到dev分支上**

如下图所示，选中dev分支并选择checkout：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SA5YJZPNc2Qf49BzOOWMKHtaV4j7du4eoP3teRO6ic9zUazXeZMRg1QA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

你会发现现在代码回到了最开始的状态，现在选中 feature-1 分支并选中 merge，准备将 feature-1 分支合并到 dev 分支上：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SrDZDndj7lovcPTcaWI10qAhxuryLPkqx9QC7YX9ORhrZ91ibu65Zacw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

再来重新看一下Log图，他长下面这样，可以看到现在feature-1分支已经与dev分支合并，并且现在他们是处于同一状态的：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SDEP7yz0X60zUX7RiaaJBqOl2icspmlEnBftF4UousEzTgHcNEHWcVhCA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

最后的最后，我们需要删除已经完成任务的feature-1分支，以免分支过多管理混乱。

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SbQWgrOibfOic3qCdWqJdXwjicbdHNn3qBsrbKPstL63lRhTGicjib3opzCw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)



## 重点来了

首先我们继续增加 feature-2 与 feature-3（跟 feature-1 一样，这里就不赘述）。但是老板说了，新开发的**功能3**不喜欢，需要删除了功能3，咋办呢？

这里就需要讲到Git的回退了，在 Android Studio中提供了两种回退的方式：Git revert 以及 Git reset。

**Git revert**

Git revert 可以将版本回退到上一步，但是会新增一个提交，他的流程就像下面这幅图一样：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SeFwPsGHUoYhCOYDzkQmRGhQ7EyTx0icCMY4ib75PsrQn5FxL9JSLVJCg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

1. 首先打开Log，找到功能3的提交，右键选择复制哈希码(Copy Revision Number)，如下图所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SA6jkITZlyZwiaAP0f30razv3l3M9BJw9wFtRcibiciaiczjMCm2QC3Moibug/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

**2. **打开Android Studio的终端Terminal，他就在Version Control的旁边，之后输入以下命令按回车键：

```
//很复杂的数字字母就是我们刚才复制的哈希码
git revert 9c834d8c66598fb132a0cc8e4c1f8c341d058f3e
```

如下图所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SwuIldZlAxCkRiapk7uZ7c26FG34bPsibgLZgC6TeS6KQDO7opKaluTkA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

**3. **之后终端会列出此次提交的具体信息，如果确认要回退，请输入 **:q** 保存此次操作并且退出会话

现在你可以看到，他确实增加了一次提交，并且回到了上一版的内容，Log应该是这样的：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SuHrY35d1pibPCo5PrhicHt4MBNuF5kAh4m5tpIjwRLPKtxMtHmicjfhSg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

**Git reset**

相比之下，Git reset 就要干脆的多，与 Git revert 的功能一样，它也可以将代码恢复到上一个版本，但是不会新增一次提交，他的流程如下：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4S7HguMpuzEeCznbtpDeGAoGfE3Il5ibf9iaDzDmtcia2KohS6SMOx03MrQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

因为我们需要删除 功能3，并且让Log看起来并没有 revert 的这一次提交，所以我们应该在dev分支上**后退两步**，确实是这样的对吧！



**1. **点击菜单栏上的 VCS-->Git-->Reset HEAD，打开对话框，在 To Commit 文本框中输入 HEAD~2，就像下图这样：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4Ssibm5ibQ3riccrAficxiav9691q588Ntx8dN1Ml9Ks0BAfFVYtwTczqSReQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SBicLbqhJATGc2dwr44tKiaYxa9V07YDowlKVVia6WpWeEFz68dhlo67Uw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

**2.** 点击Reset按钮之后，你可以发现Log变了，变回原来那个熟悉的画面了：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SxRrPkN6Om1YyHUJnrRJFN6FibZibKVicZfspLWe1NPnhjNkf9ARg03aVw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

master分支被修改

突然你发现你的同事在 master 分支上提交了两次，分别是增加了 功能1 和 功能4，但是其中的 功能1 很显然 HelloWorld 被写成了 WorldHello，例如这样的：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4S9KO5LeupjViblZxJBQ1jXTc1k2xRjLPthRRCYC7Ad0vZvGLNsd0Oaiaw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

提交更改，之后Log应该是这样的：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SGKyz6WIY30jLRW0aXicgPDvBJLj7LQQiafo67aFMl8lCsmyiawk38trnA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

我们依旧用演示图表示当前分支的发展情况：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SCicHLPlOhwogsj4qotBHoYv1DmaObKKfuITBX1V28Dbh58OYIjwJa3w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

Rebase

老板说了，master 分支只要 功能4 不需要 功能1，而 dev 分支上的 功能1、2 全部都要合并到 master 分支上。那么这个时候我们就可以使用 rebase 了。

git rebase 用于把一个分支的修改合并到当前分支。现在我们切换到 master 分支，将 dev 上的做修改加入到 master 中，所以我们选择 rebase，在Android Studio中提供了功能十分强大的rebase。

**1. **点击菜单栏上的VCS–>Git–>Rebase，如下图所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SLXXdicLXNc6Yv6gdjwa3dw4GeWzDWrnZq7iaz6thWRs0zibq6Zj23PeZw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

**2. **在弹出的对话框中，我们在Onto的下拉栏中选中dev分支，表示我们需要将master分支rebase到该分支下

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SdZXcnjJuIlu1sycex1GbGgLt0c6xLIxcHqvzBcoMTXtgR35aibm83fA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

**3. **点击Rebase之后，你会发现Android Studio弹出对话框，显示master分支的两次提交，需要我们做出选择，如下图所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SibatNOFCegmM6haUJB4NicAQjSDejSlvnUbJRicAczbEsGxGFiaibYeOibJw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

**4. **因为我们不需要master分支上的 功能1 但是需要 功能4，所以在 功能1 的提交上我们选择 skip(跳过这个提交)，在 提交4 上选择 pick(挑选此次这个提交)，点击 Start Rebasing，我们可以看到又有对话框弹出，此次是让我们对每个文件进行挑选，如下图所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SibSLaUHTUI6Hphyn8wdjoVvlF38JUjyMU52kW89UW470L4op3slFLYQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

**5. **对于每一个文件，你可以选择接受你的那一部分，或者接受另一只分支上的内容，又或者你可以点击Merge对文件进行筛选。我们点击Merge按钮，可以看到有三个文件呈现在屏幕上。其中中间的文件是最后的结果，左边的为当前分支master分支，右边的为dev分支，你还可以发现在修改过的每一行中都存在一个X >>符号，点击X表示不需要这一行的修改，点击>>表示接受这一行的修改，我们甚至还可以像在编辑器中那样复制、粘贴、编辑内容，我们最终作出的选择如下图所示，之后可以点击Apply进行保存，如果你不想保存，那就点击Abort终止此次修改：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4StXjHEX2of9YK9kgCtfHMJzb07EQa08EkvMzuGcGoL3KDpJ67pykVqg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

**6. **对于剩下的两个文件也做相同的处理，之后我们可以看到master分支已经有了dev分支的功能1和功能2和自身的功能4，并且去掉了自己之前的功能1，可以看一下Log，如下所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4S9EwwICC0q3kvm5LVLibyz7KCOPqKHpMHrE3VeN3EnXSWuJR5ibj8eEoQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

我们依旧使用演示图来表示最后的分支情况：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SibM0RBvcicW3hibj0yroQXR2rQYQ89KtVSgSKnCsibLh8eSTJZxMrNnxlw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

推送到远程仓库

推送很简单，你可以导航到菜单栏 VCS-->Import Into Version Control -->Share Project on Github，如下图所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SjjHwwswYyo7rXsJ4mewDjc2QKJTcrQp0W3BBqdnGShEdVOQ8ic3sN6A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

在弹出的对话框中填写远程仓库的名称，点击Share：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SxCicrm8l2Ow00ouLyXXdTDWJmibB4vaAChwrRlQBoaRhnwHOAyAMmhcQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

之后你就可以在你的Github上面看到这一次的推送了。

本地修改同步到远程仓库

现在我需要在工程中加入一些文件，例如说我新建了一个 screenshots 文件夹，并在其中添加了这篇文章需要用到的截图，那么如何将这些文件一起同步到远程仓库呢？其实很简单。

**1. **使用快捷键 **Alt+9** 或者点击工具按钮打开 Version Control，右键Unversioned Files，选择Git-->Add，将所有文件加入Git中，如下图：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4S8icISV079vX2O4SJb9NJWHSRP7DlFcpXFNRiasr3pro8Q0U7xOVHtcEg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

**2. **右键Default，选择Commit所有的文件之后填写提交信息，如下图：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4Sg7z5zP5xX7MxFVmPSCDoUVVPxxhJHataokqwRCoXABDicYy2eCQa8Uw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

**3. **使用快捷键 Ctrl+Shift+K 或者右键工程根目录，选择push项目，如下图所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4S8Xe2a8EqVJvpgkOJyiahVf3xdgiboX3IKIfuPVSVBrvEYiaxq5sTKc24A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

**4. **在弹出的对话框中点击Push按钮，就可以将所做的修改同步到远程仓库了，如下图：

![img](https://mmbiz.qpic.cn/mmbiz_png/v1LbPPWiaSt7WVLSZmribQCtVzpnhMbic4SutUbicJRmp8SLNF1OdyvJ4NV82XOCJ4dhvFpOzPdPjltnplWexpOBaQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

**5. **对于修改过的文件想要同步到远程仓库，按照同样的步骤就行了，这里不再赘述了。