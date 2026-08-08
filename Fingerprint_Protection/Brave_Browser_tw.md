# Brave 瀏覽器指紋保護指南

本指南說明如何在 Brave 瀏覽器中強化防指紋追蹤能力，並降低 WebRTC 洩漏真實 IP 位址的風險。

---

## 步驟 1：透過 Flags 啟用實驗性保護功能

1. 在 Brave 網址列輸入：

   ```text
   brave://flags
   ```

2. 在搜尋欄輸入：

   ```text
   Fingerprinting
   ```

3. 將相關實驗性選項從 **Default** 改為 **Enabled**。

   可能包含以下項目：

   - `Enable Fingerprinting Protection`
   - `Farbling enhancements`

> **注意：** 實驗性 Flags 的名稱、功能或可用性，可能會隨 Brave 版本更新而變更或移除。

---

## 步驟 2：設定 Shields 與 WebRTC 政策

### 啟用嚴格指紋保護

1. 開啟：

   ```text
   brave://settings/shields
   ```

2. 找到 **Fingerprinting protection**。
3. 設定為：

   ```text
   Strict
   ```

#### 保護效果

Brave 可透過 **Farbling** 保護機制注入隨機資料。

這可能使下列 API 回傳的特徵值，在不同瀏覽器工作階段之間產生變化：

- Canvas
- WebGL
- WebGPU
- 音訊指紋 API

這能增加跨網站追蹤時建立穩定瀏覽器指紋的難度。

---

### 設定 WebRTC IP 處理政策

> 此設定有助於避免 WebRTC 繞過 Proxy 或 VPN，進而暴露真實 IP 位址。

1. 開啟：

   ```text
   brave://settings/privacy
   ```

2. 找到 **WebRTC IP Handling Policy**。
3. 選擇：

   ```text
   Disable non-proxied UDP
   ```

#### 保護效果

此選項會讓 WebRTC 流量盡可能透過 Proxy，或改用 TCP 連線，以降低 WebRTC 的 UDP 流量繞過 Proxy 並洩漏真實公開 IP 位址的風險。

---

## 步驟 3：驗證保護效果

### 驗證指紋隨機化

1. 前往瀏覽器指紋偵測網站，例如：

   - [BrowserScan](https://www.browserscan.net/)
   - [Cover Your Tracks](https://coveryourtracks.eff.org/)
   - [BrowserLeaks](https://browserleaks.com/)

2. 記錄網站顯示的指紋資訊，尤其是：

   - Canvas 指紋
   - WebGL 指紋
   - AudioHash

3. 開啟新的無痕視窗，或完全重新啟動 Brave。
4. 再次造訪相同的測試網站。
5. 檢查上述指紋數值是否在不同工作階段之間發生變化。

---

### 驗證 WebRTC IP 洩漏

1. 先啟用你的 Proxy 或 VPN。
2. 前往 WebRTC 洩漏測試頁面，例如：

   - [BrowserLeaks WebRTC Test](https://browserleaks.com/webrtc)

3. 確認頁面沒有顯示以下資訊：

   - 真實公開 IP 位址
   - 區域網路／私人 IP 位址
   - ISP 提供的原始 IP 位址

> 若測試頁面仍顯示真實 IP，請檢查 Proxy 或 VPN 設定，並確認 WebRTC IP Handling Policy 已套用。

---

## 建議設定總覽

| 設定項目 | 建議值 |
|---|---|
| Fingerprinting protection | `Strict` |
| 與 Fingerprinting 相關的 Flags | 可用時設為 `Enabled` |
| WebRTC IP Handling Policy | `Disable non-proxied UDP` |
| Proxy／VPN | 測試 IP 洩漏前先啟用 |
