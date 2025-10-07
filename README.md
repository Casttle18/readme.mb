{
  "manifest_version": 3,
  "name": "Prompt Notes",
  "version": "0.1.0",
  "description": "Guarda y busca prompts como notas.",
  "action": { "default_popup": "popup.html", "default_icon": "icons/32.png" },
  "permissions": ["storage"],        // ← Necesario para guardar
  "commands": {                      // ← Atajo opcional
    "_execute_action": { "suggested_key": { "default": "Ctrl+Shift+P" } }
  }
  // TODO: agrega "icons" completos y verifica rutas
}
popup.html (UI mínima)

html
Copiar código
<!-- TODO: agrega inputs accesibles -->
<input id="title" placeholder="Título del prompt">
<textarea id="body" placeholder="Tu prompt"></textarea>
<button id="save">Guardar</button>
<input id="search" placeholder="Buscar…">
<ul id="list"></ul>

<script src="popup.js"></script>
<link rel="stylesheet" href="styles.css">
Modelo de datos (simple)

Objeto: { id, title, body, tags?, createdAt }

Pista: usa Date.now() para id y createdAt.

Almacén: chrome.storage.sync (sincroniza entre equipos; ~100KB por item / cuotas). Si te quedas corto → pasa a chrome.storage.local.

popup.js (pseudocódigo guiado)

js
Copiar código
// 1) Referencias a elementos
const titleEl = document.getElementById("title"); // ...
// 2) Cargar lista al abrir popup
//    PISTA: chrome.storage.sync.get({notes: []}, cb)
// 3) Guardar nota al click
//    - Validar campos
//    - Crear objeto nota
//    - Obtener notas existentes, push, set
//    - Limpiar inputs y recargar lista
// 4) Renderizar lista
//    - Crear <li> por nota (muestra título y fragmento)
//    - Botones: copiar, borrar (PISTA: delegación de eventos)
// 5) Buscar
//    - Filtra por title/body usando includes()
// 6) Borrar
//    - Filtra por id y set de nuevo
