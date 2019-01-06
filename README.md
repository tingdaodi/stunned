# stunned
问题收集

将本地仓库 push 到 github 报错:

异常信息：

! [remote rejected] master -> master (push declined due to email privacy restrictions)
异常原因：

配置 git 时设置了作者邮箱信息，触发了Github 隐私保护设置：
Block command line pushes that expose my email

解决方法：

关闭 Block command line pushes that expose my email 这个选项：

很多人选择关掉 GitHub 中 Email 设置选项 Block command line pushes that expose my email ；很粗暴但是不推荐。

个人推荐：

更改 git 配置的邮件地址：
如果不想关闭上面的设置，可以通过修改 Email 来解决：

1、使用命令查看当前的全局用户 Email：
    git config --global user.email

2、找到你 GitHub 给的推荐 Email：
    在 settting --> Email --> keep my Email private 选项下的 Email；
        格式是：id+username@users.noreply.github.com

3、重新设置你的全局用户 Email：
    git config --global user.email "GitHub 给的推荐 Email"

4、重置上次提交的作者信息
    git commit --amend --reset-author

        输入命令后，进入vi模式（ git 默认的编辑器）；
        不熟悉的，可以直接在英文输入法下:wq(冒号wq)保存

5、提交
    git push
如果没有其他问题，大功告成。

I just encounterd the same problem.

The steps I took to fix (thanks for the advice on this thread) were roughly as follows:

git config --global user.email "526473+gb96@users.noreply.github.com"
git rebase -i
git commit --amend --reset-author
git rebase --continue
git push
 

I found rebase -i allowed be to edit the commit message but retained the previous (private) email address in the log.

The commit --amend --reset-author seemed to be the easiest way to replace the offending email address.
