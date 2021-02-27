下载安装包

wget https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el7/gitlab-ce-13.8.4-ce.0.el7.x86_64.rpm

rpm -ivh gitlab-ce-13.8.4-ce.0.el7.x86_64.rpm

```
vim /etc/gitlab/gitlab.rb #修改external_url 'http://47.52.x.x' 改成IP地址访问gitlab
```

```
gitlab-ctl reconfigure
gitlab-ctl restart
```