![git_logo](F:\蒙特卡罗工作\研究生毕业论文\辐照损伤软件开发\Algorithms\figures\git_logo.png)

![](https://github.com/edj19/Algorithms/blob/master/figures/git_logo.png)

# Git教程

## Git介绍

Git是目前世界上最先进的分布式版本控制系统

### Git安装（installation)

**Linux上安装Git**

```go
sudo apt-get install git
```

**Windows安装Git**

直接从Git官网下载安装程序，然后按默认选项安装即可。当我们安装完成后，还需要最后一步设置，在任意目录下*Git bash Here*在命令行输入：

```
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

通过上述语句输入你的名字和Email地址。

## 基本命令

### 基本操作

创建*版本库*，版本库又名仓库，我们可以理解为一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以跟踪历史，或者在将来某个时刻可以“还原”。

* 接下来在一个合适的地方，创建一个空目录：

```
mkdir algorithms
cd algorithms
pwd
```

* 通过**git init**命令把这个目录变成Git可以管理的仓库：

```
git init
>>>Initialize empty Git repository in ....
```

通过上面的命令我们创建了一个空的仓库，可以发现当前目录下多了一个**.git**的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然Git仓库就破坏了。

* 文件添加到版本库

接下来我们编写一个文件或者脚本，比如一个markdown文件**notes.md**，具体内容如下：

```
Git is a version control system.
This is the first note
```

接下来我们利用命令**git add**将文件添加到仓库：

```
git add notes.md
```

然后利用命令**git commit**告诉Git，把文件提交到仓库：

```
git commit -m "write a notes file"
```

上面语句**-m**后面输入的是本次提交的说明，可以输入任意内容，还要注意**commit**可以一次性提交很多文件，所以我们可以多次**add**不同的文件。

* 状态查看

接下来我们再修改一下*notes.md*文件，修改内容如下：

```
Git is a version control system.
This is the first note.
This is the second note.
```

接下来我们可通过**git status**命令查看结果：

```
git status
```

上述命令可以时刻掌握仓库当前的状态，通过运行上述命令我们可知，*notes.md*文件被修改了，但是还没准备提交修改。此外如果想查看具体修改了什么内容，可以通过**git diff**命令查看：

```
git diff notes.md
```

修改完后就可以提交到仓库了，提交修改和提交新文件都是一样的，第一步**git add**:

```
git add notes.md
```

在第二步**git commit**之前，可通过**git status**查看当前仓库的状态：

```
git status
```

接下来我们就可以放心提交了：

```
git commit -m "add second note"
```

提交后我们可以再次使用**git status**命令查看仓库的当前状态，Git告诉我们当前没有需要提交的修改，而且工作目录是干净的。

* 版本回退

在实际工作中，我们可以通过**git log**命令查看版本控制系统的历史记录：

```
git log
```

上述命令显示从最近到最远的提交日志，我们也可以加入**--pretty=oneline**参数来简化日志：

```
git log --pretty=oneline
```

如果现在我们想把*notes.md*文件回退到上一个版本，该如何做呢？首先我们需要明确在Git中，用**HEAD**表示当前版本，上一个版本就是**HEAD^**，上上一个版本就是**HEAD^^**，当然往上100个版本写个100个**^**比较容易写不出来，可以写为**HEAD~100**。

通过**git reset**命令进行回退：

```
git reset --hard HEAD^
```

通过**git log**命令可以发现最新的版本已经不见了，那如果想回去该咋办呢？我们可以通过找到最新的版本的**commit id**为*cf890.....*，于是就可以指定回到未来的某个版本：

```
git reset --hard cf890
```

如果找不到最新版本的id，Git可以利用**git reflog**用来记录你的每一次命令：

```
git reflog
```

通过上述命令你就可以找到**commit id**了。

### 属性查看

当我们安装配置之后，有时候需要查看当前配置的相关情况，可使用下面的命令：

1. 查看本地Git的用户名和邮箱

```
git config user.name  # 用户名
git config user.email # 邮箱
```

2. 查看global类型的配置情况

```
git config --global --list
```

3. 如果你想切换用户，则还是可以通过设定用户名和邮箱的方式进行修改

```
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

### 版本操作

工作区有一个隐藏目录**.git**叫做Git的版本库，这里存了很多东西，其中最重要的称为**stage(或index)**的暂存区，还有Git为我们自动创建的第一个分支**master**，以及指向**master**的一个指针叫做**HEAD**。相应的图示如下图所示：

![](https://github.com/edj19/Algorithms/blob/master/figures/git_版本库.jpg)

![git_版本库](F:\蒙特卡罗工作\研究生毕业论文\辐照损伤软件开发\Algorithms\figures\git_版本库.jpg)

则将文件往Git版本库添加时，分两步执行：

1. 第一步用**git add**把文件添加进去，实际上就是把文件修改提交到暂存区；
2. 第二步是用**git commit**提交修改，实际上就是把暂存区的所有内容提交到当前分支。

注：因为我们创建Gir版本库时，Git自动为我们创建了唯一一个**master**分支，现在的**git commit**就是往**master**分支上提交更改。在我们每次修改后，如果不用**git add**到暂存区，那就不会加入到**commit**中。

* 撤销修改

当我们修改文件后，在没提交前，如果想删除不需要的文件，就可以直接进行删除后，利用**git status**查看，可以利用**git checkout -- file**在工作区的修改全部撤销，有两种情况：

1. 一种是*notes.md*自修改后就没有被放在暂存区，现在撤销修改就回到和版本一模一样的状态；
2. 一种是*notes.md*已经添加到暂存区后，又做了修改，现在撤销修改就回到添加到暂存区后的状态。

总之就是让这个文件回到最近一次**git commit**或**git add**时的状态。

注：**git checkout -- file**命令中的**--**很重要，没有**--**就变成了“切换到另一个分支”的命令，后面分支管理会介绍。

如果你现在修改后已经通过**git add**到暂存区该咋办呢？利用**git status**查看后，Git告诉我们可以利用**git reset HEAD <file>**把暂存区的修改撤销掉(unstage)，重新放回工作区：

```
git reset HEAD notes.md
```

接下来利用命令**git checkout -- notes,md**丢弃对工作区的修改，这样就完成了。

* 删除文件

当我们添加一个新文件到Git并且提交后，如果想删除文件直接在文件管理器中把没用的文件删除或者用**rm**命令进行删除，此时工作区和版本库就不一致了，然后利用命令**git rm**删除，并且**git commit**后，文件就从版本库删除了！

```
git rm test.txt
git commit -m "remove test.txt"
```

### 远程仓库

注册Github账户，就可以免费获得Git远程仓库，然而由于本地Git仓库和Github仓库之间的传输通过SSH加密的，因此需要设置：

第一步：创建SSH Key

```
ssh-keygen -t rsa -C "youremail@example.com"
```

接下来一路回车，使用默认值即可，一切完成后就在用户主目录下有个**.ssh**目录，里面有**id_rsa**和**id_rsa.pub**两个文件，这两个就是SSH Key的秘钥对。

第二步：登陆Github，打开“Account settings","SSH Keys"页面，然后点”**Add SSH Key**"，填上任意Title，在Key文本框里粘贴**id_rsa.pub**文件的内容，这样就可以在GitHub上免费托管的Git仓库。

注：GitHub允许添加多个Key

* 添加远程库

通过上面的步骤在本地创建了一个Git仓库后，又在GitHub创建了一个Git仓库，并且让这两个仓库进行远程同步，这样GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作，真是一举两得。

首先，登陆GitHub，在右上角找到“Create a new repo"按钮，创建一个新的仓库：

![](https://github.com/edj19/Algorithms/blob/master/figures/gitthub01.jpg)



![github01](F:\蒙特卡罗工作\研究生毕业论文\辐照损伤软件开发\Algorithms\figures\github01.jpg)

填入Repository name，其他保持默认设置，点击“Create repository"，就成功创建了一个新的Git仓库：

![](https://github.com/edj19/Algorithms/blob/master/figures/github02.jpg)

![github02](F:\蒙特卡罗工作\研究生毕业论文\辐照损伤软件开发\Algorithms\figures\github02.jpg)

通过上面的信息GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后把本地仓库的内容推送到GitHub仓库。

通过上面的显示，在本地仓库运行下面的命令：

```
git remote add origin https://github.com/edj19/Algorithms.git
```

添加后，远程库的名字就是**origin**，这是Git默认的叫法，接下来就可以把本地库的所有内容推送到远程库上：

```
git push -u origin master
```

把本地库的内容推送到远程，用**git push**命令，实际上就是把当前分支**master**推送到远程。

注：由于远程库是空的，第一次推送**master**分支时，加上了**-u**参数，Git不但把本地的**master**分支内容推送到远程新的**master**分支，还会把本地的**master**分支和远程的**master**分支关联起来，在以后的推送就可以简化命令，采用下面的命令：

```
git push origin master
```

* 从远程库克隆

我们可以将远程库利用下面命令克隆到本地库：

```
git clone https://github.com/edj19/Algorithms.git
```

好了通过上面的介绍一个简单的git操作以及与GitHub协作就整理的差不多，大家就可以愉快的学习了！！！！

## Git进阶

### 图片，目录

* 如何向GitHub中README.md添加图片呢？











