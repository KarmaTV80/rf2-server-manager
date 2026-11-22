# RF2 Server Manager

[English](README.md) · [Italiano](README.it.md) · **Español** · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt.md)

**Descarga:** [última versión](https://github.com/KarmaTV80/rf2-server-manager/releases/latest)

**Apoya el proyecto:** [dona con PayPal](https://www.paypal.com/donate/?business=3T7ZTAXBQY3EN&no_recurring=0&item_name=Sostieni+Karma+TV%3A+progetti+e+canali+YouTube%2C+Instagram%2C+TikTok.+Support+my+projects+and+channels.+Grazie%21+Thanks%21&currency_code=EUR) – la app es gratuita, cada donación ayuda a mantenerla actualizada.

---

Herramienta para Windows que configura e inicia un servidor dedicado de RF2.
No es un producto oficial y no está vinculada a Studio 397 ni a Motorsport Games.

En el primer inicio la app detecta el idioma de Windows: italiano, inglés, español, francés, alemán o portugués. Los demás idiomas pasan a inglés. El botón con la bandera arriba a la derecha lo cambia, y la app recuerda tu elección.

## Requisitos

- Windows 10 u 11 de 64 bits. .NET ya está incluido en el exe.
- Espacio en disco para el servidor y los contenidos.
- Microsoft Edge WebView2 Runtime, solo para el navegador de la pestaña Workshop. Sin él, puedes pegar el ID del Workshop a mano.

El servidor dedicado y SteamCMD no están incluidos: la app puede descargarlos de Valve y Steam con la configuración guiada.

## Primer inicio

1. Abre `RF2ServerManager.exe`. No hace falta instalarlo.
2. Si Windows muestra "Windows protegió su PC", elige **Más información** y luego **Ejecutar de todas formas**. Aparece porque el exe no tiene firma digital.
3. En la configuración guiada elige las carpetas de SteamCMD y del servidor, o deja que la app los descargue.
4. Inicia el servidor una vez: crea sus archivos de configuración. Si Windows pide permiso para el firewall, elige **Permitir**.

## Actualizaciones

Al iniciarse, la app mira en GitHub si hay una versión nueva. Si la hay, abajo en el menú de la izquierda aparece el recuadro **Actualizar ahora**. La app la descarga, comprueba su huella SHA-256 y se vuelve a abrir sola; el servidor, si está encendido, sigue encendido. Debajo del número de versión, **Buscar actualizaciones** repite la comprobación a mano. Si no se puede escribir en la carpeta de la app (por ejemplo dentro de Archivos de programa), descarga la versión nueva desde la [página de versiones](https://github.com/KarmaTV80/rf2-server-manager/releases).

## Contenidos que ya tienes en el juego

No hace falta volver a descargarlos ni copiarlos a mano. La app busca sola la carpeta del juego, que también puedes elegir en el paso 1. Preparar. En el paso 3. Contenido pulsa **Añadir del juego**, selecciona coches y circuitos y pulsa **Copiar al servidor**. El juego solo se lee.

En **Biblioteca** cada contenido muestra su estado: *Listo*, *Por instalar* o *Falta el paquete*, cuando los amigos no pueden descargarlo. El botón de la fila hace lo correcto: instala, copia el paquete del juego o abre el Workshop buscando ese contenido. Los coches y circuitos del evento se eligen en el paso 4. Evento, con **Crear un evento nuevo**.

Los contenidos instalados en el juego sin paquete `.rfcmp` (por ejemplo comprados en una web) aparecen al final de las listas: de ellos se copia al servidor la instalación, y solo podrán entrar los pilotos que ya los tengan, en la misma versión.

Los DLC oficiales comprados funcionan en el servidor: la app copia sola el archivo de desbloqueo que prepara el juego (`ServerUnlock.bin`). Las actualizaciones de los contenidos también se aplican solas.

## Jugar con otras personas

En el router redirige hacia la IP del PC:

| Puerto | Protocolo | Uso |
|---|---|---|
| 54297 | TCP y UDP | Simulación |
| 64297 | TCP | Descarga de archivos por parte de los clientes |
| 64298 y 64299 | UDP | Steam: sin ellos el servidor no aparece en la lista del juego |

**No abras nunca los puertos 5397 y 5398**: controlan el servidor y el juego. Pon siempre una contraseña de acceso y una contraseña de administrador distintas entre sí. El botón **Comprobar red y puertos** del paso 10. Servidor te ayuda a comprobarlo.

### CGNAT, doble router y VPN

Si tu proveedor usa CGNAT (una IP pública compartida entre varios clientes), abrir puertos en el router no sirve: los amigos no llegan al servidor. Desde la versión 1.0.7 **Comprobar red y puertos** te avisa cuando encuentra una dirección CGNAT en el camino hacia internet. También puedes comparar la IP WAN que muestra la página del router con la IP pública que muestra la app: si son distintas, estás detrás de CGNAT o de un segundo router. En ese caso pide a tu proveedor una IP pública, o abre los puertos en los dos routers. Las VPN (Hamachi, ZeroTier y similares) no las gestiona la app.

## Servidor en el mismo PC que el juego

Un PC aparte es lo ideal, pero mucha gente tiene uno solo, y la app está pensada también para ese caso:

- El servidor dedicado es un programa aparte: la app lo instala con SteamCMD en su propia carpeta, nunca dentro de la del juego.
- Juego y servidor usan los dos el puerto 5397 para su interfaz web: antes de cada inicio la app mueve la del servidor al 5398, así no chocan.
- Iniciar el servidor mientras el juego carga ralentiza a los dos: con **Iniciar primero el juego** la app espera a que el juego esté en el menú y luego inicia el servidor sola.
- Para eventos grandes sigue siendo mejor un PC aparte: el servidor no quita recursos al juego.

## Paquetes y DLC de pago

- Los amigos descargan coches, circuitos y eventos solo de la carpeta `Packages` del servidor: cada `.rfcmp` y `.rfmod` tiene que estar ahí, o al entrar reciben un error. La Biblioteca marca lo que falta (*Falta el paquete*) y puede copiarlo del juego, y los eventos creados con la app dejan ahí su `.rfmod` solos.
- Los DLC oficiales de pago solo se abren en el servidor con `ServerUnlock.bin`, que el juego crea en su carpeta `UserData` para el contenido que tienes. La app lo copia en la carpeta `UserData` del servidor antes de instalar contenido y antes de cada inicio. Si el servidor está en otro PC, copia tú ese archivo, y otra vez después de comprar DLC nuevos.

## Antitrampas

En el paso 9. Chat y ping la app puede señalar a los pilotos con vueltas o velocidades imposibles y los saltos de un punto a otro de la pista, comparando a cada uno con los demás de la misma clase. No desconecta a nadie: avisa y escribe todo en el registro de sospechosos (`sospetti.log`), y luego decide quien gestiona el servidor. El servidor no ve dentro del PC de los pilotos, así que encuentra los efectos de las trampas, no los programas.

## Dónde están los datos

- Ajustes y registro: `%AppData%\RF2ServerManager`
- Contraseñas: solo en los archivos de configuración del servidor, que las guarda en texto plano. No van a los perfiles.

## Informar de un problema

Usa **Informar** arriba a la derecha en la app, o **Info → Informar de un problema** (desde la versión 1.0.6). La app muestra el registro ya sin nombre de usuario de Windows, nombres de los pilotos, Steam ID, direcciones IP y mensajes del chat, lo guarda en un archivo de texto y abre en GitHub el [formulario de informes](https://github.com/KarmaTV80/rf2-server-manager/issues/new?template=segnalazione.yml): describe qué pasó y adjunta el archivo. Los informes son públicos y se necesita una cuenta gratuita de GitHub. El botón **Abrir carpeta de registros** está en el paso 1. Preparar.

## Límites conocidos

- La creación de mods y la instalación de paquetes manejan MAS2 y ModMgr en segundo plano, con sus ventanas ocultas: el progreso se lee en el registro de la app. Con "Iniciar la sesión de inmediato" también la ventana del servidor se abre minimizada: se vuelve a abrir desde la barra de tareas de Windows. Una actualización de esas herramientas puede requerir adaptar la app.
- Los contenidos de pago y los paquetes copiados del Workshop pueden no instalarse: la app muestra el error y limpia los archivos.
- Práctica 2 no tiene hora ni duración propias en la configuración del servidor.

## Condiciones de uso

Gratis, también para campeonatos y ligas. No está permitido modificarla, descompilarla, revenderla ni distribuirla desde otros sitios: comparte solo el enlace oficial. Texto completo en `LICENSE.txt` y en la ventana **Acerca de** de la app.

Componentes de terceros: FlaUI y Newtonsoft.Json (licencia MIT), Microsoft WebView2 SDK (licencia de Microsoft), .NET (licencia MIT), fuentes Saira Extra Condensed y Barlow (SIL Open Font License, textos en `Licenze\`).
