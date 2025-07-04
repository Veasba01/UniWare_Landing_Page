# Configuración de EmailJS para el Formulario de Contacto

## Paso 1: Crear una cuenta en EmailJS

1. Ve a [EmailJS](https://www.emailjs.com/)
2. Crea una cuenta gratuita (incluye hasta 200 emails por mes)
3. Confirma tu email

## Paso 2: Configurar el servicio de email

1. Ve a la sección **Email Services** en tu dashboard
2. Haz clic en **Add New Service**
3. Selecciona **Gmail** como proveedor
4. Autoriza EmailJS para usar tu cuenta de Gmail
5. Copia el **Service ID** que se genera (ejemplo: `service_xyz123`)

## Paso 3: Crear un template de email

1. Ve a la sección **Email Templates**
2. Haz clic en **Create New Template**
3. Usa este template:

**Subject:** Nuevo contacto desde UniWare - {{nombre}}

**Content:**
```
Has recibido un nuevo mensaje desde el formulario de contacto de UniWare:

Nombre: {{nombre}}
Email: {{email}}
Negocio: {{negocio}}
Necesidad: {{necesidad}}

Mensaje:
{{mensaje}}

---
Este email fue enviado desde el formulario de contacto de UniWare Landing Page.
```

4. Guarda el template y copia el **Template ID** (ejemplo: `template_abc456`)

## Paso 4: Obtener tu Public Key

1. Ve a la sección **Account** → **General**
2. Copia tu **Public Key** (anteriormente llamado User ID)
3. NO uses la Private Key, solo la Public Key

## Paso 5: Configurar el código

Abre el archivo `src/components/ContactSection.astro` y reemplaza:

```javascript
emailjs.init('TU_PUBLIC_KEY_AQUI'); // Reemplaza con tu Public Key

// Y en el envío del formulario:
const result = await emailjs.sendForm(
  'TU_SERVICE_ID_AQUI',    // Reemplaza con tu Service ID
  'TU_TEMPLATE_ID_AQUI',   // Reemplaza con tu Template ID
  form
);
```

Por tus valores reales:

```javascript
emailjs.init('tu_public_key_real'); // Tu Public Key real

// Y en el envío del formulario:
const result = await emailjs.sendForm(
  'service_xyz123',    // Tu Service ID real
  'template_abc456',   // Tu Template ID real
  form
);
```

## Paso 6: Probar el formulario

1. Guarda los cambios
2. Ejecuta tu proyecto con `npm run dev`
3. Ve a la sección de contacto
4. Llena el formulario y envíalo
5. Revisa tu Gmail para ver si llegó el correo

## Notas importantes:

- Los nombres de los campos en el formulario HTML deben coincidir con las variables en el template (`{{nombre}}`, `{{email}}`, etc.)
- EmailJS tiene un límite gratuito de 200 emails por mes
- Los correos pueden tardar algunos minutos en llegar
- Revisa la carpeta de spam si no ves el correo

## Troubleshooting:

Si no funciona, revisa:

1. La consola del navegador para errores
2. Que los IDs sean correctos
3. Que el servicio de Gmail esté autorizado
4. Que los nombres de campos coincidan con el template

## Variables disponibles en el template:

- `{{nombre}}` - Nombre completo del cliente
- `{{email}}` - Email del cliente
- `{{negocio}}` - Nombre del negocio
- `{{necesidad}}` - Tipo de servicio requerido
- `{{mensaje}}` - Mensaje adicional del cliente
