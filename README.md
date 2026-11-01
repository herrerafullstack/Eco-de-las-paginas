# Eco de las páginas

Sitio web responsive de reseñas y recomendaciones literarias. Incluye catálogo público, filtros por género, búsqueda, detalle de reseñas, autenticación con Google mediante Firebase, panel administrativo y sincronización del catálogo JSON con Google Drive.

## Requisitos
- Node.js 20 o superior
- Proyecto Firebase con Authentication habilitado (proveedor Google)
- Proyecto Google Cloud con Google Drive API habilitada y OAuth 2.0 Web Client ID
- Firebase Hosting (opcional para publicar)

## 1. Configuración
1. Copiar `.env.example` a `.env`.
2. Completar los valores de Firebase desde **Firebase Console → Project settings → Your apps → Web app**.
3. Crear un OAuth Client ID tipo **Web application** en Google Cloud y completar `VITE_GOOGLE_CLIENT_ID`.
4. En el OAuth client, agregar los orígenes autorizados para desarrollo y producción (por ejemplo `http://localhost:5173` y el dominio de Hosting).
5. En Google Cloud, habilitar **Google Drive API**. Configurar la pantalla de consentimiento OAuth y agregar los usuarios de prueba mientras la app esté en modo testing.
6. Completar `VITE_ADMIN_EMAILS` con las cuentas que deben ver el panel, separadas por coma.

> La lista de administradores del frontend controla la visibilidad del panel, no constituye una autorización de servidor. El acceso a Drive se realiza con el consentimiento del usuario autenticado y el alcance `drive.file`. El archivo de datos se guarda en el Drive de la cuenta que autoriza la conexión.

## 2. Ejecutar localmente
```bash
npm install
npm run dev
```
Abrir la URL que informa Vite (habitualmente `http://localhost:5173`).

## 3. Compilar
```bash
npm run build
```
La salida se genera en `dist/`.

## 4. Publicar en Firebase Hosting
```bash
npm install -g firebase-tools
firebase login
firebase use --add
npm run build
firebase deploy --only hosting
```
Antes de publicar, configurar en Firebase Authentication → Settings → Authorized domains el dominio de producción.

## Uso
- El público puede explorar, filtrar y leer reseñas.
- Una cuenta autenticada cuyo email esté en `VITE_ADMIN_EMAILS` verá **Administrar**.
- Dentro del panel, conectar Google Drive para cargar o sincronizar `eco-de-las-paginas-data.json`.
- Se pueden agregar y eliminar lecturas y guardar notas privadas en el catálogo sincronizado.
- Sin Drive conectado, los cambios se conservan en el almacenamiento local del navegador.

## Personalización
- Estilos: `src/style.css`
- Interfaz y lógica: `src/main.js`
- Textos iniciales, géneros y libros de ejemplo: función `defaultData()` en `src/main.js`

## Importante antes de entregar
Este ZIP contiene una base funcional preparada para configuración, pero no incluye credenciales reales ni puede validar el acceso a cuentas Firebase/Google del propietario. Configurar los servicios y probar el flujo de login/Drive antes de usarlo en producción. El catálogo inicial contiene contenido de demostración que debe reemplazarse por el contenido definitivo.
