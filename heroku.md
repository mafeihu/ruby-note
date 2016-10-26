##heroku

####第一次设定 Heroku
**[1].注册[Heroku] [1]帐号**
**[2].下载及安装 [toolbelt][2]工具**
@(安装命令如下)
`wget -O- https://toolbelt.heroku.com/install-ubuntu.sh | sh`

`wget -qO- https://toolbelt.heroku.com/install.sh | sh`
@(加载密钥)

@(查看命令)
```
$ heroku --version
heroku-toolbelt/3.43.9 (x86_64-darwin10.8.0) ruby/1.9.3
heroku-cli/5.2.39-010a227 (darwin-amd64) go1.6.2
```


**[3].请在你的专案目录下执行 `heroku create`**
####第一次在 Heroku 开 App
**前提：Heroku 使用Git进行布署，你的专案必须用Git做版本控制。**
**创建项目**
**添加到版本库**
**请在你的专案目录下执行 `heroku create`**
####部署到 Heroku
**[1].在你的专案目录下执行 `git push heroku master` 将程式推送到 heroku 去**
**[2].执行 `heroku run rake db:migrate`**
**[3].执行 `heroku open` 就会打开浏览器了**
####如何浏览 Logs?
**`heroku logs --tail`**
####打开远端的 Rails console？
**`heroku run rails console`**

[1]: https://dashboard.heroku.com/
[2]: https://devcenter.heroku.com/articles/heroku-command-line/