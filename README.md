<div align="center">
  <img src="./static/images/logo.png" alt="logo"/>
  <h1 align="center">IPTV-API</h1>
</div>
<div align="center">1、界面是在电脑win下运行，手机平板界面与此不同。2、因网站在境外，有可能打不开，可在网址前加kk。3、打开别人源代码，点击Forkw，此源代码就会自动粘贴到自己仓库下，文件名随便写。4、由于Fork下Actions 工作流默认关闭，需手动开启，第一次进入Actions，下方有I understand my w0rkflows……点击，就会在Actions下生成All workflows下update schedule，点击右侧Run workflow下Run workflow确认运行。5、第二次之后操作，直接点出Actions下update schedule，右侧Run workflow下Run workflow，因反应慢，需刷新。6、配置：config 文件夹内 demo.txt 是频道（📺央视频道、📡卫视频道、🌊港·澳·台频道、🎬电影频道等）。config 文件夹内的 config.ini 有生成结果路径，生成结果文件内本无output文件，设定好后，运行config/config.ini，成功后会自动生成；config/rtp目录下有组播数据地区_运营商.txt；首次工作流是手动触发，后续执行（默认北京时间每日6:00 与 18:00）将自动触发，如果想每2天执行更新可在github/workflows/main.yml下修改：- cron: '0 22 */2 * *'- cron: '0 10 */2 * *。</div>

- [🔗 最新结果](#最新结果)
- [⚙️ 配置参数](#配置)
- [🚀 快速上手](#快速上手)
    - [工作流](#工作流)
    - [命令行](#命令行)
    - [GUI软件](#GUI-软件)
    - [Docker](#Docker)
- [📖 详细教程](./docs/tutorial.md)
- [🗓️ 更新日志](./CHANGELOG.md)
- [📣 免责声明](#免责声明)
- [⚖️ 许可证](#许可证)
  
## 特点

- ✅ 自定义模板，生成您想要的频道
- ✅ 支持多种获取源方式：组播源、酒店源、订阅源、关键字搜索
- ✅ 接口测速验效，获取延迟、速率、分辨率，过滤无效接口
- ✅ 偏好设置：IPv6、接口来源排序优先级与数量配置、接口白名单
- ✅ 定时执行，北京时间每日 6:00 与 18:00 执行更新
- ✅ 支持多种运行方式：工作流、命令行、GUI 软件、Docker(amd64/arm64/arm v7)
- ✨ 更多功能请见[配置参数](#配置)
  
## 最新结果

- 接口源：
  
```bash
https://ghproxy.1888866.xyz/raw.github.com/Guovin/iptv-api/gd/output/result.m3u
```

```bash
https://ghproxy.1888866.xyz/raw.github.com/Guovin/iptv-api/gd/output/result.txt
```

或

```bash
https://cdn.jsdelivr.net/gh/Guovin/iptv-api@gd/output/result.m3u
```

```bash
https://cdn.jsdelivr.net/gh/Guovin/iptv-api@gd/output/result.txt
```

- 数据源：
  
```bash
https://ghproxy.1888866.xyz/raw.github.com/Guovin/iptv-api/gd/source.json
```

或

```bash
https://cdn.jsdelivr.net/gh/Guovin/iptv-api@gd/source.json
```

## 配置



### 快速上手

### 工作流

Fork 本项目并开启工作流更新，具体步骤请见[详细教程](./docs/tutorial.md）

### 命令行

```shell
pip install pipenv
```

```shell
pipenv install --dev
```

启动更新：

```shell
pipenv run dev
```

启动服务：

```shell
pipenv run service
```

### GUI 软件

1. 下载[IPTV-API 软件地址](https://github.com/Guovin/iptv-api/releases)，此软件用于W10，W7用iptv-update-too。
   
2. 或者在项目目录下运行以下命令，即可打开 GUI 软件：
   
```shell
pipenv run ui
```

<img src="./docs/images/ui.png" alt="IPTV-API更新软件" title="IPTV-API更新软件" style="height:600px" />

### Docker

- iptv-api（完整版本）：性能要求较高，更新速度较慢，稳定性、成功率高；修改配置 open_driver = False 可切换到 Lite
  版本运行模式（推荐酒店源、组播源、关键字搜索使用此版本）
- iptv-api:lite（精简版本）：轻量级，性能要求低，更新速度快，稳定性不确定（推荐订阅源使用此版本）
  
1. 拉取镜像：

- iptv-api：
  
```bash
docker pull guovern/iptv-api:latest
```

- iptv-api:lite：
  
```bash
docker pull guovern/iptv-api:lite
```

2. 运行容器：

- iptv-api：
```bash
docker run -d -p 8000:8000 guovern/iptv-api
```

- iptv-api:lite：
```bash
docker run -d -p 8000:8000 guovern/iptv-api:lite
```

卷挂载参数（可选）：
实现宿主机文件与容器文件同步，修改模板、配置、获取更新结果文件可直接在宿主机文件夹下操作
以宿主机路径/etc/docker 为例：

- iptv-api：
```bash
docker run -v /etc/docker/config:/iptv-api/config -v /etc/docker/output:/iptv-api/output -d -p 8000:8000 guovern/iptv-api
```

- iptv-api:lite：
- 
```bash
docker run -v /etc/docker/config:/iptv-api-lite/config -v /etc/docker/output:/iptv-api-lite/output -d -p 8000:8000 guovern/iptv-api:lite
```

端口环境变量：

```bash
-e APP_PORT=8000
```

3. 更新结果：
- 接口地址：ip:8000
- M3u 接口：ip:8000/m3u
- Txt 接口：ip:8000/txt
- 接口内容：ip:8000/content
- 测速日志：ip:8000/log
## 免责声明

本项目仅供学习交流用途，接口数据均来源于网络，如有侵权，请联系删除

## 许可证

[MIT](./LICENSE) License &copy; 2024-PRESENT [Govin](https://github.com/guovin)
