# 📺 IPTV API M3U Documentation

Documentation for consuming the IPTV API via Xtream Codes and M3U List.

---

# 📌 Overview

This project provides access to IPTV streams through:

- 📡 Live Streams (Live TV)
- 🎬 VOD (Movies)
- 📺 Series
- 📂 Categories
- 📄 M3U List
- 🔐 Authentication via Xtream Codes

---

# 🔐 1. Authentication (Xtream Codes API)

## Base URL

```bash
http://YOUR_SERVER/player_api.php?username=USER&password=PASS
```

When accessing only with `username` and `password`, the API returns the account information:

## 📦 Authentication Response

```json
{
"user_info": {
"username": "",
"password": "", 
"message": "", 
"auth": 1, 
"status": "Active", 
"exp_date": "12312312", 
"is_trial": "0", 
"active_cons": "0", 
"created_at": "12313123", 
"max_connections": "1", 
"allowed_output_formats": ["ts"] 
}, 
"server_info": { 
"url": "server_url", 
"port": "80", 
"https_port": "443", 
"server_protocol": "http", 
"rtmp_port": "8001", 
"timezone": "AAAA", 
"timestamp_now": 123123123, 
"time_now": "2046-12-28 18:03:05"

}
}
```

---

# 📂 2. Categories

## 📺 Live TV Categories

```bash
http://YOUR_SERVER/player_api.php?username=USER&password=PASS&action=get_live_categories
```

### 📦 Response (Example)

```json
[

{
"category_id": "456",
"category_name": "(EXEMPLO)",
"parent_id": 0

},

{
"category_id": "4567",
"category_name": "(EXEMPLO)",
"parent_id": 0

},

{
"category_id": "45678", 
"category_name": "(EXEMPLO)", 
"parent_id": 0 
},
]
```

---

## 🎬 VOD Categories

```bash
http://YOUR_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_vod_categories
```

### 📦 Answer (Example)

```json
[ 
{ 
"category_id": "123", 
"category_name": "(EXEMPLO)", 
"parent_id": 0 
}, 
{ 
"category_id": "1234", 
"category_name": "(EXEMPLO)", 
"parent_id": 0 
}, 
{ 
"category_id": "12345", 
"category_name": "(EXEMPLO)", 
"parent_id": 0 
},
]
```


---

## 📺 Categories Series

```bash
http://YOUR_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_series_categories
```

### 📦 Answer (Example)

```json
[ 
{ 
"category_id": "789", 
"category_name": "(EXEMPLO)", 
"parent_id": 0 
}, 
{ 
"category_id": "78910", 
"category_name": "(EXEMPLO)", 
"parent_id": 0 
}, 
{ 
"category_id": "7891011", 
"category_name": "(EXEMPLO)", 
"parent_id": 0 
},
]
```

---

# 📡 3. Available Endpoints

---

## 📺 List Live Channels

```bash
http://YOUR_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_live_streams
```

### 📦 Answer (Example)

```json
[ 
{ 
"num": 1, 
"name": "Name TV", 
"stream_type": "created_live", 
"stream_id": 123, 
"stream_icon": "https://example.com", 
"epg_channel_id": null, 
"added": "123", 
"category_id": "1", 
"custom_sid": "", 
"tv_archive": 0, 
"direct_source": "", 
"tv_archive_duration": 0 
}
]
```

---

## 🎬 List VOD (Movies)

```bash
http://YOUR_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_vod_streams
```

### 📦 Answer (Example)

```json
[ 
{ 
"num": 1, 
"name": "Example Movie", 
"stream_type": "movie", 
"stream_id": 123, 
"stream_icon": "https://example.com", 
"rating": "0", 
"rating_5based": 0, 
"added": "123", 
"category_id": "1", 
"container_extension": "mp4", 
"custom_sid": "", 
"direct_source": "" 
}
]
```

---

## 📺 List Series

```bash
http://YOUR_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_series
```

### 📦 Answer (Example)

```json
[ 
{ 
"num": 1, 
"name": "(EXEMPLO)", 
"series_id": 2, 
"cover": "https://example.com", 
"plot": "description series", 
"cast": "example name, example name", 
"director": "", 
"genre": "Action & Adventure, Drama", 
"releaseDate": "2013-03-03", 
"last_modified": "123123", 
"rating": "8", 
"rating_5based": 4, 
"episode_run_time": "44", 
"category_id": "783" 
}
]
```

---

# ▶️ 4. How to Watch (Generate Final URL)

After obtaining the `stream_id`, assemble the final URL.

---

## 📺 Watch Live TV

```bash
http://YOUR_SERVER/live/USERNAME/PASSWORD/STREAM_ID.ts
```

### Example

```bash
http://example.com/live/123/123/456.ts
```

---

## 🎬 Watch VOD (Movies)

```bash
http://YOUR_SERVER/movie/USERNAME/PASSWORD/STREAM_ID.mp4
```

---

## 📺 Watch Episodes of Series

```bash
http://YOUR_SERVER/series/USERNAME/PASSWORD/STREAM_ID.mp4

```

---

# 📄 5. M3U List

## Standard Format

```bash
http://YOUR_SERVER/get.php?username=USER&password=PASS&type=m3u_plus&output=ts
```

The list can be used in:

- VLC
- Kodi
- IPTV Smarters
- Web Players
- Mobile Applications

---

# 💻 6. Consuming via JavaScript (Axios)

```javascript
import axios from "axios";

const api = axios.create({
baseURL: "http://YOUR_SERVER/player_api.php",

});

async function getVod() {

try {

const response = await api.get("", {

params: {

username: "YOUR_USER",

password: "YOUR_PASSWORD",

action: "get_vod_streams",

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

© 2026 - IPTV API M3U Documentation
