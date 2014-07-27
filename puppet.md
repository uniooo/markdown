# puppet 安装配置

## 一、安装

安装 CentOS 6.5

安装ruby(rdoc文档)：

    yum install ruby rdoc
    

添加源:

    rpm -ivh http://mirrors.sohu.com/fedora-epel/6/x86_64/epel-release-6-8.noarch.rpm
    rpm -ivh http://yum.puppetlabs.com/el/6/products/x86_64/puppetlabs-release-6-6.noarch.rpm
    
yum安装:

    yum install puppet

安装结束复制一份，作为c1。

---

## 二、配置
### 1、修改hosts、hostname、network
添加:

    192.168.40.134 c1.puppet c1
    192.168.40.135 master.puppet master

结束之后将hosts文件发送给c1

hostname命令:
查看:

    hostname

修改(将hostname修改为master.puppet):

    hostname master.puppet

network:

    vim /etc/sysconfig/network
    
    NETWORKING=yes
    HOSTNAME=master.puppet
    
**//MARK 此处添加规则貌似没有成功，故而后来采取关闭防火墙，先mark，待有空再研究一下防火墙**
### 2、添加防火墙规则，允许任何人连接TCP的8140端口：

    iptables -A INPUT -p tcp -m state --state NEW --dport 8140 -j ACCEPT

### 3、修改puppet.conf:

    vi /etc/puppet/puppet.conf
    
在`[master]`下面添加（如果`[master]`不存在，则手工添加）:

    certname = master.puppet
    
### 4、开启puppet master:

    puppet master --verbose --no-daemonize
    
`--verbose` 显示更多的输出项目
`--no-daemonize` 前台运行，并将输出重定向至标准输出
    
## 三、连接:
### 1、开启 puppet agent:

    puppet agent --server=master --no-daemonize --verbose
    
显示:

    Info: csr_attributes file loading from /etc/puppet/csr_attributes.yaml
    Info: Creating a new SSL certificate request for c1.puppet
    Info: Certificate Request fingerprint (SHA256): 7D:89:66:4F:FA:64:A8:21:F2:36:A6:5C:7D:19:69:0C:D3:DB:7C:13:1C:25:F4:41:62:17:5A:F0:A6:42:CC:34
    Notice: Did not receive certificate
    Notice: Did not receive certificate
    Notice: Did not receive certificate
    
### 2、在master上通过验证：

    puppet cert --list //列出请求列表
    puppet cert --sign c1.puppet //签名证书
    puppet cert --sign --all //对所有证书进行签名
    
## 四、编写配置：

这里我们用一个文件test做测试。我们希望test文件出现在c1的`/home/unio/`目录下。

### 1、site.pp文件

    import 'nodes.pp'
    $puppetserver = 'master.puppet'
    
### 2、创建nodes.pp并定义节点
    
    touch /etc/puppet/manifests/nodes.pp
    vim nodes.pp
    
nodes.pp:

    node 'c1.puppet' {
        include test
    }
    
    
### 3、创建test模块

    mkdir -p  /etc/puppet/modules/test/{files,templates,manifests}
    touch /etc/puppet/modules/test/manifests/init.pp
    
inti.pp:
    
    class test {
        file { "home/unio/test":
        owner => "unio",
        group => "unio",
        mode => 0440,
        source => "puppet://$puppetserver/modules/test/home/unio/test",
        }
    }

### 4、创建test文件

    mkdir -p /etc/puppet/modules/sudo/files/home/unio
    touch /etc/puppet/modules/sudo/files/home/unio/test
    vim test
    
test:

    this file should be send to c1



为了加速看到效果，我们重启c1后再次连接master。很快就可以看到c1的`/home/unio/`目录下的`test`文件了。



---

## FAQ：
### 1、防火墙：
为了避免防火墙的影响，使用`service iptables stop`关闭防火墙

### 2、删除agent端整个ssl文件夹：
这里注意，某些错误提示里面说 `rm -f /var/lib/puppet/ssl/c1.puppet.pem`,但是这样做貌似仍然无法work，即守候的命令行收到请求，但是puppet cert --list 显示没有收到证书请求

    rm -rf /var/lib/puppet/ssl
    
### 3、时间同步：
master和agent的时间必须同步，否则貌似会出一些奇怪的问题，使用：

    ntpdate asia.pool.ntp.org

    
## Reference：
精通Puppet配置管理工具 ISBN 978-7-115-27951-4
http://puppetlabs.com/
http://www.jsxubar.info/category/system-administration/puppet
http://www.liucy.org/2013/06/05/hello-world/
