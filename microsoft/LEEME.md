# Plan compartido con Microsoft 365 (OneDrive)

Con esto, el panel (`gestion_binapps.html`, publicado en GitHub) deja de guardar en el navegador:

- Cada persona entra con **su cuenta de Microsoft de Binapps** (la del correo). No hay PIN.
- Sus actividades **personales** se guardan en **su propio OneDrive** (carpeta *Aplicaciones › Panel Gestión
  Binapps*): la otra persona no puede abrirlas, porque es Microsoft quien lo controla.
- Las actividades **en conjunto** se guardan en `plan-conjunto.json`, un archivo en el OneDrive de Maye
  (carpeta *Plan de trabajo Binapps*) compartido con Luisa con permiso de edición.
- Si las dos guardan al mismo tiempo, el panel lo detecta y vuelve a leer antes de escribir: no se pisan.

## Paso 1 · Registrar el panel en Microsoft (lo hace un administrador de Microsoft 365, una vez)

1. Entrar a **https://entra.microsoft.com** con una cuenta administradora de Binapps.
2. **Identidad › Aplicaciones › Registros de aplicaciones › + Nuevo registro**.
   - **Nombre:** `Panel Gestión Binapps`
   - **Tipos de cuenta compatibles:** *Solo las cuentas de este directorio organizativo (Binapps)*.
   - **URI de redirección:** plataforma **Aplicación de página única (SPA)** y la dirección
     `https://finanzasmaye.github.io/GestionBinapps-/gestion_binapps.html`
   - **Registrar**.
3. En la página que abre, copiar dos datos (no son contraseñas, se pueden enviar por chat):
   - **Id. de aplicación (cliente)**
   - **Id. de directorio (inquilino)**
4. **Permisos de API › + Agregar un permiso › Microsoft Graph › Permisos delegados**: marcar
   **Files.ReadWrite.All** (User.Read ya viene). **Agregar permisos**.
5. Pulsar **Conceder consentimiento de administrador para Binapps** y confirmar. Debe quedar en verde.

No hace falta crear ningún "secreto" ni certificado: el panel no guarda claves.

## Paso 2 · Poner esos dos datos en el panel

Se pasan a Claude (o se escriben en `gestion_binapps.html`, en `const MS = { clientId: '…', tenantId: '…' }`)
y se sube el archivo a GitHub.

## Paso 3 · Crear el plan conjunto (Maye, una vez)

1. Abrir el panel y **Entrar con Microsoft**.
2. En **Resumen** aparece *Crear el plan conjunto con Luisa Villa*: escribir el correo de Luisa y pulsar
   **Crear plan conjunto**. Se crea el archivo en tu OneDrive y se le comparte con permiso de edición.
3. El panel muestra un **código** (`b!…!…`): pasárselo a Claude para que lo ponga en el panel
   (`MS.conjunto`) y lo suba a GitHub.
4. Pulsar **Subirlas a mi plan** para llevar las actividades que ya tenías en el navegador. Las pendientes
   que dicen "con Luisa Villa" quedan en conjunto; las demás, personales.

## Paso 4 · Luisa

Se le pasa el link `https://finanzasmaye.github.io/GestionBinapps-/gestion_binapps.html`. Entra con su
cuenta de Microsoft y ya ve lo que tienen en conjunto. Lo que ella cree queda en su OneDrive (personal) o
en el plan conjunto si marca **En conjunto**. Si le aparece "Subirlas a mi plan", **no** lo use (serían las
actividades de ejemplo que trae el panel).

## Bueno saber

- **No borrar ni mover** `plan-conjunto.json` ni la carpeta *Plan de trabajo Binapps*: el panel lo busca ahí.
- El archivo conjunto se puede abrir en OneDrive como respaldo (es texto JSON).
- Si Microsoft pide volver a entrar (pasa cada tanto), el panel lo hace solo.
- Para quitarle el acceso a alguien: dejar de compartirle el archivo en OneDrive.
