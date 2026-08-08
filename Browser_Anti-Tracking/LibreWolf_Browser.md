# LibreWolf WebRTC Protection Settings

This guide explains how to use `about:config` to control WebRTC behavior in LibreWolf and reduce the risk of public IP or local network IP leaks.

---

## Fine-Tune WebRTC Through `about:config`

1. Enter the following address in the LibreWolf address bar:

   ```text
   about:config
   ```

2. Press Enter.
3. Click:

   ```text
   Accept the Risk and Continue
   ```

---

## 1. Force WebRTC Traffic Through a Proxy

Search for:

```text
media.peerconnection.ice.proxy_only
```

Set the value to:

```text
true
```

### Protection Effect

- Forces all WebRTC traffic to use a proxy connection.
- When a proxy is configured, WebRTC will not attempt direct connections.
- Helps prevent WebRTC from bypassing the proxy and exposing your real IP address.

> This setting is recommended for privacy-focused users who have correctly configured a proxy.

---

## 2. Restrict WebRTC to the Default Route Address

Search for:

```text
media.peerconnection.ice.default_address_only
```

Set the value to:

```text
true
```

### Protection Effect

- Restricts WebRTC to using only the IP address of the default network route.
- Reduces the risk of exposing additional local IP addresses in systems with multiple network adapters, VPN adapters, virtual adapters, or local networks.

---

## 3. Disable WebRTC Host Candidates

Search for:

```text
media.peerconnection.ice.no_host
```

Set the value to:

```text
true
```

### Protection Effect

- Prevents WebRTC from collecting any **Host Candidates**.
- Further reduces the chance of exposing local/private IP addresses and local network information.
- Can improve anonymity and reduce fingerprinting information.

---

## Verify WebRTC Protection

After applying the settings, enable your proxy or VPN and visit:

[BrowserLeaks WebRTC Test](https://browserleaks.com/webrtc)

Confirm that the page does not reveal:

- Your real public IP address
- Your original ISP IP address
- Local/private network IP addresses
- Unexpected IPv6 addresses

> If your real IP address is still displayed, review your LibreWolf proxy settings, VPN connection status, and confirm that all listed `about:config` preferences are set to `true`.

---

## Recommended Settings Summary

| Preference | Recommended Value | Purpose |
|---|---|---|
| `media.peerconnection.ice.proxy_only` | `true` | Forces WebRTC traffic through a proxy |
| `media.peerconnection.ice.default_address_only` | `true` | Restricts WebRTC to the default route IP |
| `media.peerconnection.ice.no_host` | `true` | Prevents WebRTC Host Candidate collection |
