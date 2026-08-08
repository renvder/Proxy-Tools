# Brave Browser Fingerprint Protection Guide

This guide explains how to strengthen fingerprinting resistance and reduce potential WebRTC IP leaks in Brave Browser.

---

## Step 1: Enable Experimental Protections via Flags

1. Type the following address into the Brave address bar:

   ```text
   brave://flags
   ```

2. Search for:

   ```text
   Fingerprinting
   ```

3. Change relevant experimental options from **Default** to **Enabled**.

   Examples may include:

   - `Enable Fingerprinting Protection`
   - `Farbling enhancements`

> **Note:** Experimental flags may change, be renamed, or be removed in future Brave versions.

---

## Step 2: Configure Shields and WebRTC Policy

### Enable Strict Fingerprinting Protection

1. Open:

   ```text
   brave://settings/shields
   ```

2. Locate **Fingerprinting protection**.
3. Set it to:

   ```text
   Strict
   ```

#### Protection Effect

Brave can inject randomized data through its **Farbling** protections.

This can cause characteristic values returned by APIs such as the following to vary across browser sessions:

- Canvas
- WebGL
- WebGPU
- Audio fingerprinting APIs

This makes stable cross-site fingerprint tracking more difficult.

---

### Set WebRTC IP Handling Policy

> This helps prevent WebRTC from bypassing a proxy or VPN and exposing your real IP address.

1. Open:

   ```text
   brave://settings/privacy
   ```

2. Locate **WebRTC IP Handling Policy**.
3. Select:

   ```text
   Disable non-proxied UDP
   ```

#### Protection Effect

This forces WebRTC traffic to use a proxy or TCP connection where possible, reducing the risk that WebRTC UDP traffic bypasses your proxy and reveals your real public IP address.

---

## Step 3: Verify Protection Effectiveness

### Verify Fingerprint Randomization

1. Visit a browser fingerprint testing website, such as:

   - [BrowserScan](https://www.browserscan.net/)
   - [Cover Your Tracks](https://coveryourtracks.eff.org/)
   - [BrowserLeaks](https://browserleaks.com/)

2. Record your reported fingerprint values, especially:

   - Canvas fingerprint
   - WebGL fingerprint
   - AudioHash

3. Open a new Incognito window, or restart Brave.
4. Visit the same testing site again.
5. Check whether the fingerprint values change between sessions.

---

### Verify WebRTC IP Leaks

1. Enable your proxy or VPN connection.
2. Visit a WebRTC leak testing page, such as:

   - [BrowserLeaks WebRTC Test](https://browserleaks.com/webrtc)

3. Confirm that the page does **not** reveal:

   - Your real public IP address
   - Your local/private network IP address
   - Your ISP-provided IP address

> If a real IP address is still visible, review your proxy/VPN configuration and confirm that the selected WebRTC policy is active.

---

## Recommended Settings Summary

| Setting | Recommended Value |
|---|---|
| Fingerprinting protection | `Strict` |
| Fingerprinting-related flags | `Enabled` where available |
| WebRTC IP Handling Policy | `Disable non-proxied UDP` |
| Proxy/VPN | Enabled before testing for leaks |
