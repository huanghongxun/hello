> 中山大学数据科学与计算机学院 软件工程 2017级 服务计算作业，17343050
GitHub 仓库地址：https://github.com/huanghongxun/hello
# 安装 Golang
Ubuntu 18.04 默认的 apt 源中包含的 golang-go 包是 Go 1.10，并不是最新版，因此添加非官方的软件源 `sudo add-apt-repository ppa:knakamur/golang-1.13` 以获得 Go 1.13。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190907235125188.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h1YW5naG9uZ3h1bg==,size_16,color_FFFFFF,t_70)
添加了软件源之后，我们就可以通过命令 `sudo apt install golang-go` 安装 Go 1.13 了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190907235021382.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h1YW5naG9uZ3h1bg==,size_16,color_FFFFFF,t_70)
## 安装必要的工具和插件
### 安装 Git 客户端
通过命令 `sudo apt install git` 即可安装 git 工具。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190908094102958.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h1YW5naG9uZ3h1bg==,size_16,color_FFFFFF,t_70)
### 安装 Go 相关工具
鉴于国内无法正常连接 Google 的站点 `golang.org`，我们使用代理解决：通过添加环境变量 `GOPROXY`、`all_proxy` 使 `go get` 命令通过我们自己的代理访问 `golang.org`：通过命令 `sudo vim /etc/profile.d/goproxy.sh` 添加脚本以添加环境变量：
比如我的 http 代理服务器架设于本地的 `http://localhost:1080`，那么通过命令 `export GOPROXY=http://localhost:1080` 命令即可导出环境变量。然后注销并重新登录后环境变量即可生效。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019090810113114.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h1YW5naG9uZ3h1bg==,size_16,color_FFFFFF,t_70)
这样 VSCode 就可以正常安装 Go 语言的相关工具了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190908100243854.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h1YW5naG9uZ3h1bg==,size_16,color_FFFFFF,t_70)
# Hello World
首先通过创建项目文件夹 `~/gowork`
```bash
mkdir -p ~/gowork
```
接着我们使用 `go mod init github.com/huanghongxun/hello` 创建模块，并创建 `~/gowork/main.go`：
```go
package main

import "fmt"

func main() {
    fmt.Printf("hello, world\n")
}   
```
并使用 `go install github.com/huanghongxun/hello` 命令编译并安装模块后即可通过 `hello` 命令调用我们创建的程序：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190908101641121.png)
我们可以通过 `which hello` 命令查看程序的安装位置，可以看到被安装在 `$GOPATH/bin` 下。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190908101712435.png)
# Go Tour
通过命令
```bash
go get -u golang.org/x/tour
tour
```
即可启动 gotour:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190908104525301.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h1YW5naG9uZ3h1bg==,size_16,color_FFFFFF,t_70)

# 你的第一个库
为了创建 `stringutil` 包，我们在 `gowork` 文件夹根目录下创建 `stringutil` 文件夹，并创建 `reverse.go` 文件如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190908105054466.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h1YW5naG9uZ3h1bg==,size_16,color_FFFFFF,t_70)
接着我们便可通过 `go build github.com/huanghongxun/hello/stringutil` 命令编译这个库了。（注意，这种方法必须使用 Go 1.12 及以上版本，并通过 `go mod init github.com/huanghongxun/hello` 命令来创建根模块才可以，否则你必须使用传统的文件目录格式。）
最后我们修改 `main.go` 引用这个库如下，可以看到终端输出正常工作，输出了 `Hello, Go!`。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190908105006545.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h1YW5naG9uZ3h1bg==,size_16,color_FFFFFF,t_70)
## 创建测试
通过创建 `XXX_test.go` 文件来测试 `XXX.go` 代码的正确性，go 提供了基本的单元测试框架 `testing` 帮助我们进行测试。
我们创建 `stringutil/reverse_test.go` 来测试 `reverse.go` 的正确性，可以看到 `go test github.com/huanghongxun/hello/stringutil` 命令正常测试了 `reverse.go` 的功能，并输出了测试时间。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190908105548756.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h1YW5naG9uZ3h1bg==,size_16,color_FFFFFF,t_70)