<!--
 * @Author: wzdnzd
 * @Date: 2022-03-06 14:51:29
 * @Description: 
 * Copyright (c) 2022 by wzdnzd, All Rights Reserved.
-->

> 說明: 
> + `auto-checkin.py`用於基於SS-Panel搭建的機場簽到，`renewal.py`用於基於V2Board搭建的機場訂閱續期
> + 支持`Python2` 和 `Python3`
> + 目前不支持任何帶有驗證碼（登陸或簽到時需要輸入驗證碼）功能的機場
> + 對於本項目來說，簽到是最不起眼的一個小功能。如果你喜歡探索，你將獲得如下成果。
<img width="1168" alt="a" src="https://github.com/wzdnzd/aggregator/assets/8565764/f75b8057-fa86-4d5c-a19f-fe3100ca853f">

## 免責申明
+ 本項目僅用作學習爬蟲技術，請勿濫用。
+ 禁止使用該專案進行任何盈利活動，對一切非法使用所產生的後果，本人概不負責。

## 自動簽到使用方法（支持多個機場）
### 1. 利用Github Actions簽到（推薦）
+ 點擊右上角`Fork`克隆本項目
+ ~~修改專案為私有，具體方法見[Github更改倉庫的可見性](https://docs.github.com/cn/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/setting-repository-visibility#changing-a-repositorys-visibility)~~
+ ~~編輯`.github/actions/checkin/config.json`，填寫機場功能變數名稱、郵箱及密碼~~
+ **設置密鑰：分別添加名（即`Name`）為 `AP_DOMAINS`、`AP_EMAILS`、`AP_PASSWORDS` 的密鑰並填寫對應的值（即`Value`）。如有多個帳號(不論是同一機場與否)，需要在 `Value` 欄裏一一填寫並用 `||` 隔開**
[![添加密鑰](https://s1.ax1x.com/2022/08/14/vNWxoj.png)](https://imgtu.com/i/vNWxoj)
[![密鑰](https://s1.ax1x.com/2022/08/14/vU1lng.png)](https://imgtu.com/i/vU1lng)
+ 若要修改簽到時間，可修改`.github/workflows/checkin.yml`檔的`cron`配置
[![修改簽到時間](https://s1.ax1x.com/2022/08/14/vUSkjS.png)](https://imgtu.com/i/vUSkjS)
+ 在 Actions 頁面啟用 workflow，可先手動觸發運行一次驗證配置是否正確
[![手動觸發](https://s1.ax1x.com/2022/08/14/vUlBFI.png)](https://imgtu.com/i/vUlBFI)

### 2. 本地運行
+ 克隆代碼庫
 ```shell
git clone https://github.com/wzdnzd/aggregator.git
```
+ 安裝依賴庫
```shell
pip install -U requests
```
+ 修改 `config.json` 配置檔
```ini
proxyServer: 代理伺服器地址，非必需

waitTime: 0 ~ 24，模擬任意時間簽到，非必需

retry: 失敗時重試次數，非必需

domains：支持多個機場，必須

domain：機場主功能變數名稱，必須

proxy：true | false，是否使用代理

email：註冊時使用的email

password：密碼
```
+ `windows` 操作系統可通過 `任務計畫程式` 添加到定時任務，詳見[Windows系統中設置Python程式定時運行](https://blog.csdn.net/CaiJin1217/article/details/81453940)
+ `Linux` 或 `MacOS` 可通過 `cron` 添加到定時任務（或登陸啟動項），詳見[利用Linux的crontab實現定時執行python任務](https://bbs.huaweicloud.com/blogs/333192)
