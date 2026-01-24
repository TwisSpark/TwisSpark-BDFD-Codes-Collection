## Comando: !purge / !clear
**Alias sugeridos:** purge, clear, limpiar, borrar  

**Descripción:**  
Elimina una cantidad específica de mensajes recientes en el canal donde se ejecuta el comando. Es una herramienta de moderación rápida para limpiar spam, floods o conversaciones no deseadas.

**Uso:**  
`!purge [cantidad]`  
`!clear [cantidad]`

- Si no se indica ninguna cantidad → borra **100 mensajes** por defecto  
- Máximo permitido por Discord: **100 mensajes** por ejecución  
- Solo usuarios con permisos de **Administrador** pueden usarlo

**Ejemplos:**  
`!purge 50` → Borra los últimos 50 mensajes  
`!purge` → Borra los últimos 100 mensajes  
`!clear 20` → Borra los últimos 20 mensajes

**Características incluidas:**  
- Validación automática: no permite cantidades negativas ni mayores a 100  
- Mensaje de confirmación con contador exacto de mensajes borrados  
- Registro automático en el canal de logs configurado (si existe)  
  - Muestra: moderador, canal afectado, cantidad borrada, fecha y hora  
- El mensaje del comando se autodestruye después de 8 segundos para mantener el canal limpio  
- Colores diferenciados: verde para éxito, rojo/naranja para errores

**Configuración necesaria (una sola vez):**  
Establece el canal de logs con una variable (por ejemplo):  
`$var[canal_logs;123456789012345678]`  
(o usa un comando separado para configurarlo mencionando el canal)

**Resumen en una línea (para embed o lista rápida):**  
`🧹 !purge [cantidad] → Borra hasta 100 mensajes recientes + registra la acción en logs`

```
$nomention
$suppressErrors
$onlyAdmin[No tienes permisos para usar este comando.]
$reply
$allowUserMentions[]

$c[─────── Captura la cantidad escrita por el usuario ───────]
$var[cantidad;$message]

$c[─────── Si no escribió nada → usa 100 por defecto ───────]
$var[cantidad_real;$if[$isNumber[$var[cantidad]]==true] $var[cantidad] $else 100 $endif]

$c[─────── Cambia este número por el ID real del canal ───────]
$var[canal_logs;1463310762662559824] 
  
$c[─────── Bloquea cantidades inválidas ───────]
$if[$var[cantidad_real]<=0]
  $description[❌ La cantidad debe ser mayor a 0.]
  $color[ff5555]
$else

$c[─────── Ejecuta el borrado ───────]
$clear[$var[cantidad_real]]

$c[─────── Mensaje de confirmación ───────]
$description[🧹 **Eliminados $var[cantidad_real] mensaje(s)** con éxito.]
$color[55ff55]
$footer[Por $nickname]
$addTimestamp

$c[─────── Envía log al canal configurado (si existe) ───────]
$if[$channelExists[$var[canal_logs]]==true]
$sendEmbedMessage[$var[canal_logs];;📜 Registro de Purga;;
**Moderador:** $nickname ($authorID)
**Canal:** <#$channelID>
**Mensajes eliminados:** $var[cantidad_real]
**Fecha y hora:** <t:$getTimestamp:F>
;ffffff;;;$serverName[$guildID];$serverIcon;;;yes]
$endif

$c[─────── Limpia el mensaje del comando después de 8 segundos ───────]
$deleteIn[8s]

$endif 
```
