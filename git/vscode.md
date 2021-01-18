[TOC]

### Vscode插件

[高效搬砖：我的VS Code配置分享和插件推荐](https://my.oschina.net/u/4593024/blog/4549653/)

#### 关于前端插件

```open in browser```

​		This allows you to open the current file in your default browser or application.

```Live Server```

​		Launch a development local Server with live reload feature for static & dynamic pages

​		当代码进行保存的时候可以即时地更新页面。

```Image preview```

​		悬停可以预览照片。

------------

### 关于git

```gitlens```

​		GitLens supercharges the Git capabilities built into Visual Studio Code. It helps you to visualize code authorship at a glance via Git blame annotations and code lens, seamlessly navigate and explore Git repositories, gain valuable insights via powerful comparison commands, and so much more.

​		gitlens可以看到git pull下来的所有文件的改动记录，并且观看代码的改动。

---

#### 关于代码任务管理

```todo tree``` & ```todo highlight```

​		两个配合使用可以记录。

​		```todo highlight``` > ```Extension Settings``` > ```Todohighlight: Keywords > Edit in settings.json``` 

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

```Highlight Matching Tag```

​		括号匹配等的高亮显示。

#### vscode git

​		```Source Control```栏：```Changes```文件夹保存本地修改过的代码的文件，通过在修改文件后的```+```可以将文件添加到```Stage Changes```，```commit```按钮可以将代码放在准备push的栈（commit之前记得在Message的input框中填写本次commit的内容），然后在```···```中的```push```将代码push上去。

​		同时如果想要pull/clone代码，也可以通过```···```中的```pull ```/ ```clone``` 进行操作。

