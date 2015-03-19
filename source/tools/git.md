# Git使用
## Ubuntu安装git
```
sudo apt-get install git
```
## 给Github添加ssh-key，无需密码向github提交内容
```
sshkeygen -t rsa
cat .ssh/id_rsa.pub
```
github -> Profile -> SSH keys Add -> SSH Key, 复制到Key中

## 将远程库拷贝至本地
```
git clone git@github.com:OpenMindClub/pythoncamp0.git
```

## 更新内容至远程
```
git add -A
git commit
git push
```

## 从远程更新内容至本地
```
git pull
```


