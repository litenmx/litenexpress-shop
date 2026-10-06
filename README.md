# Liten Express — configuración de sitio público

Dominio público único:
litenexpress.shop

## Cambios de seguridad y confianza

- Se eliminó del sitio público el enlace a un portal administrativo/login alojado en otro dominio.
- El archivo CNAME contiene un solo dominio.
- Se eliminaron del frontend público el nombre completo del titular, RFC y folios administrativos que no son necesarios para la experiencia pública.
- El cotizador no solicita contraseñas, tarjetas, CVV, cuentas bancarias ni credenciales.
- Se eliminaron dependencias visuales externas de Google Fonts.
- La respuesta del backend se procesa con creación de nodos DOM y `textContent`, evitando inyectar directamente datos del servidor con `innerHTML`.
- Se agregaron validaciones de código postal, texto, peso y dimensiones.
- La llamada al backend usa `credentials: omit`, caché desactivada, política de referer restrictiva y timeout.
- Se agrega una política CSP básica desde HTML.
- Los enlaces externos abren con `noopener noreferrer`.
- Se mantienen solo dos integraciones comerciales visibles: mapa de sucursal y WhatsApp.

## Dominio / DNS

Este proyecto está preparado para tener un único dominio público: `litenexpress.shop`.

Si antes existía otro dominio:
1. No lo uses como alias que apunte de regreso a `litenexpress.shop`.
2. No configures redirecciones recíprocas entre dominios.
3. No pongas el dominio antiguo en el archivo `CNAME`.
4. En GitHub Pages, el archivo `CNAME` de una publicación desde rama debe contener un solo dominio y únicamente el nombre del dominio.
5. Configura el dominio personalizado en GitHub Pages antes de terminar la configuración DNS.
6. Evita registros DNS comodín (`*`) y revisa que no existan subdominios abandonados que apunten a servicios que ya no controlas.
7. Activa HTTPS en GitHub Pages y comprueba que el dominio verificado sea `litenexpress.shop`.

Consulta oficial de GitHub:
https://docs.github.com/es/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

## Backend

El frontend consulta:
https://liten-express.onrender.com/api/cotizar-publico

El backend debe:
- aceptar únicamente los campos necesarios para cotizar;
- no pedir credenciales desde el frontend público;
- no guardar nombres, teléfonos, identificaciones o datos bancarios en los registros de la API;
- aplicar rate limiting y validación del lado del servidor;
- validar `Origin`/CORS para aceptar solo `https://litenexpress.shop` (y, durante la migración, el dominio de pruebas estrictamente necesario);
- devolver JSON con una estructura estable;
- no devolver HTML o JavaScript dentro de `servicios`;
- mantener las credenciales de operadores en un sistema separado del endpoint público de cotización.

## Estructura

- `index.html` — página pública y cotizador
- `quienessomos.html` — información del negocio
- `terminos.html` — términos comerciales
- `privacidad.html` — aviso de privacidad
- `CNAME` — dominio único
- `README.md` — estas instrucciones

## Importante

Ningún cambio de HTML puede garantizar que un proveedor externo jamás marque o suspenda un dominio. La meta de esta versión es que el sitio sea coherente con un negocio legítimo, transparente y de bajo riesgo: un solo dominio, sin suplantación, sin captación de credenciales, sin pagos ocultos y con una finalidad pública claramente explicada.

Ante un falso positivo de un proveedor, conserva evidencia real de propiedad del dominio, identidad comercial y operación física para el proceso de revisión correspondiente.
