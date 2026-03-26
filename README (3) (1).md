# 🎬 EdgarAI Stream

> Plataforma de streaming personal estilo Netflix — películas, series, anime, canales en vivo, radio y más.

![EdgarAI Stream](https://img.shields.io/badge/EdgarAI-Stream-e50914?style=for-the-badge&logo=netflix&logoColor=white)
![HTML](https://img.shields.io/badge/HTML5-Single%20File-orange?style=flat-square)
![Supabase](https://img.shields.io/badge/Supabase-Auth%20%2B%20DB-3ECF8E?style=flat-square)
![HLS.js](https://img.shields.io/badge/HLS.js-Streaming-blue?style=flat-square)
![TMDB](https://img.shields.io/badge/TMDB-API-01b4e4?style=flat-square)

---

## 📋 Descripción

EdgarAI Stream es una plataforma de streaming construida en un solo archivo HTML que combina el catálogo de TMDB con reproductores embebidos (Vidsrc) y soporte completo para listas M3U/IPTV. Incluye autenticación con Supabase, diseño responsive para móvil y soporte para múltiples categorías de contenido.

---

## ✨ Funcionalidades

- **🎬 Películas** — Catálogo completo vía TMDB con paginación, filtros por género y reproducción vía Vidsrc
- **📺 Series** — Selector de temporada y episodio, reproductor con fuentes en cadena
- **🎌 Anime** — Filtros por género (Acción, Comedia, Drama, Aventura)
- **🎨 Caricaturas** — En español e inglés con paginación
- **💃 Telenovelas** — México, Colombia, Argentina, Venezuela, Brasil, Chile, Perú
- **⚽ Deportes** — Canales en vivo + listas M3U deportivas
- **📡 Canales en Vivo** — 16+ canales HLS verificados (DW, France 24, Al Jazeera, NASA TV, etc.)
- **📻 Radio** — 30+ estaciones de radio en vivo (Latina, Pop, Rock, Jazz, Electrónica, Noticias)
- **🔞 Adultos +18** — Sección con carga de lista M3U propia
- **📋 Listas M3U** — 50+ listas organizadas por región y categoría
- **🔍 Búsqueda global** — Busca películas y series en tiempo real
- **👤 Autenticación** — Login, registro y perfil con avatares via Supabase

---

## 🛠️ Stack Tecnológico

| Tecnología | Uso |
|------------|-----|
| HTML5 / CSS3 / JS vanilla | Frontend completo (single file) |
| Supabase | Autenticación y base de datos |
| TMDB API | Catálogo de películas y series |
| HLS.js | Reproducción de streams M3U8 |
| Vidsrc / 2embed | Embeds de películas y series |
| iptv-org | Listas M3U públicas |

---

## 🚀 Instalación y uso

### Requisitos
- Un servidor web simple (Python, Node, nginx, Apache)
- Cuenta en [Supabase](https://supabase.com)
- API Key de [TMDB](https://www.themoviedb.org/settings/api)

### Configuración rápida

1. **Clona el repositorio**
```bash
git clone https://github.com/tu-usuario/edgarai-stream.git
cd edgarai-stream
```

2. **Abre `index.html`** y edita las constantes de configuración al inicio del script:
```javascript
const EDGAR_IMG    = 'URL_DE_TU_IMAGEN_EN_SUPABASE_STORAGE';
const SUPABASE_URL = 'https://tu-proyecto.supabase.co';
const SUPABASE_KEY = 'tu_anon_public_key';
const TMDB_KEY     = 'tu_tmdb_api_key';
```

3. **Corre el servidor**
```bash
# Con Python
python3 -m http.server 8080

# Con Node
npx serve .
```

4. **Abre** `http://localhost:8080` en tu navegador

---

## ⚙️ Configuración de Supabase

### Base de datos — tabla `profiles`
```sql
create table profiles (
  id uuid references auth.users on delete cascade primary key,
  username text,
  avatar text,
  avatar_filter text,
  email text,
  created_at timestamptz default now()
);

-- Habilitar RLS
alter table profiles enable row level security;

create policy "Users can view own profile"
  on profiles for select using (auth.uid() = id);

create policy "Users can update own profile"
  on profiles for update using (auth.uid() = id);

create policy "Users can insert own profile"
  on profiles for insert with check (auth.uid() = id);
```

### Storage — bucket `assets`
- Crea un bucket público llamado `assets`
- Sube tu imagen principal como `edgarai.jpg`

### Autenticación
- Ve a **Authentication → Providers → Email**
- Desactiva **"Confirm email"** para desarrollo local
- Reactiva cuando configures SMTP en producción

---

## 📱 Responsive

Optimizado para:
- iPhone 13 Pro (390×844)
- Android moderno
- Tablets
- Desktop

Incluye menú hamburguesa, barra de navegación inferior, buscador móvil y soporte para Safe Area (isla dinámica iPhone).

---

## 🎥 Fuentes de reproducción

El player usa un sistema de fuentes en cadena:

```
1. HLS.js (streams .m3u8 nativos)
   ↓ si falla →
2. Vidsrc.to
   ↓ si falla →
3. Vidsrc.me
   ↓ si falla →
4. 2embed.cc
   ↓ si falla →
5. Embedder.net
```

---

## 📡 Listas M3U incluidas

| Categoría | Listas |
|-----------|--------|
| Latinoamérica | México, Argentina, Colombia, Chile, Perú, Venezuela, Brasil y más |
| Europa | España, Francia, Alemania, Italia, UK, Rusia y más |
| USA/Global | EE.UU., Canadá, En Español Global, En Inglés Global |
| Asia | Japón, Corea, China, India, Indonesia |
| Películas | General, Documentales, Terror, Comedia |
| Series | General, En Español, USA |
| Anime | General, Japón, Latino |
| Deportes | Global, USA, MMA, Automovilismo |
| Noticias | Global, América, Europa |
| Radio | Global, Latina, USA |

---

## ⚠️ Aviso Legal

Este proyecto es de uso personal y educativo. El contenido reproducido a través de Vidsrc y otros embeds es responsabilidad de dichos servicios. Las listas M3U provienen de repositorios públicos como [iptv-org](https://github.com/iptv-org/iptv).

---

## 📄 Licencia

MIT License — libre para uso personal.

---

## 👤 Autor

**EdgarAI** — Urban · Digital · Anonymous

> *// Tu plataforma definitiva*
