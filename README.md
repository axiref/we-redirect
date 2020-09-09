# we-redirect

微信和QQ内置浏览器中的外链跳转，引导用户从浏览器打开

纯静态访问

支持白名单

# 使用

```
yarn install
yarn build
```

会编译在`./dist`目录，将该目录里生成的文件放在你的静态站点，比如绑定的域名是 `example.com`

访问

> example.com/?url=<你要跳转的URL>

这时候会弹出一个提示框，将其中的参数复制

访问

> example.com/<刚刚复制的内容>

这样就生成了你的跳转链接，这个链接可用于在QQ或者微信中分发

主要的参数是`u`，内容为base64编码后的URL

之所以需要编码，是因为QQ内置浏览器会根据URL的querystring进行拦截，所以起码得编码一下

还有白名单模式，打开 `src/App.vue`，修改其中的`allows`，内容为hostname

如果设置了`allows`变量，则白名单生效，留空则不使用白名单跳转

修改代码后需要再次运行`yarn build` 编译到`./dist`目录

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
