# main.js

```
const { mockXHR } = require('../mock')  
mockXHR()
```

以下是mock文件夹的结构，下面一个一个来学习。

mock/

	-role/
		-index.js
		-routes.js
	-article.js
	-index.js
	-mock-server.js
	-remote-search.js
	-user.js
	-utils.js

# mock/index.js

### const Mock = require('mockjs')

[mockjs三方库](https://github.com/nuysoft/Mock/wiki/Getting-Started)


今天主要的目标是 封装一个基于axios和mockjs的带mock功能网络库。

应该达到什么目标：
mock：
1. 总控，分模块，分接口
2. 最好走axios统一的逻辑，包括统一的拦截器等逻辑，确保在发送和接受的逻辑一致。
3. 最好要改配置，逻辑，url。
4. 生产环境明确不能启用mock。
5. 挂载到原型链上最好，访问方便。

request：
1. 调用方便，挂载到原型链。
2. 拦截器 对错误进行统一处理。 比如超时，token失效需要重新登陆等。
3. 域名基于环境不同的管理，多个域名
4. https://www.jianshu.com/p/9077baa9d543
5. 