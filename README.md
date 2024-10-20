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
  ```
  # 21114 TCP for web console, only available in Pro version
  # 21115 TCP for NAT type test
  # 21116 TCP TCP hole punching
  # 21116 UDP heartbeat/ID server
  # 21117 TCP relay
  # 21118/21119 TCP for web socket if you want to run web client
  ```
+ 安裝步驟
  + 安裝 Conrainer Manager
  + 開啟 Conrainer Manager
  + 專案>新增
    + 專案名稱: rustdesk-server
    + 路徑: /docker/rustdesk-server  (要先建好/docker/rustdesk-server/data)  
    + 建立 yaml檔案(參考官方，我改成指定版本1.1.9)
    + 

### Client 1.3.1
+ 下載位置: https://github.com/rustdesk/rustdesk/releases/tag/1.3.1
+ 必要設定: IP KEY 如果有改PORT就要指定
+ 自訂ID:
  + %AppData%\RustDesk\config\RustDesk.toml for portable
  + C:\Windows\ServiceProfiles\LocalService\AppData\Roaming\RustDesk\config\RustDesk.toml for installed
  stop all RustDesk.exe first.
  ```
  net stop RustDesk
  taskkill /im RustDesk /f
  
  $nome = (Get-CimInstance -ClassName Win32_ComputerSystem).Name
  $id = Get-Content C:\Windows\ServiceProfiles\LocalService\AppData\Roaming\RustDesk\config\RustDesk.toml | Select -First 1
  $newId = "id = '$nome'"
  
  $filecontent = Get-Content -Path C:\Windows\ServiceProfiles\LocalService\AppData\Roaming\RustDesk\config\RustDesk.toml -Raw
  
  $filecontent
  
  $filecontent.Replace("$id","$newId") | Set-Content -Path C:\Windows\ServiceProfiles\LocalService\AppData\Roaming\RustDesk\config\RustDesk.toml                  
  
  
  $pass = "password"
  $pw = Get-Content C:\Windows\ServiceProfiles\LocalService\AppData\Roaming\RustDesk\config\RustDesk.toml | Select -First 1 -Skip 1
  
  $newPw = "password = '$pass'"
  
  $filecontent = Get-Content -Path C:\Windows\ServiceProfiles\LocalService\AppData\Roaming\RustDesk\config\RustDesk.toml -Raw
  
  $filecontent
  
  $filecontent.Replace("$pw","$newPw") | Set-Content -Path C:\Windows\ServiceProfiles\LocalService\AppData\Roaming\RustDesk\config\RustDesk.toml
  $pw = Get-Content C:\Windows\ServiceProfiles\LocalService\AppData\Roaming\RustDesk\config\RustDesk.toml | Select -First 1 -Skip 1
  
  net start RustDesk
  ```
