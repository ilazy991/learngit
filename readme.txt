git学习

创建一个空目录：mkdir *
查看目录：pwd

通过git init命令把这个目录变成Git可以管理的仓库。
第一步用命令git add告诉Git，把文件添加到仓库：git add readme.txt 注意，可反复多次使用，添加多个文件；
第二步，用命令git commit告诉Git，把文件提交到仓库：git commit -m "wrote a readme file"
-m为本次add的说明
$ git commit -m "wrote a readme file"

要随时掌握工作区的状态，使用git status命令。

如果git status告诉你有文件被修改过，用git diff可以查看修改内容。

HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。






常用的git操作总结，大家看还有没有别的骚操作

从历史的提交建立新分支的方法：
方法一： checkout到历史提交，然后checkout -b。
方法二： reset到历史提交，checkout -b，然后再reset到原来的版本。
方法三： git branch <branch> <start point>

将某个历史版本全部拉到工作区和暂存区：
方法一： 可能的需求是为了将过去删除掉的修改重新应用到最新的版本，这时可以先回到历史版本处建立分支，然后回到原来的最新的版本，进行merge分支的操作。
方法二： reset加上hard参数到需要的历史版本，然后再reset加上soft参数回来。

将历史版本的某文件版本拉到当前工作区或者暂存区进行处理：
方法一： git reset HEAD~2 foo.py，直接拉到暂存区。
方法二： git checkout HEAD~2 foo.py，拉到工作区和暂存区。

已经有添加到暂存区的文件修改，之后又进行了修改。想要都撤销掉，变为和仓库中的版本相同（仓库覆盖工作和暂存）：
方法一：1、git reset HEAD file 清空暂存区的提交，变为和仓库中的版本相同。2、git checkout  --  file 以暂存区为蓝本，覆盖掉工作区。
方法二：git checkout HEAD --  file 。

已经添加到暂存区的修改之后又进行了修改，想要都撤销掉，变为和仓库中的版本相同（仓库覆盖工作和暂存）：
方法一：git reset --hard HEAD 重设HEAD，hard参数覆盖工作区和暂存区。
方法二：强制切换到其他分支丢弃更改，然后再切回来。

撤销当前工作区的文件修改，变为和暂存区相同（暂存覆盖工作）：
方法一：git checkout -- file 暂存区覆盖工作区(以暂存区为蓝本，覆盖掉工作区)。

撤销添加到暂存区的文件修改，将修改退回到工作区（暂存先覆盖工作，然后仓库覆盖暂存）：
方法一：1、git checkout  --  file 以暂存区为蓝本，覆盖掉工作区。 2、git reset HEAD file 清空暂存区的提交，变为和仓库中的版本相同。

清空暂存区文件修改：
方法一：git reset -- file 清空暂存区的文件修改。

清空暂存区：
方法一：git reset HEAD file 清空暂存区。

checkout文件层面的操作：
主要对暂存区和工作区起作用，一般有暂存区覆盖工作区的行为特征。

reset文件层面的操作：
主要对暂存区起作用。



命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。