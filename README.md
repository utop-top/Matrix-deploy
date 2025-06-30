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
### synapse conduwuit 都为matirx服务器; 
### ele-hq中为相关的服务配置，
### element-web(网页登录客户端)
### element-call （视频通话服务,包含element-call,   lk-jwt,   likekit;)
### 假设你使用的域名为 example.com 作为matrix 主服务器地址与名称， example.com就是matrix服务器的server_name
### 那么你需要解析的域名有：
### matrix_server  : example.com
### element-call   ：call.example.com;   jwt.example.com;   livekit.example.com
### element-web    : app.example.com
### 记得将上述域名解析后更改nginx 中相关的域名

## ntfy为android的自定义推送服务，你只需要在服务器中搭建ntfy,使用命令创建一个管理员账户（项目中提供在ntfy/start.txt文件中）下载ntfy app ，配置好服务器。在element X 客户端选择ntfy推送


graph TD
    A[External Matrix Server] -->|/_matrix/federation/| B[Nginx:8448]
    B --> C[Upstream federation_readers]
    C --> D1[federation-reader-1:9601]
    C --> D2[federation-reader-2:9602]
    C --> D3[federation-reader-3:9603]
    D1 --> E[Upstream event_persisters]
    D2 --> E
    D3 --> E
    E --> F1[event-persister-1:9201]
    E --> F2[event-persister-2:9202]
    F1 --> G[synapse-db:5412]
    F2 --> G
    G --> H[Synapse Main Process:8008]
    H --> I[Upstream generic_workers]
    I --> J1[generic-worker-1:9101]
    I --> J2[generic-worker-2:9102]
    I --> J3[generic-worker-3:9103]
    I --> J4[generic-worker-4:9104]
    I --> J5[generic-worker-5:9105]
    I --> J6[generic-worker-6:9106]
    H --> K[push-worker-1:9501]
    H --> L[typing-writer-1:9701]
    H --> M[synapse-redis:6378]
    H --> N[Upstream federation_senders]
    N --> O1[federation-sender-1:9401]
    N --> O2[federation-sender-2:9402]
    N --> O3[federation-sender-3:9403]
    O1 --> A
    O2 --> A
    O3 --> A
    B --> P[Upstream media_workers]
    P --> Q1[media-worker-1:9301]
    P --> Q2[media-worker-2:9302]
    P --> Q3[media-worker-3:9303]
    J1 --> R[Client]
    J2 --> R
    J3 --> R
    J4 --> R
    J5 --> R
    J6 --> R
    K --> R
    L --> R
    Q1 --> R
    Q2 --> R
    Q3 --> R
