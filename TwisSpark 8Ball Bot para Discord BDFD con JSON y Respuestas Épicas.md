
# TwisSpark 8Ball Bot para Discord BDFD con JSON y Respuestas Épicas

Comando Bola 8 para tu bot de Discord usando Bot Designer For Discord (BDFD). Incluye respuestas clásicas y una versión caótica, divertida y con actitud al estilo Twis Spark. JSON listo para copiar, mejorar o sparkificar tu bot 

## Codigo 1 : 
Prefix : ¡8ball 

Slash : /8ball (pregunta)

```
$nomention
$reply 
$allowUserMentions[]

$if[$isSlash==true]
$var[question;$message[pregunta]]
$else 
$var[question;$message]
$endif

$jsonParse[{
  "response_normal": ["Sí, definitivamente", "Es cierto","Sin duda","Puedes confiar en ello","Muy probablemente","Las señales apuntan a que sí","Sí","Parece buena idea","Respuesta confusa, intenta de nuevo","Pregunta de nuevo más tarde","Mejor no decirte ahora","No puedo predecirlo ahora","Concéntrate y pregunta otra vez","No cuentes con ello","Mi respuesta es no","Mis fuentes dicen que no","Muy dudoso","No parece ser el momento adecuado"
    \],
    
  "response_twis": ["¡Obvio, y con fuego real del reino de Twis Spark!","Ni lo sueñes, incluso los dragones se ríen de eso","Tal vez… pero solo si bailas bajo la lluvia de pepitas mágicas","Definitivamente sí, y con corona incluida","No, y que los goblins lo sepan también","Las estrellas brillan y dicen que vas a triunfar","Hmm… mejor espera, los fantasmas del castillo no están de humor","¡Sí, y con una explosión de confeti real!","Depende… ¿has saludado al rey loco hoy?","Ni pensarlo, incluso los trolls dicen que es imposible","Sí, y que los unicornios bailen contigo","Tal vez… si robas un caramelo del reino sin que te vean","Claro que sí, con magia, locura y un toque de Twis Spark","No, y los cuervos del castillo están de acuerdo","Sí, y que la trompeta del caos suene fuerte","Hmm… el destino dice que hagas un salto mortal primero","¡Obviamente sí! Pero solo si gritas ‘Twis Spark es el rey loco’","Ni en tus sueños más locos, salvo que invadas mi reino","Tal vez… pero cuidado con los dragones bailarines","Sí, y que todos los pasteles vuelen hasta ti","Definitivamente sí, y que los fuegos artificiales celebren tu victoria!"
    \]
}]



$if[$var[question]!=]
$author[$nickname]
$authorIcon[$authorAvatar]
$title[🎱 Bola mágica de $username[$botID]]
$addField[🎱 Pregunta;$var[question];no]
$addField[🎱 Respuesta;$json[response_twis;$random[0;$jsonArrayCount[response_twis]]] ;no]
$color[#8c52ff]
$else  
$ephemeral 
$description[`👀` Pregúntame algo.]
$color[#d9d9d9]
$endif
```

Video en YouTube 
https://youtu.be/7Y2xuE0mU94?si=NuHF63TrmxMJ32g0

Mi canal 
https://youtube.com/@twis_spark
