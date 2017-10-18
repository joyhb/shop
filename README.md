# shop

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```
## github上传文件方法
#首先在自己的github上创建一个项目，右上角+号New repository，填写项目名称就好（英文的哦），其他都默认就可以。
## 在本地安装git，https://pan.baidu.com/s/1kU5OCOB#list/path=%2Fpub%2Fgit
#安装好了之后呢。打开Git Bash。创建SSH秘钥ssh-keygen -t rsa -C "youremail@example.com"，注意后面的邮箱是你注册github的邮箱哈。生成后在C盘的user（或者是用户）下的administrator下有个.ssh/id_rsa.pub文件，里面就是生成的秘钥
## 在你的github账户上创建ssh秘钥
在你的账户的settings下有SSH and GPG keys，然后点击new ssh key按钮，把.ssh/id_rsa.pub文件里面的内容复制过来就可以了
## 创建好了ssh秘钥就可以在本机Git Bash中创建目录了
1.可以创建空的目录
2.直接cd到现有的目录，例如：在E盘下的shop文件夹，那么在Git Bash中就cd e:  然后cd shop就到了shop目录了，然后使用下面的步骤上传文件到github就ok了
# git init
# git add README.md
# git commit -m "first commit"
# git remote add origin https://github.com/joyhb/shop.git
# git push -u origin master
# For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
## 删除远程分支git push origin  :分支名称  (注意冒号要与前面origin分开)
