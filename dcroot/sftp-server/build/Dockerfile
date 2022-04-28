FROM centos:7
#第三步：指令集
RUN yum -y update
RUN yum -y install openssh* net-tools lsof telnet passwd 
RUN echo '123123' | passwd --stdin root
#不以PAM认证登录而是以密钥对登录（非对称密钥），即禁用ssh的PAM认证
RUN sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
#禁用ssh中PAM会话模块
RUN sed -i '/^session\s\+required\s\+pam_loginuid.so/s/^/#/' /etc/pam.d/sshd
#创建ssh工作目录和权限设置
RUN mkdir -p /root/.ssh && chown root:root /root && chmod 700 /root/.ssh
#开放22端口
EXPOSE 22
#第四步：启动容器时执行指令
CMD ["/usr/sbin/sshd","-D"]
