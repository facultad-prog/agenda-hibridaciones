# Agenda de Hibridaciones — Facultad de Derecho

Aplicación web institucional para consultar y administrar las actividades híbridas de la Facultad de Derecho.

## Arquitectura elegida

- **Página:** HTML, CSS y JavaScript, sin compilación.
- **Publicación:** GitHub Pages gratuito.
- **Datos:** Cloud Firestore de Firebase, plan Spark gratuito.
- **Acceso de administración:** Google, limitado a `facultad@derecho.uncu.edu.ar`.
- **Consulta:** pública, sin iniciar sesión.
- **Importación inicial:** archivo `.ics` exportado desde Google Calendar.

El proyecto ya contiene la configuración del proyecto Firebase `agenda-hibridaciones-derecho`. La clave web incluida en `config.js` es una identificación pública del proyecto; la modificación de los datos está protegida por las reglas de Firestore.

## Funciones incluidas

- Semana actual automática y navegación entre semanas.
- Vista mensual; en celular se transforma en una lista vertical legible.
- Agenda de lunes a sábado, sin domingos.
- Cierre de agenda el 28 de diciembre de 2026.
- Feriados marcados: 12 de octubre, 23 de noviembre, 7 y 8 de diciembre.
- Tarjetas compactas con día, horario, actividad y aula; el resto se despliega.
- Botones para abrir o copiar el enlace.
- Carga manual, edición, duplicación y eliminación.
- Actividades únicas, semanales o cada 15 días.
- Importación inicial desde Google Calendar mediante `.ics`.
- Campo de grabación.
- Tipografía Montserrat, color `#014a7d` y logo institucional.

## Estructura

```text
agenda-hibrida-derecho/
├── assets/
│   └── logo-fd-blanco.png
├── firebase/
│   └── firestore.rules
├── .nojekyll
├── index.html
├── styles.css
├── app.js
├── config.js
└── README.md
```

## Publicar en GitHub Pages

1. Ingresar en GitHub y crear un repositorio público llamado `agenda-hibrida-derecho`.
2. Dentro del repositorio, elegir **Add file → Upload files**.
3. Subir **el contenido de esta carpeta**, no el archivo ZIP: `index.html`, `app.js`, `styles.css`, `config.js`, `.nojekyll` y las carpetas `assets` y `firebase`.
4. Presionar **Commit changes**.
5. Abrir **Settings → Pages**.
6. En **Build and deployment**, seleccionar **Deploy from a branch**.
7. Elegir la rama `main`, la carpeta `/ (root)` y presionar **Save**.
8. Esperar unos minutos. GitHub mostrará una dirección similar a `https://USUARIO.github.io/agenda-hibrida-derecho/`.

## Autorizar GitHub Pages en Firebase

Este paso habilita el botón **Administrar agenda** en el sitio publicado.

1. Copiar únicamente el dominio de la dirección de GitHub, por ejemplo `USUARIO.github.io` (sin `https://` y sin `/agenda-hibrida-derecho/`).
2. En Firebase abrir **Authentication → Configuración → Dominios autorizados**.
3. Presionar **Agregar dominio**.
4. Pegar `USUARIO.github.io` y guardar.

## Cargar una actividad

1. Abrir el enlace público de la agenda.
2. Presionar **Administrar agenda**.
3. Ingresar con la cuenta `facultad@derecho.uncu.edu.ar`.
4. Presionar **+ Cargar actividad**.
5. Completar fecha, horario, actividad, Secretaría, responsable, aula, plataforma, cuenta, enlace, grabación y observaciones.
6. En **Repetición**, elegir **No se repite**, **Todas las semanas** o **Cada 15 días**. Para una repetición, indicar hasta qué fecha debe generarse.
7. Presionar **Guardar actividad**.

No se edita ningún archivo para el uso cotidiano.

## Editar, duplicar o eliminar

1. Ingresar como responsable.
2. Desplegar la tarjeta de una actividad.
3. Elegir **Editar**, **Duplicar** o **Eliminar**.

Al duplicar, la copia se prepara automáticamente para la semana siguiente. Se puede modificar la fecha antes de guardarla.

## Importación inicial desde Google Calendar

### Exportar el calendario

1. Abrir Google Calendar desde una computadora.
2. Entrar en **Configuración → Importar y exportar**.
3. En **Exportar**, presionar **Exportar**.
4. Descomprimir el archivo `.zip` descargado y localizar el archivo `.ics` del calendario correspondiente.

### Importar en la agenda

1. Ingresar en la agenda con la cuenta responsable.
2. Presionar **Importar calendario**.
3. Seleccionar el archivo `.ics`.
4. Completar los datos comunes que no estaban en Calendar: Secretaría, responsable, plataforma, cuenta, grabación y observaciones.
5. Presionar **Importar actividades**.

La aplicación toma automáticamente el título, la fecha, el horario, la ubicación y los enlaces reconocibles. Evita volver a importar el mismo evento si se usa nuevamente el mismo archivo.

## Probar los ejemplos

Agregar `?demo=1` al final de la dirección publicada, por ejemplo:

```text
https://USUARIO.github.io/agenda-hibrida-derecho/?demo=1
```

Esta modalidad muestra tres actividades de ejemplo y permite probar carga, repetición, edición, duplicación y eliminación en ese navegador, sin modificar la base real.

## Seguridad

La copia exacta de las reglas está en `firebase/firestore.rules`. Las reglas permiten la lectura pública de la colección `actividades` y solo permiten crear, modificar o eliminar cuando Firebase verifica el correo `facultad@derecho.uncu.edu.ar`.
