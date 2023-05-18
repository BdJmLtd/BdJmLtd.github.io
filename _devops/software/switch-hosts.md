---
title:  "SwitchHosts"
sequence: '001'
---

## 下载

下载地址：

```text
https://github.com/oldj/SwitchHosts/releases
```

找到`SwitchHosts_windows_installer_<version>.exe`文件：

{:refdef: style="text-align: center;"}
![](/assets/image/windows/software/switchhosts/switchhosts-windows-installer-exe-download.png)
{: refdef}

## 安装

下一步：

{:refdef: style="text-align: center;"}
![](/assets/image/windows/software/switchhosts/switchhosts-install-01.png)
{: refdef}

安装：

{:refdef: style="text-align: center;"}
![](/assets/image/windows/software/switchhosts/switchhosts-install-02.png)
{: refdef}

等待：

{:refdef: style="text-align: center;"}
![](/assets/image/windows/software/switchhosts/switchhosts-install-03.png)
{: refdef}

完成：

{:refdef: style="text-align: center;"}
![](/assets/image/windows/software/switchhosts/switchhosts-install-04.png)
{: refdef}

## 如何使用

第一步，“以管理员身份运行”SwitchHosts软件：

{:refdef: style="text-align: center;"}
![](/assets/image/windows/software/switchhosts/switchhosts-config-00.png)
{: refdef}

第二步，点击`+`号添加新配置：

{:refdef: style="text-align: center;"}
![](/assets/image/windows/software/switchhosts/switchhosts-config-01.png)
{: refdef}

选择“本地”，然后输入一个标题（例如，与ArcGIS服务相关，就输入“ArcGIS“）：

{:refdef: style="text-align: center;"}
![](/assets/image/windows/software/switchhosts/switchhosts-config-02.png)
{: refdef}

第三步，添加具体的Hosts信息，并启用它：

{:refdef: style="text-align: center;"}
![](/assets/image/windows/software/switchhosts/switchhosts-config-03.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/windows/software/switchhosts/switchhosts-config-04.png)
{: refdef}

第四步，验证是否成功。

第1种验证方式，回到“系统 Hosts“界面，如果看到刚才的配置的信息，就表示成功。

{:refdef: style="text-align: center;"}
![](/assets/image/windows/software/switchhosts/switchhosts-config-05.png)
{: refdef}

第2种验证方式，在命令行输入`ping arcgisportal.jinma.cn`，查看是否能够解析成功：

```cmd
> ping arcgisportal.jinma.cn
```

{:refdef: style="text-align: center;"}
![](/assets/image/windows/software/switchhosts/switchhosts-config-06.png)
{: refdef}

## 推荐配置

### ArcGIS

应该失效了：

```text
192.168.1.68 arcgisportal.jinma.cn
192.168.1.50 arcgisserver.jinma.cn
```

### WebSite

```text
# Github
20.205.243.166 github.com
140.82.114.4 github.com
20.27.177.113 github.com

# Github Pages
185.199.108.153 github.io
185.199.109.153 github.io
185.199.110.153 github.io
185.199.111.153 github.io

# Jekyll
185.199.108.153 jekyllrb.com
185.199.109.153 jekyllrb.com
185.199.110.153 jekyllrb.com
185.199.111.153 jekyllrb.com

# threejs
185.199.108.153 threejs.org
185.199.109.153 threejs.org
185.199.110.153 threejs.org
185.199.111.153 threejs.org

# cesium
65.9.42.17 www.cesium.com

# mvnrepository.com
104.22.60.77 mvnrepository.com
104.22.61.77 mvnrepository.com
172.67.28.102 mvnrepository.com
```

### 局域网

```text
192.168.1.200 maven.lan.net
192.168.1.200 nacos.lan.net
192.168.1.200 mysql.lan.net
192.168.1.200 doc.lan.net
192.168.1.200 jekyll.lan.net
192.168.1.211 dma.lan.net
192.168.1.211 device.lan.net
```
