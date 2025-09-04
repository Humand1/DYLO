# DYLO - Aplicación Web de Subida de Documentos

Una aplicación web moderna para procesar y subir documentos PDF a la plataforma Humand con separación automática por RFC.

## Características

- **Interfaz web moderna**: Diseño responsive con drag & drop
- **Procesamiento automático**: Separación de PDFs por RFC
- **Integración con APIs**: Conexión con Redash y Humand
- **Gestión de usuarios**: Mapeo automático RFC → username
- **Configuración de firma**: Soporte para documentos que requieren firma
- **Logs en tiempo real**: Seguimiento detallado del proceso
- **Deployment en Vercel**: Configurado para hosting en la nube

## Estructura del Proyecto

```
dylo_web_app/
├── backend/                 # API FastAPI
│   ├── main.py             # Aplicación principal
│   ├── models.py           # Modelos de datos
│   ├── redash_client.py    # Cliente para APIs de Redash
│   ├── pdf_processor.py    # Procesamiento de PDFs
│   └── humand_client.py    # Cliente para API de Humand
├── frontend/               # Interfaz web
│   ├── index.html          # Página principal
│   ├── style.css           # Estilos CSS
│   └── script.js           # Lógica JavaScript
├── requirements.txt        # Dependencias Python
├── vercel.json            # Configuración de Vercel
└── README.md              # Este archivo
```

## Tecnologías Utilizadas

### Backend
- **FastAPI**: Framework web moderno para Python
- **PyMuPDF**: Procesamiento de archivos PDF
- **Requests**: Cliente HTTP para APIs externas
- **Pydantic**: Validación de datos

### Frontend
- **HTML5/CSS3**: Estructura y estilos
- **JavaScript ES6+**: Lógica del cliente
- **Font Awesome**: Iconografía
- **CSS Grid/Flexbox**: Layout responsive

## Instalación y Desarrollo Local

### Prerrequisitos
- Python 3.8+
- pip

### Configuración

1. **Clonar el repositorio**
```bash
git clone <repository-url>
cd dylo_web_app
```

2. **Instalar dependencias**
```bash
pip install -r requirements.txt
```

3. **Ejecutar el servidor de desarrollo**
```bash
cd backend
python -m uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

4. **Acceder a la aplicación**
- Abrir navegador en: `http://localhost:8000`
- API docs disponibles en: `http://localhost:8000/docs`

## Deployment en Vercel

### Configuración Automática

El proyecto está configurado para deployment automático en Vercel:

1. **Conectar repositorio a Vercel**
2. **Vercel detectará automáticamente la configuración**
3. **El deployment se realizará automáticamente**

### Variables de Entorno

No se requieren variables de entorno adicionales ya que las API keys están hardcodeadas en el código (como en el script original).

### Configuración Manual

Si necesitas configurar manualmente:

```bash
# Instalar Vercel CLI
npm i -g vercel

# Hacer deploy
vercel --prod
```

## Uso de la Aplicación

### Flujo de Trabajo

1. **Configurar API Key**: Ingresar la API key de Humand
2. **Cargar Datos**: Cargar carpetas y usuarios desde Redash
3. **Seleccionar Carpeta**: Elegir carpeta de destino
4. **Configurar Opciones**: Prefijo y requisitos de firma
5. **Subir Archivos**: Arrastrar o seleccionar PDFs
6. **Procesar**: Ejecutar el procesamiento automático
7. **Revisar Resultados**: Ver estadísticas y logs

### Características Principales

- **Drag & Drop**: Arrastra archivos PDF directamente
- **Búsqueda de Carpetas**: Filtra carpetas por nombre o ID
- **Vista Previa**: Muestra formato de archivos generados
- **Progreso en Tiempo Real**: Barra de progreso y logs
- **Gestión de Errores**: Manejo robusto de errores
- **Descarga de Logs**: Exporta logs para análisis

## API Endpoints

### GET `/api/folders`
Obtiene las carpetas disponibles desde Redash.

### GET `/api/users`
Obtiene los usuarios con RFC desde Redash.

### POST `/api/upload-documents`
Procesa y sube múltiples archivos PDF.

**Parámetros:**
- `files`: Archivos PDF (multipart/form-data)
- `folder_id`: ID de la carpeta destino
- `api_key`: API key de Humand
- `signature_status`: Estado de firma (PENDING/SIGNATURE_NOT_NEEDED)
- `prefix`: Prefijo opcional para nombres de archivo

### GET `/health`
Endpoint de verificación de salud.

## Limitaciones y Consideraciones

### Vercel
- **Tiempo de ejecución**: Máximo 60 segundos por request
- **Tamaño de archivos**: Límite de 50MB por archivo
- **Memoria**: Límite de 1GB RAM

### Procesamiento
- **Formato PDF**: Solo acepta archivos PDF válidos
- **RFC**: Debe estar presente en el texto del PDF
- **Usuarios**: Requiere mapeo RFC → username en Redash

## Diferencias con la Aplicación Original

### Ventajas de la Versión Web
- ✅ **Acceso universal**: Funciona en cualquier navegador
- ✅ **No requiere instalación**: Sin dependencias locales
- ✅ **Interfaz moderna**: Diseño responsive y atractivo
- ✅ **Hosting en la nube**: Disponible 24/7
- ✅ **Actualizaciones automáticas**: Sin necesidad de redistribuir

### Limitaciones vs Versión Desktop
- ❌ **Configuración de firma**: No incluye selector visual de áreas
- ❌ **Archivos locales**: No guarda archivos procesados localmente
- ❌ **Tiempo de procesamiento**: Limitado por Vercel (60s)

## Soporte y Mantenimiento

### Logs y Debugging
- Los logs se muestran en tiempo real en la interfaz
- Se pueden descargar para análisis posterior
- Errores detallados en la consola del navegador

### Monitoreo
- Endpoint `/health` para verificación de estado
- Métricas disponibles en el dashboard de Vercel

## Contribución

Para contribuir al proyecto:

1. Fork el repositorio
2. Crear una rama para la feature
3. Realizar cambios y tests
4. Crear Pull Request

## Licencia

Este proyecto es de uso interno para DYLO.
