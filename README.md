

# 部署坑

1. 先去搞一下redis
https://vercel.com/hoeys-projects/~/stores/integration/upstash/store_taUx7Kht5YatLBj2/guides
拿到下面信息
```
KV_URL="rediss://default:xxx@crisp-whale-xxx.upstash.io:6379"
KV_REST_API_URL="https://crisp-whale-xxx.upstash.io"
KV_REST_API_TOKEN="xxx"
KV_REST_API_READ_ONLY_TOKEN="xxx"
REDIS_URL="rediss://default:xxx@crisp-whale-xxx.upstash.io:6379"
```

2. 改一下api.config.js
主要就是clientId和obfuscatedClientSecret, 到Azure API管理面板然后申请应用，在里面设置好，不会自行查一下，也都很简单

需要注意的是应用那里填写Web，然后写http://localhost

3. 改一下site.config.js

4. 改一下代码，重新提交到仓库
把这里面的clientSecret改成自己申请的clientSecret
index.ts 里面的 
```
body.append('client_secret', clientSecret)
```
oAuthHandler.ts 里面的
```
params.append('client_secret', clientSecret)
```

上面盖的内容都要提交到github仓库

5. 到vercel里面发布
这里需要注意 build用pnpm build和 pnpm install 
另外一个需要注意的是需要把上面申请的redis加进去，key填写等号左边的，value写等号右边的，注意不要带双引号

6. 访问具体的应用，然后获取access_token，登录成功。

7. 在vercel里面加了下面几个环境变量
```
CLIENT_ID
SECRET_KEY
USER_PRINCIPAL_NAME
BASE_DIRECTORY
ENABLE_EXPERIMENTAL_COREPACK

KV_URL
KV_REST_API_URL
KV_REST_API_TOKEN
KV_REST_API_READ_ONLY_TOKEN
REDIS_URL
```



