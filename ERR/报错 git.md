报错 git

git push 发生1报错，最后用的是2方法解决了，git push 成功，但1方法解决方案还是写下来，万一哪天又碰到了呢。

1

github删除密码身份验证，改用token 个人访问令牌的

```bash
remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
remote: Please see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/ 
for more information.
fatal: Authentication failed for 'https://github.com/username/xxx.git/'
```

https://stackoverflow.com/questions/68775869/support-for-password-authentication-was-removed-please-use-a-personal-access-to

2

```bash
fatal: unable to access 'https://github.com/username/xx.git /': Empty reply from server
```



解决办法  

https://www.zhihu.com/question/26717343



git.config

1 sslVerify = true

2 proxy = 

```
[http]
	sslVerify = false
	proxy = 
```

