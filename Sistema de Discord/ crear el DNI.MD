```
$nomention

$c[ Carga el JSON previo del usuario si existe (para chequear si ya tiene DNI) ]
$jsonParse[$getUserVar[dni;$authorID]]

$c[ Variables que el usuario puede pasar en el mensaje ]
$var[nombre;$message[nombre]]
$var[apellido;$message[apellido]]
$var[nacionalidad;$message[nacionalidad]]
$var[sexo;$toUppercase[$message[sexo]]]  
$var[fecha_nac;$message[fecha_de_nacimiento]]

$c[ Si ya tiene DNI activo → muestra mensaje de error y termina ]
$if[$json[dni;activo]==si]
  $ephemeral
  $color[#FF0000]
  $description[¡$nickname ya tienes un DNI registrado!  
  No puedes crear otro. Usa !ver_dni para verlo o pide a un admin resetearlo.]
  $thumbnail[$authorAvatar]
$else

  $c[ Genera N° de documento (serie) random: Letra A/B/C + 8 dígitos ]
  $var[n_de_documento;$randomText[A;B;C]$random[10000000;99999999]]

  $c[ Fecha de emisión: usa la fecha actual con formato dd-MM-yyyy (ceros incluidos) ]
  $var[fecha_de_emision;$date[dd-MM-yyyy]]

  $c[ RUN (RUT) random realista: 8-9 dígitos + DV random (0-9 o K) ]
  $var[rut;$random[10000000;25999999]-$randomText[0;1;2;3;4;5;6;7;8;9;K]]

  $c[ Calcula fecha de vencimiento: +10 años a la emisión ]
  $var[fecha_vencimiento;$dateAdd[$var[fecha_de_emision];10;year];format:dd-MM-yyyy]

  $c[ Embed principal – diseño épico PLUS Max Ultra Pro ]
  $thumbnail[$authorAvatar]
  $color[#d32f2f]  $c[ Rojo bandera chilena ]
  $title[🪪 CÉDULA DE IDENTIDAD CHILENA – PLUS MAX ULTRA PRO EDITION 2026 🇨🇱]
  $description[## ¡Felicidades, **$nickname**!  
  Tu DNI god-tier ha sido generado en **$serverName[$guildID]** 🔥  
  Comando ejemplo: `!dni nombre:Twis apellido:Spark fecha_de_nacimiento:15-05-2003`]

  $addField[👤 Nombre completo;$var[apellido], $var[nombre];true]
  $addField[⚧ Sexo;$var[sexo];true]
  $addField[🌍 Nacionalidad;$var[nacionalidad];true]

  $addField[🎂 Fecha Nacimiento;$var[fecha_nac];true]
  $addField[🆔 RUN;$var[rut];true]
  $addField[🔢 N° Documento;$var[n_de_documento];true]

  $addField[🗓️ Emisión;$var[fecha_de_emision];true]
  $addField[📆 Vencimiento;$var[fecha_vencimiento];true]

  $addField[🔒 Estado;**VIGENTE** – Edición Especial Ultra Pro God Mode;false]

  $footer[Registro Civil e Identificación – Versión PLUS Max Ultra Pro | @SoyTwisSpark]

  $c[ Guarda todos los datos en el JSON del usuario ]
  $jsonSetString[dni;nombre;$var[nombre]]
  $jsonSetString[dni;apellido;$var[apellido]]
  $jsonSetString[dni;nacionalidad;$var[nacionalidad]]
  $jsonSetString[dni;sexo;$var[sexo]]
  $jsonSetString[dni;fecha_nacimiento;$var[fecha_nac]]
  $jsonSetString[dni;n_de_documento;$var[n_de_documento]]
  $jsonSetString[dni;rut;$var[rut]]
  $jsonSetString[dni;fecha_emision;$var[fecha_de_emision]]
  $jsonSetString[dni;fecha_vencimiento;$var[fecha_vencimiento]]
  $jsonSetString[dni;activo;si]

  $c[ Guarda el JSON completo en la variable de usuario ]
  $setUserVar[dni;$jsonStringify[$json[dni]];$authorID]

$endif 
```