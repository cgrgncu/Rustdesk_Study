# Rustdesk_Study

### 官方資源
+ 官方網站: https://rustdesk.com/
+ 說明文件(繁體中文): https://rustdesk.com/docs/zh-tw/

### Rustdesk Server by Synology NAS 7.2 Container Manager (Docker)
+ REF: https://rustdesk.com/docs/zh-tw/self-host/rustdesk-server-oss/synology/dsm-7/
+ 兩個容器:
  + hbbs - RustDesk ID註冊伺服器
    + hbbs預設使用port:
      + 21115(tcp)，用途: NAT類型測試
      + 21116(tcp/udp)，用途: 21116/UDP是hbbs用作ID註冊與心跳服務，21116/TCP是hbbs用作TCP打洞與連接服務
      + 21118(tcp)，用途: 21118和21119是為了支持網頁客戶端。如果您不需要網頁客戶端（21118，21119）支持，對應端口可以不開。
  + hbbr - RustDesk 中繼伺服器
    + hbbr預設使用port:
      + 21117(tcp)，用途:21117是hbbr用作中繼服務。
      + 21119(tcp)，用途: 21118和21119是為了支持網頁客戶端。如果您不需要網頁客戶端（21118，21119）支持，對應端口可以不開。
