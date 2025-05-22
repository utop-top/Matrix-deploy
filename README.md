# 这里是整理出来的matrix 部署文档；使用docker 或者k8s 部署

### Matrix 是联邦通讯加密协议 官网：[Matrix.org](https://matrix.org)
### Matrix synapse github社区 [github/element-hq](https://github.com/element-hq/synapse) 目前由element分叉
###
###
### Synapse 服务器，主社区版（python语言）功能齐全且带实验功能的matrix

#### Matrix continuwuity （rust）轻量高效的matrix服务器 由conduwuit分叉出来，目前处于积极的维护状态，社区活跃
#### continuwuity官网 [continuwuity.org](https://continuwuity.org/) 
#### 项目地址[forgejo.ellis.link](https://forgejo.ellis.link/continuwuation/continuwuity)


## 关于部署
## synapse conduwuit 都为matirx服务器; 
## ele-hq中为相关的服务配置，
## element-web(网页登录客户端)
## element-call （视频通话服务,包含element-call,lk-jwt,likekit;)
## 假设你使用的域名为 example.com 作为matrix 主服务器地址与名称， example.com就是matrix服务器的server_name
## 那么你需要解析的域名有：
## matrix_server : example.com
## element-call 你需要解析的域名 call.example.com; jwt.example.com; livekit.example.com
## element-web : app.example.com
## 记得将上述域名解析后更改nginx 中相关的域名
