### 如何用gitignore删除远程repo里的不需要的文件/夹

#### 适用情况：
目前已经创建了github repo并且已经push过至少一遍代码，在push过程中可能用的是
```
git add.
```
```
git commit -m "xxxxx"
```
```
git push origin [branch_name]
```
这三行命令。但之后突然发现其实有些不需要的文件，文件夹，比如说vscode生成的.vscode文件夹，或者.env文件夹等也同样被push了，那如何在repo中删除他们呢？

#### 1. gitignore
我们可以在项目文件夹下创建一个叫.gitignore的文件，这个文件可以用来声明哪些项目文件或文件夹是被过滤掉的，比如现在我的项目文件夹叫做project， project里有两个子文件夹
A, B, 还有冗余文件夹.vscode, .env，为了在repo中只保留A,B， 先在project里创建.gitignore文件，然后写出要过滤的文件与文件夹

```markdown
# .gitignore file
.env
.vscode
```

#### 2. 清除repo里的cache
因为我们之前已经把.vscode, .env文件夹给push了，如果在写完.gitignore文件之后直接push的话是无法删除repo里的文件夹的，即使新建一个branch再push也没有效果，这是因为
git有缓存，所以我们需要清除缓存使用以下命令
```
git rm -r --cached .env .vscode
```
清除之后再进行add, commit，push 三个操作，就会发现.gitignore起作用了，.vscode, .env在repo中被删除。

