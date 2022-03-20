报错 git

# err
Git报错解决：fatal: unable to access: OpenSSL SSL_read: Connection was reset, errno 10054

解决办法:修改设置，解除ssl验证

git config --global http.sslVerify "false" 
git config --global https.sslVerify "false" 

git push -u origin main



# err2

fatal: Could not read from remote repository.

[配置ssh](https://docs.github.com/cn/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

[测试 是否连接成功](https://docs.github.com/cn/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection)



