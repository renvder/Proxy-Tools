# LibreWolf 瀏覽器 WebRTC 防護設定

本指南說明如何透過 `about:config` 精細控制 LibreWolf 的 WebRTC 行為，以降低真實 IP 位址與內網 IP 位址洩漏的風險。

---

## 透過 `about:config` 進行精細控制

1. 在 LibreWolf 網址列輸入：

   ```text
   about:config
   ```

2. 按下 Enter。
3. 點擊：

   ```text
   接受風險並繼續
   ```

---

## 1. 強制 WebRTC 僅透過 Proxy 連線

在搜尋欄輸入：

```text
media.peerconnection.ice.proxy_only
```

將值設定為：

```text
true
```

### 保護效果

- 強制所有 WebRTC 流量透過 Proxy 連線。
- 若已設定 Proxy，WebRTC 不會嘗試建立直接連線。
- 可降低 WebRTC 繞過 Proxy 並洩漏真實 IP 位址的風險。

> 此設定適合重視隱私，且已正確設定 Proxy 的使用者。

---

## 2. 限制使用預設路由 IP 位址

在搜尋欄輸入：

```text
media.peerconnection.ice.default_address_only
```

將值設定為：

```text
true
```

### 保護效果

- 僅使用預設網路路由的 IP 位址。
- 降低多網卡、多 VPN、虛擬網卡或區域網路環境下，其他內網 IP 位址被 WebRTC 收集的風險。

---

## 3. 禁止收集 Host Candidates

在搜尋欄輸入：

```text
media.peerconnection.ice.no_host
```

將值設定為：

```text
true
```

### 保護效果

- 禁止 WebRTC 收集任何 **Host Candidates**。
- 可進一步降低區域網路 IP 位址與本機網路資訊洩漏的可能性。
- 有助於提升匿名性與降低瀏覽器指紋資訊。

---

## 驗證 WebRTC 防護

完成設定後，建議先啟用 Proxy 或 VPN，再前往以下網站測試：

[BrowserLeaks WebRTC Test](https://browserleaks.com/webrtc)

確認頁面未顯示：

- 真實公開 IP 位址
- ISP 原始 IP 位址
- 區域網路／私人 IP 位址
- 不預期的 IPv6 位址

> 若仍出現真實 IP，請檢查 LibreWolf 的 Proxy 設定、VPN 狀態，以及上述 `about:config` 參數是否均已設為 `true`。

---

## 建議設定總覽

| 設定項目 | 建議值 | 作用 |
|---|---|---|
| `media.peerconnection.ice.proxy_only` | `true` | 強制 WebRTC 流量透過 Proxy |
| `media.peerconnection.ice.default_address_only` | `true` | 限制使用預設路由 IP |
| `media.peerconnection.ice.no_host` | `true` | 禁止收集 Host Candidates |
