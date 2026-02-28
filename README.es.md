# 📺 Documentación de la API de IPTV M3U

Documentación para usar la API de IPTV mediante códigos Xtream y la lista M3U.

---

# 📌 Resumen

Este proyecto proporciona acceso a transmisiones IPTV mediante:

- 📡 Transmisiones en vivo (TV en vivo)
- 🎬 VOD (Películas)
- 📺 Series
- 📂 Categorías
- 📄 Lista M3U
- 🔐 Autenticación mediante Xtream Codes

---

# 🔐 1. Autenticación (API de Xtream Codes)

## URL base

```bash
http://YOUR_SERVER/player_api.php?username=USER&password=PASS
```

Al acceder solo con `username` y `password`, la API devuelve la información de la cuenta:

## 📦 Respuesta de autenticación

```json
{
"user_info": {
"username": "",
"password": "",
"message": "",
"auth": 1,
"status": "Activo",
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

# 📂 2. Categorías

## 📺 Categorías de TV en vivo

```bash
http://YOUR_SERVER/player_api.php?username=USER&password=PASS&action=get_live_categories
```

### 📦 Respuesta (Ejemplo)

```json
[

{
"category_id": "456",
"category_name": "COPINHA 2026 ⚽",
"parent_id": 0

},

{
"category_id": "4567",
"category_name": "PARTIDOS DE HOY",
"parent_id": 0

},

{
"category_id": "45678",
"category_name": "PAY-PER-VIEW",
"parent_id": 0
},
]
```

---

## 🎬 Categorías de VOD

```bash
http://YOUR_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_vod_categories
```

### 📦 Respuesta (Ejemplo)

```json
[
{
"category_id": "123",
"category_name": "LANZAMIENTOS 2026",
"parent_id": 0
},
{
"category_id": "1234",
"category_name": "LANZAMIENTOS 2025",
"parent_id": 0
},
{
"category_id": "12345",
"category_name": "2024 LANZAMIENTOS",
"parent_id": 0
},
]
```

---

## 📺 Categorías Serie

```bash
http://YOUR_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_series_categories
```

### 📦 Respuesta (Ejemplo)

```json
[
{
"category_id": "789",
"category_name": "Anime ∤ Doblado",
"parent_id": 0
},
{
"category_id": "78910",
"category_name": "Series ∤ Netflix",
"parent_id": 0
},
{
"category_id": "7891011",
"category_name": "Series ∤ Disney+",
"parent_id": 0
},
]
```

---

# 📡 3. Disponible Puntos finales

---

## 📺 Lista de canales en vivo

```bash
http://YOUR_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_live_streams
```

### 📦 Respuesta (Ejemplo)

```json
[
{
"num": 1,
"name": "Nombre TV",
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

## 🎬 Lista de VOD (Películas)

```bash
http://YOUR_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_vod_streams
```

### 📦 Respuesta (Ejemplo)

```json
[
{
"num": 1,
"name": "Película de ejemplo",
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

## 📺 Lista Serie

```bash
http://YOUR_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_series
```

### 📦 Respuesta (Ejemplo)

```json
[
{
"num": 1,
"name": "SERIES",
"series_id": 2,
"cover": "https://example.com",
"plot": "description series",
"cast": "example name, example name",
"director": "",
"genre": "Action & Adventure, Drama",
"releaseDate": "2013-03-03",
"last_modified": "123123",
"rating": "8",
"rating_based_5": 4,
"episode_run_time": "44",
"category_id": "783"
}
]
```

---

# ▶️ 4. Cómo ver (Generar URL final)

Después de obtener el `stream_id`, crea la URL final.

---

## 📺 Ver TV en vivo

```bash
http://SU_SERVIDOR/live/USERNAME/PASSWORD/STREAM_ID.ts
```

### Ejemplo

```bash
http://example.com/live/123/123/456.ts
```

---

## 🎬 Ver VOD (Películas)

```bash
http://SU_SERVIDOR/movie/USERNAME/PASSWORD/STREAM_ID.mp4
```

---

## 📺 Ver episodios de Serie

```bash
http://SU_SERVIDOR/series/NOMBRE_USUARIO/CONTRASEÑA/ID_DEL_STREAM.mp4

```

---

# 📄 5. Lista M3U

## Formato estándar

```bash
http://SU_SERVIDOR/get.php?username=USER&password=PASS&type=m3u_plus&output=ts
```

La lista se puede usar en:

- VLC
- Kodi
- Smarters de IPTV
- Reproductores web
- Aplicaciones móviles

---

# 💻 6. Consumir mediante JavaScript (Axios)

```javascript
import axios from "axios";

const api = axios.create({
baseURL: "http://SU_SERVIDOR/player_api.php",

});

Función asíncrona getVod() {

try {

const response = await api.get("", {

params: {

username: "TU_USUARIO",

password: "TU_CONTRASEÑA",

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

# 🔒 Mejores prácticas de seguridad

- ❌ Nunca expongas el nombre de usuario y la contraseña en el frontend
- ✅ Usa un proxy de backend
- ✅ Usa variables de entorno
- ✅ Usa HTTPS
- ✅ Controla las conexiones simultáneas

---

© 2026 - Documentación de la API de IPTV M3U