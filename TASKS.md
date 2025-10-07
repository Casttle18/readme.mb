# Lista de tareas derivada de README

## Manifest (manifest.json)
- [ ] Completar los metadatos del manifiesto, incluyendo los iconos requeridos y la verificación de rutas en `icons/`.
- [ ] Confirmar que la acción predeterminada (`default_popup`, `default_icon`) apunta a archivos existentes dentro de la extensión.
- [ ] Validar que los permisos incluyen `storage` y evaluar si son necesarios permisos adicionales.
- [ ] Revisar y ajustar el atajo de teclado (`Ctrl+Shift+P`) definido en `commands` según las necesidades del usuario.

## Interfaz (popup.html)
- [ ] Implementar los campos de entrada accesibles para título y cuerpo del prompt, cuidando etiquetas y atributos ARIA si son necesarios.
- [ ] Añadir el botón de guardado y los campos de búsqueda/listado respetando una estructura semántica.
- [ ] Conectar los recursos externos: `popup.js` y `styles.css`, asegurando que las rutas sean correctas.

## Modelo de datos
- [ ] Definir el objeto de nota con propiedades `{ id, title, body, tags?, createdAt }`.
- [ ] Implementar la generación de `id` y `createdAt` usando `Date.now()`.
- [ ] Determinar cómo gestionar opcionalmente las etiquetas (`tags`).

## Almacenamiento
- [ ] Utilizar `chrome.storage.sync` para guardar y sincronizar las notas.
- [ ] Manejar límites de cuota de `chrome.storage.sync` y definir una estrategia de migración a `chrome.storage.local` si es necesario.

## Lógica (popup.js)
- [ ] Obtener referencias a los elementos del DOM al cargar el popup.
- [ ] Cargar y renderizar la lista de notas al iniciar usando `chrome.storage.sync.get({ notes: [] }, callback)`.
- [ ] Validar y guardar nuevas notas al hacer clic en "Guardar", actualizando el almacenamiento y limpiando los campos.
- [ ] Renderizar la lista de notas mostrando título y fragmento, con botones para copiar y borrar (posible delegación de eventos).
- [ ] Implementar búsqueda en tiempo real filtrando por `title` y `body` con `includes()`.
- [ ] Implementar la eliminación de notas filtrando por `id` y actualizando el almacenamiento.
