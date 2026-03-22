# Clash Verge 客户端使用指南

## 步骤一：安装 Clash Verge

1. 前往 [Clash Verge 官方 GitHub](https://github.com/clash-verge-rev/clash-verge-rev/releases) 下载最新版本
2. 根据操作系统选择安装包：
   - macOS：下载 `.dmg` 文件
   - Windows：下载 `.exe` 安装包
   - Linux：下载 `.AppImage` 或 `.deb` 文件
3. 安装并启动 Clash Verge

---

## 步骤二：导入本地配置

将以下内容保存为 `config.yml`，然后导入到 Clash Verge：
用发给你的用户名和密码替换配置中的用户名密码
```yml
mixed-port: 7890
allow-lan: false
mode: rule
log-level: info

proxies:
  - name: "洛杉矶原生住宅节点-LA"
    type: hysteria2
    server: 45.32.67.92
    port: 443                                                                                                                                                                                                                     
    password: "用户名:密码"  
    sni: bing.com
    skip-cert-verify: true

proxy-groups:
  - name: "Proxy"
    type: select
    proxies:
      - 洛杉矶原生住宅节点-LA
      - DIRECT

rules:
  # 本地/局域网直连
  - GEOIP,PRIVATE,DIRECT

  # Apple 系统服务直连（iCloud同步、App Store、系统更新流量极大）
  - DOMAIN-SUFFIX,apple.com,DIRECT
  - DOMAIN-SUFFIX,icloud.com,DIRECT
  - DOMAIN-SUFFIX,apple-dns.net,DIRECT
  - DOMAIN-SUFFIX,mzstatic.com,DIRECT
  - DOMAIN-SUFFIX,cdn-apple.com,DIRECT

  # Windows 系统服务直连（系统更新、OneDrive、微软商店流量极大）
  - DOMAIN-SUFFIX,microsoft.com,DIRECT
  - DOMAIN-SUFFIX,windowsupdate.com,DIRECT
  - DOMAIN-SUFFIX,windows.com,DIRECT
  - DOMAIN-SUFFIX,microsoftonline.com,DIRECT
  - DOMAIN-SUFFIX,office.com,DIRECT
  - DOMAIN-SUFFIX,office365.com,DIRECT
  - DOMAIN-SUFFIX,onedrive.com,DIRECT
  - DOMAIN-SUFFIX,live.com,DIRECT
  - DOMAIN-SUFFIX,msftconnecttest.com,DIRECT
  - DOMAIN-SUFFIX,msftncsi.com,DIRECT

  # 国内域名直连（覆盖用了境外CDN的国内网站）
  - GEOSITE,CN,DIRECT
  # 国内 IP 直连
  - GEOIP,CN,DIRECT

  # 其余走代理
  - MATCH,Proxy
```

**导入方式：**

1. 打开 Clash Verge，点击左侧 订阅
2. 点击右上角 *新建  命名为 节点1
3. 选择本地配置文件 `config.yml` 导入
4. 导入成功后，点击该配置将其激活（激活后配置名称高亮显示）



## 步骤三：选择节点并设置规则模式

1. 在 Clash Verge 左侧点击 **订阅**，选中节点1
2. 在 Clash Verge 左侧点击 **代理**，选中洛杉矶原生住宅节点-LA
   - 右上角模式选择 **规则**（不要选"全局"，全局会绕过所有分流规则，流量全走代理）
3. 在 Clash Verge 左侧点击 **设置**，开启虚拟网卡模式（让所有程序的流量都被 Clash 接管）
4. 完成

> **注意：** 虚拟网卡（TUN）和规则模式是互相配合的：
> - 虚拟网卡 = 抓住所有流量
> - 规则模式 = 按 rules 决定直连还是代理
> 两者同时开启，国内流量自动直连，只有需要翻墙的流量才走 VPS，达到节省流量的效果。

