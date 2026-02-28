# 📺 IPTV API M3U Documentation

Documentation for consuming the API via Xtream Codes and M3U List.

# 📺 Technical Study of Streaming APIs

<p align="center">
<img src="https://img.shields.io/badge/STATUS-EDUCACIONAL-blue?style=for-the-badge">

<img src="https://img.shields.io/badge/FIM-APENAS%20PARA%20ESTUDO-green?style=for-the-badge">
</p>

<p align="center">

<b>⚠️ IMPORTANT LEGAL NOTICE ⚠️</b><br>

This material is EXCLUSIVELY for educational and technical study purposes.

There is no connection with any commercial or illegal service.

All data is fictitious and serves only to demonstrate API structures.

</p>

---

## 📌 About this Study

This repository documents **technical concepts**

---

# 📌 Overview

This project provides access to API streams through:

- 📡 Live Streams (EXAMPLE)
- 🎬 VOD (EXAMPLE)
- 📺 Series (EXAMPLE)
- 📂 Categories (EXAMPLE)
- 📄 M3U List (EXAMPLE)
- 🔐 Authentication via Xtream Codes (EXAMPLE)

---

# 🔐 1. Authentication (Xtream Codes API EXAMPLE)

## Base URL

```bash
http://EXEMPLA_URL/player_api.php?username=USER&password=PASS
```

When accessing only with `username` and `password`, the API returns the account information:

---

# 📂 2. Categories

## 📺 Live TV Categories

```bash
http://EXEMPLA_URL/player_api.php?username=USER&password=PASS&action=get_live_categories
```
---

## 🎬 VOD Categories

```bash
http://EXEMPLA_URL/player_api.php?username=USER&password=PASS&action=get_vod_categories
```
---

## 📺 Categories Series

```bash
http://EXEMPLA_URL/player_api.php?username=USER&password=PASS&action=get_series_categories
```
---

# 📡 3. Available Endpoints

---

## 📺 List Live Channels

```bash
http://EXEMPLA_URL/player_api.php?username=USER&password=PASS&action=get_live_streams
```
---

## 🎬 List VOD (Movies)

```bash
http://EXEMPLA_URL/player_api.php?username=USER&password=PASS&action=get_vod_streams
```
---

## 📺 List Series

```bash
http://EXEMPLA_URL/player_api.php?username=USER&password=PASS&action=get_series
```
---

# ▶️ 4. How to Watch (Generate Final URL)

After obtaining the `stream_id`, assemble the final URL.

---

## 📺 Watch Live TV

```bash
http://EXEMPLA_URL/live/USERNAME/PASSWORD/STREAM_ID.ts
```

### Example

```bash
http://example.com/live/123/123/456.ts
```

---

## 🎬 Watch VOD (Movies)

```bash
http://EXEMPLA_URL/movie/USERNAME/PASSWORD/STREAM_ID.mp4
```

---

## 📺 Watch Episodes of Series

```bash
http://EXEMPLA_URL/series/USERNAME/PASSWORD/STREAM_ID.mp4

```

---

# 📄 5. M3U List

## Standard Format

```bash
http://EXEMPLA_URL/get.php?username=USER&password=PASS&type=m3u_plus&output=ts
```

The list can be used in:

- VLC
- Kodi
- Smarters
- Web Players
- Mobile Applications

---

# 💻 6. Consuming via JavaScript (Axios)

```javascript
import axios from "axios";

const api = axios.create({
baseURL: "http://EXEMPLA_URL/player_api.php",

});

async function getVod() {

try {

const response = await api.get("", {

params: {

username: "YOUR_USER",

password: "YOUR_PASSWORD",

action: "actions",

},

});

console.log(response.data);

} catch (error) {

console.error("Error:", error);

}
}

getVod();

```

---

# 🔒 Security Best Practices

- ❌ Never expose username and password on the frontend
- ✅ Use backend proxy
- ✅ Use environment variables
- ✅ Use HTTPS
- ✅ Control simultaneous connections

---

© 2026 - API M3U Documentation
