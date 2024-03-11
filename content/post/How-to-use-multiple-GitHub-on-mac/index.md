
---
author: Hugo Authors
title: 怎么在一台电脑上面设置工作和私人github 
date: 2024-03-08
description: 怎么在一台电脑上面设置工作和私人github账户
math: true
categories:
    - Test
    - 随笔

tags :
   - github

---




在使用github的时候,我们一般有两个账户,一个用于个人使用，另一个用于工作。今天在配置我的Mac时候，遇到了麻烦，我找了一些教程，但是很多说明不全面。在这篇文章中，我将把所有必要的步骤整合在一起，记录自己解决过程，希望也能帮助到你。

#### 1. 生成SSH密钥


可以参考github doc 文档中关于生成ssh的部分
https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

假设你的两个账户分别为`personal@gmail.com` 和 `work@gmail.com`  ,使用以下命令生成ssh key。    




```bash
    ssh-keygen -t ed25519 -C personal@gmail.com
    ssh-keygen -t ed25519 -C work@gmail.com     
```

然后查看你的目录`~/.ssh/`目录  会看到下面几个文件



```bash

    ~/.ssh/id_ed25519_personal        # 个人账户的私钥
    ~/.ssh/id_ed25519_personal.pub    # 个人账户的公钥
    ~/.ssh/id_ed25519_work            # 工作账户的私钥
    ~/.ssh/id_ed25519_work.pub        # 工作账户的公钥
    
```

生成密钥后运行此命令,启动一个 SSH 代理并将其环境变量添加到当前 shell 中。

````shell

    eval "$(ssh-agent -s)"      
    

````

### 2. 修改配置文件  ~./ssh/config 

然后修改 ~./ssh 下面的的config文件,  如果不存在，使用下面命令新建


```shell 

    touch ~/.ssh/config

 ```
 打开~/.ssh/config 文件，添加以下内容

 ``` shell
 
    #GitHub for personal
    Host github.com                              # Notice the host for personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_personal    # Private key for personal account

    #Github for work
    Host github.com-work                         # Notice the host for work 
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_work        # Private key for work account

    Host *
    # UseKeychain yes                           # If you choose a password to generate keys
    AddKeysToAgent yes                        # Load the keys from keychain into ssh-agent automatically
    IdentitiesOnly yes                        # Tells the ssh-agent server to use the IdentityFiles specified above for each host

```

保存文件,如果你在生成ssh key的时候选择使用密码，记得把 `# UseKeychain ～yes `   这行注释打开。

 ### 3.将密钥添加到 macOS 钥匙串

  ##### 1.--apple-use-keychain选项会将密钥存储到钥匙串中，并使密钥持久启动。

```shell

    ssh-add -D           # Will delete all identities added previously from the ssh agent
    ssh-add --apple-use-keychain ~/.ssh/id_ed25519_personal
    ssh-add --apple-use-keychain ~/.ssh/id_ed25519_work    


```



> 如果使用ssh-add -d用于删除身份，则钥匙串中的每个密钥都将被删除。（阅读手册页以ssh-add获取更多详细信息）。
##### 2. 检查密钥是否已经添加

使用`ssh-add -l`检查是否已添加。

此时，如果您重新启动系统，那么密钥将自动从钥匙串加载到 ssh-agent ！

### 4. 将公钥添加到您对应的账户中


将公钥添加到您在 GitHub 上的帐户。Github 已经有很好的文档了。有关更多信息，请参阅将新的 SSH 密钥添加到您的 GitHub 帐户。
https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account?platform=mac

### 5. 测试连接

测试两个帐户的连接

```shell
    ssh -T git@github.com
    ssh -T git@github.com-work    

````
如果配置正确，这应该返回

```shell
    Hi USERNAME1! You've successfully authenticated, but GitHub does not provide shell access. 
    Hi USERNAME2! You've successfully authenticated, but GitHub does not provide shell access. 

```
### 6. 如何使用 --克隆仓库

如果您想使用您的personal帐户，请从 GitHub 复制远程存储库链接并将其克隆为
``` shell

    git clone git@github.com:personal/project.git

```
如果你已经clone，可以设置remote url

``` shell

    git remote set-url origin git@github.com:personal/project.git

```

 如果你想使用你的工作账户，把通过将主机git@github.com替换为工作主机git@github.com-work来修改 
```shell

git clone git@github.com-work:company/project.git
```
设置远程originurl的规则相同

```shell

git remote set-url origin git@github.com-work:company/project.git

```
### 7. 测试一下

在 GitHub 上创建一个存储库，然后按照上面的说明克隆它。将当前工作目录更改为本地存储库。为此存储库配置用户电子邮件和名称（您也可以全局执行，但我更喜欢这种方式）。
如果您克隆了帐户的存储库work，则将其配置为

```shell
    git config --local user.email "work@gmail.com"
    git config --local user.name "work"
```
现在您可以向 GitHub 远程存储库推送/拉取。

```yaml
links:
  - title: GitHub
    description: GitHub is the world's largest software development platform.
    website: https://github.com
    image: https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png
  - title: TypeScript
    description: TypeScript is a typed superset of JavaScript that compiles to plain JavaScript.
    website: https://www.typescriptlang.org
    image: ts-logo-128.jpg
```