报错 git

# err
Git报错解决：fatal: unable to access: OpenSSL SSL_read: Connection was reset, errno 10054

解决办法:修改设置，解除ssl验证

git config --global http.sslVerify "false" 
git config --global https.sslVerify "false" 

git push -u origin main