# Proyecto Anatomía Coronaria 3D - Listo para Netlify

## 📋 Estructura del Proyecto

```
netlify-deploy/
├── index.html           ← Aplicación principal (YA LISTA)
├── videos/              ← Coloca tus videos angiográficos aquí (.mp4, .webm)
├── posters/             ← Imágenes de preview de videos
├── frames/              ← Si usas secuencias de frames PNG
└── README.md            ← Este archivo
```

## 🚀 Cómo Subir a Netlify

### Opción 1: Drag & Drop (MÁS FÁCIL)

1. Ve a https://app.netlify.com
2. Crea una cuenta (gratis)
3. Arrastra TODA esta carpeta `netlify-deploy` a Netlify
4. ¡Listo! Tu sitio estará en: `https://tu-proyecto-123.netlify.app`

### Opción 2: Netlify CLI

```bash
# Instalar Netlify CLI
npm install -g netlify-cli

# Deployar
cd netlify-deploy
netlify deploy --prod
```

### Opción 3: GitHub + Netlify (Auto-deploy)

1. Sube este proyecto a GitHub
2. En Netlify → "New site from Git"
3. Conecta tu repositorio
4. Build settings:
   - Build command: (dejar vacío)
   - Publish directory: `/`

## 📹 Agregar tus Videos

1. Convierte tus secuencias DICOM a MP4:
   ```bash
   ffmpeg -i entrada.avi -vcodec libx264 -crf 23 -vf scale=800:-1 salida.mp4
   ```

2. Coloca videos en carpeta `videos/`:
   ```
   videos/
   ├── normal_rao30.mp4
   ├── normal_lao45.mp4
   ├── stenosis_lad.mp4
   └── ...
   ```

3. Actualiza las rutas en `index.html`:
   ```javascript
   video: 'videos/normal_rao30.mp4'
   ```

## 🌐 Conectar Dominio Propio

### En Netlify:
1. Ve a Site Settings → Domain Management
2. Add custom domain → Escribe tu dominio
3. Netlify te dará registros DNS

### En tu proveedor de dominio (GoDaddy, Namecheap, etc.):

**Para dominio principal (ejemplo.com):**
```
Tipo: A
Nombre: @
Valor: 75.2.60.5
```

**Para subdominio (coronarias.ejemplo.com):**
```
Tipo: CNAME
Nombre: coronarias
Valor: tu-proyecto.netlify.app
```

Espera 10-30 minutos para propagación DNS.

## 🔒 HTTPS Automático

Netlify activa HTTPS automáticamente en tu dominio. 
No necesitas hacer nada adicional.

## 📊 Optimización

### Si tus videos son muy pesados:

**Reducir tamaño:**
```bash
# Comprimir manteniendo calidad
ffmpeg -i input.mp4 -vcodec libx264 -crf 28 -preset slow output.mp4

# Convertir a WebM (más ligero)
ffmpeg -i input.mp4 -c:v libvpx-vp9 -crf 30 output.webm
```

### Hospedar videos externamente:

Si superas el límite de 100GB/mes de Netlify, usa:
- **Cloudflare R2** - Sin costo de transferencia
- **Bunny.net** - CDN video especializado
- **Backblaze B2** - Almacenamiento económico

## 🎯 Checklist Pre-Deploy

- [ ] Videos convertidos a MP4/WebM
- [ ] Videos colocados en carpeta `videos/`
- [ ] Rutas actualizadas en index.html
- [ ] Imágenes DICOM anonimizadas (sin datos de pacientes)
- [ ] Probado localmente abriendo index.html

## 💰 Costos

**Netlify Gratis:**
- ✅ Hosting ilimitado
- ✅ 100GB ancho de banda/mes
- ✅ HTTPS incluido
- ✅ Dominio personalizado

**Si necesitas más:**
- Netlify Pro: $19/mes (1TB ancho de banda)
- Dominio .com: ~$10/año

## 📞 Soporte

Si tienes dudas:
1. Documentación Netlify: https://docs.netlify.com
2. Comunidad: https://answers.netlify.com

## 🎓 Próximos Pasos

1. Deploy inicial con contenido de prueba
2. Agregar 3-5 videos reales
3. Configurar dominio propio
4. Agregar casos clínicos
5. Promocionar a colegas

¡Éxito con tu proyecto educativo!
