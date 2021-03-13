[TOC]

### Vscode插件

[高效搬砖：我的VS Code配置分享和插件推荐](https://my.oschina.net/u/4593024/blog/4549653/)

#### `open in browser` & `Live Server`

`open in browser`：This allows you to open the current file in your default browser or application.

`Live Server`：Launch a development local Server with live reload feature for static & dynamic pages，当代码进行保存的时候可以即时地更新页面。

****

#### `Auto Rename Tag` `Bracket Pair Colorizer 2` `Highlight Matching Tag`

`Auto Rename Tag`：html标签同步更改。

 `Bracket Pair Colorizer 2`：会把不同的匹配括号用不同颜色标注出来，更容易找到配对的括号。

 `Hightlight Matching Tag`：点击一个标签之后，会在所配对的标签下面用underline标注出来。

`Image preview`：悬停可以预览照片。

------------

####  `gitlens`

`gitlends`：gitlens可以看到git pull下来的所有文件的改动记录，并且观看代码的改动。

---

#### `todo tree` & `todo highlight`

`Todo Tree`：记录关键字，比如`todo`，会以一棵树的方式在侧栏记录，点击后跳转到记录的位置。

`Todo Highlight`：对关键字有不同的样式展示，可以配置相关文件改变样式。

​		`todo highlight` > `Extension Settings` > `Todohighlight: Keywords > Edit in settings.json` 

```json
// settings.json
{
    "todo-tree.tree.showScanModeButton": false,
    "todohighlight.keywords": [
        "TODO",
        "FIXME",
    ],
    "todo-tree.regex.regexCaseSensitive": false,
    "todo-tree.tree.showInExplorer": true,
    "todo-tree.highlights.defaultHighlight": {
        "foreground": "black",
        "background": "yellow",
        "icon": "check",
        "rulerColour": "yellow",
        "type": "tag",
        "iconColour": "yellow"
    },
    "todo-tree.highlights.customHighlight": {
        "TODO": {
            "background": "yellow",
            "rulerColour": "yellow",
            "icon": "tag",
            "iconColour": "yellow"
        },
        "FIXME": {
            "background": "red",
            "icon": "beaker",
            "rulerColour": "red",
            "iconColour": "red",
        },
    },
}
```

****

### Vscode git

​		`Source Control`栏：`Changes`文件夹保存本地修改过的代码的文件，通过在修改文件后的`+`可以将文件添加到`Stage Changes`，`commit`按钮可以将代码放在准备push的栈（commit之前记得在Message的input框中填写本次commit的内容），然后在`···`中的`push`将代码push上去。

​		同时如果想要pull/clone代码，也可以通过`···`中的`pull `/ `clone` 进行操作。

#### 1. 无权限push

- [x] 问题出现：在终端上git clone了代码，在vscode上push的时候无权限，即`denied`。
- [x] 解决方式：使用终端进入到对应的目录下，`git push`可以成功，但是每次都要输入密码。

