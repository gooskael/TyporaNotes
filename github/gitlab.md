[git连接gitlab远程仓库](https://blog.csdn.net/lkt_anhua/article/details/78835226)

ssh:

```shell
cd ~/.ssh
```

测试是否成功

```shell
ssh -T git@gitlab.com
```



```shell
// 查看已经连接的远程仓库
git remote -v
// 断开连接
git remote rm origin
```

