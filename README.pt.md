
# 📺 IPTV API M3U Documentation

Documentação para consumo da API IPTV via Xtream Codes e Lista M3U.

---

# 📌 Visão Geral

Este projeto fornece acesso a streams IPTV através de:

- 📡 Streams ao Vivo (Live TV)
- 🎬 VOD (Filmes)
- 📺 Séries
- 📂 Categorias
- 📄 Lista M3U
- 🔐 Autenticação via Xtream Codes

---

# 🔐 1. Autenticação (Xtream Codes API)

## Base URL

```bash
http://SEU_SERVIDOR/player_api.php?username=USER&password=PASS
```

Ao acessar apenas com `username` e `password`, a API retorna as informações da conta:

## 📦 Resposta de Autenticação

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
    "url": "url_servidor",
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

# 📂 2. Categorias

## 📺 Categorias Live TV

```bash
http://SEU_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_live_categories
```

### 📦 Resposta (Exemplo)

```json
[
    {
        "category_id": "456",
        "category_name": "COPINHA 2026 ⚽",
        "parent_id": 0
    },
    {
        "category_id": "4567",
        "category_name": "JOGOS DE HOJE",
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

## 🎬 Categorias VOD

```bash
http://SEU_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_vod_categories
```

### 📦 Resposta (Exemplo)

```json
[
    {
        "category_id": "123",
        "category_name": "LANÇAMENTOS 2026",
        "parent_id": 0
    },
    {
        "category_id": "1234",
        "category_name": " LANÇAMENTOS 2025",
        "parent_id": 0
    },
    {
        "category_id": "12345",
        "category_name": "LANÇAMENTOS 2024",
        "parent_id": 0
    },
]
```


---

## 📺 Categorias Séries

```bash
http://SEU_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_series_categories
```

### 📦 Resposta (Exemplo)

```json
[
     {
        "category_id": "789",
        "category_name": "Anime ∤ Dublado",
        "parent_id": 0
    },
    {
        "category_id": "78910",
        "category_name": "Serie ∤ Netflix",
        "parent_id": 0
    },
    {
        "category_id": "7891011",
        "category_name": "Serie ∤ Disney+",
        "parent_id": 0
    },
]
```

---

# 📡 3. Endpoints Disponíveis

---

## 📺 Listar Canais ao Vivo

```bash
http://SEU_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_live_streams
```

### 📦 Resposta (Exemplo)

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

## 🎬 Listar VOD (Filmes)

```bash
http://SEU_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_vod_streams
```

### 📦 Resposta (Exemplo)

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

## 📺 Listar Séries

```bash
http://SEU_SERVIDOR/player_api.php?username=USER&password=PASS&action=get_series
```

### 📦 Resposta (Exemplo)

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
    "rating_5based": 4,
    "episode_run_time": "44",
    "category_id": "783"
  }
]
```

---

# ▶️ 4. Como Assistir (Gerar URL Final)

Após obter o `stream_id`, monte a URL final.

---

## 📺 Assistir Live TV

```bash
http://SEU_SERVIDOR/live/USERNAME/PASSWORD/STREAM_ID.ts
```

### Exemplo

```bash
http://example.com/live/123/123/456.ts
```

---

## 🎬 Assistir VOD (Filmes)

```bash
http://SEU_SERVIDOR/movie/USERNAME/PASSWORD/STREAM_ID.mp4
```

---

## 📺 Assistir Episódios de Séries

```bash
http://SEU_SERVIDOR/series/USERNAME/PASSWORD/STREAM_ID.mp4
```

---

# 📄 5. Lista M3U

## Formato Padrão

```bash
http://SEU_SERVIDOR/get.php?username=USER&password=PASS&type=m3u_plus&output=ts
```

A lista pode ser utilizada em:

- VLC
- Kodi
- IPTV Smarters
- Players Web
- Aplicações Mobile

---

# 💻 6. Consumindo via JavaScript (Axios)

```javascript
import axios from "axios";

const api = axios.create({
  baseURL: "http://SEU_SERVIDOR/player_api.php",
});

async function getVod() {
  try {
    const response = await api.get("", {
      params: {
        username: "SEU_USER",
        password: "SUA_SENHA",
        action: "get_vod_streams",
      },
    });

    console.log(response.data);
  } catch (error) {
    console.error("Erro:", error);
  }
}

getVod();
```

---

# 🔒 Boas Práticas de Segurança

- ❌ Nunca exponha username e password no frontend
- ✅ Utilize backend proxy
- ✅ Utilize variáveis de ambiente
- ✅ Use HTTPS
- ✅ Controle conexões simultâneas

---

© 2026 - IPTV API M3U Documentation
