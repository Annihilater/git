[toc]
# 提交git的时候如何保护隐私文件？

作为程序员我们经常会在 github 上提交代码，但是有些隐私信息并不适合公开，比如数据库文件、系统自动生成的文件（如缩略图等）、语言编译时产生的文件以及带有敏感信息的配置文件等等。

那么我们如何限制这个文件提交呢？

好在 git 还是比较人性化的，我们只需要自己创建一个 `.gitignore` 文件，并且按照 git 的规则配置提交文件的规则就好了，git 会自动按照 `.gitignore` 文件里的规则来进行提交。

##命令行创建 `.gitignore` 文件：
```
cd directory 
touch .gitignore
```
**注:** `directory` 为 `.git` 所在目录

##编辑 `.gitignore` 文件
使用 `vim` 命令：
```
vi .gitignore
```
里面内容自己编辑了。
###编辑规则
1、`/` 表示目录 
比如 `/A/*` 就表示忽略 `A` 目录下所有内容
2、`*` 表示匹配多个字符
上面忽略 `A` 目录下的所有内容使用的是 `*` ，忽略 `iml` 结尾的文件即使用`.iml`
3、`[ ]` 表示匹配多个单个字符
`[abc]`就表示 `a`、`b`、`c` 中任何一个字符即可
4、`！` 表示跟踪某类文件
比如`/*，!*c` 表示忽略所有文件，但是跟踪`.c` 结尾的文件，这样 `.c` 结尾的文件就不会被忽略了

### .gitignore 文件模板
我们不必从头开始写 `.gitignore` 文件，因为 `github` 上有现成的开源模板：[A collection of .gitignore templates
](https://github.com/github/gitignore)

哈哈，`github` 真是个好东西！！！

##删除之前上传的不应该被上传的文件
我们都知道新手可能不会使用 `.gitignore` 文件，很大可能就上传了不该被上传的文件，那么这些已经上传的文件如何删除呢？

这时我们不能直接使用 `git rm directory`，这样就会删除本地仓库的文件，这不是我们想要的。

可以使用 `git rm -r -cached directory` 来删除缓冲，然后进行正常的
```
$ git add -A
$ git commit -m "提交信息"
$ git push origin master
```
这样之前上传的不该被上传的文件就被删除了。

