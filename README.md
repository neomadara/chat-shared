# chat-shared

Shared layer del sistema de mensajería en tiempo real. Contiene la lógica de negocio compartida entre las versiones web y mobile.

## Contenido

```text
chat-shared/
├── lib/
│   └── supabase.js             # Cliente Supabase (patrón initSupabase/getSupabase)
├── services/
│   └── chatService.js          # Servicio centralizado de operaciones de chat
├── hooks/
│   └── chat/
│       ├── useChatRooms.js     # Hook para lista de chatrooms
│       ├── useChatMessages.js  # Hook para mensajes con realtime y paginación
│       └── useSendMessage.js   # Hook para enviar mensajes
└── components/
    └── chat/
        ├── MessageSimple.js       # Componente de mensaje individual
        └── MemoizedMessageGroup.js # Componente de grupo de mensajes por fecha
```

## Inicialización

Este repo no se instala directamente. Se integra en `chat-web` y `chat-mobile` via git subtree bajo `src/shared/`.

Cada plataforma debe inicializar Supabase con sus propias variables de entorno:

```javascript
import { initSupabase } from './shared/lib/supabase'

initSupabase({
    url: process.env.SUPABASE_URL,
    anonKey: process.env.SUPABASE_ANON_KEY
})
```

## Sincronización

### Desde chat-shared hacia las plataformas

```bash
# En chat-shared
git add .
git commit -m "feat: update shared layer"
git push origin main
```

```bash
# En chat-web
git subtree pull --prefix=src/shared https://github.com/neomadara/chat-shared.git main --squash

# En chat-mobile
git subtree pull --prefix=src/shared https://github.com/neomadara/chat-shared.git main --squash
```

### Desde una plataforma hacia chat-shared

```bash
# Desde chat-web o chat-mobile
git subtree push --prefix=src/shared https://github.com/neomadara/chat-shared.git main
```

## Variables de entorno

Copia `.env-example` y completa con tus valores:

```bash
cp .env-example .env
```

```bash
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_ANON_KEY=your_anon_key_here
APP_NAME=Evaluacion
```
