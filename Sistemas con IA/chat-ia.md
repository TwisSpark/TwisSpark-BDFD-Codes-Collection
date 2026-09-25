
# 🤖 Comando de IA con Groq para BDFD

Comando de inteligencia artificial para **Bot Designer For Discord** usando la API gratuita de **Groq**.

---

## 🔑 Paso 1: Obtén tu API Key de Groq (gratis)

1. Entra en → [https://console.groq.com](https://console.groq.com)
2. Inicia sesión o crea una cuenta (puedes usar Google o tu email)
3. En el menú lateral, haz clic en **API Keys**
4. Pulsa el botón **Create API Key**
5. Dale un nombre (por ejemplo: `BDFD`) y copia la key  
   *(empieza por `gsk_...`)*

> ⚠️ **Importante:** Guárdala bien, solo se muestra una vez.

---

## 🔒 Paso 2: Guarda la API Key de forma segura

**No pongas la API key directamente en el código.**  
Es mucho más seguro guardarla en una variable de BDFD.

### Cómo hacerlo:

1. Ve a tu bot en BDFD → **Variables**
2. Crea una nueva variable con este nombre:  
   `GROQ_KEY`
3. En el valor, pega tu API key de Groq
4. Guarda los cambios

Así tu key queda protegida y no se ve en el código.

---

## 📜 Código del comando

Copia y pega el siguiente código en tu comando de BDFD:

```bdscript
$nomention
$reply
$allowUserMentions[]
$botTyping

$onlyIf[$message!=;❌ Escribe algo después del comando.
Ejemplo: `!ai Hola, ¿cómo estás?`]

$httpAddHeader[Content-Type;application/json]
$httpAddHeader[Authorization;Bearer $getVar[GROQ_KEY]]
$httpPost[https://api.groq.com/openai/v1/chat/completions;{
  "model": "openai/gpt-oss-20b",
  "messages": [
    {
      "role": "system",
      "content": "Eres un asistente útil y amigable. Responde siempre en español de forma clara y concisa."
    },
    {
      "role": "user",
      "content": "$message"
    }
 \],
  "max_tokens": 800,
  "temperature": 0.7
}]

$if[$httpStatus==200]
  $title[🤖 Respuesta de IA]
  $description[$httpResult[choices;0;message;content]]
  $color[#F55036]
  $footer[Groq • Modelo: gpt-oss-20b]
$else
  $title[❌ Error]
  $description[No se pudo obtener respuesta.
**Status:** `$httpStatus`]
  $color[#FF0000]
$endif
```

---

## 🧠 Modelos disponibles en Groq

Puedes cambiar el modelo en la línea `"model": "..."` por cualquiera de estos:

| Modelo                    | Descripción                  | Recomendado |
|---------------------------|------------------------------|-------------|
| `openai/gpt-oss-20b`      | Rápido y equilibrado         | ✅ Sí       |
| `openai/gpt-oss-120b`     | Más inteligente              | Mejor calidad |
| `qwen/qwen3.8-27b`        | Excelente en español         | Muy bueno   |
| `qwen/qwen3.6-27b`        | Alternativa sólida           | Buena       |

---

## 📌 Notas

- El límite gratuito de Groq es aproximadamente **30 requests por minuto** y **1000 por día**.
- No se necesita tarjeta de crédito.
- El comando responde en español por defecto.

---

## 📄 Licencia

Este código es de uso libre. Puedes modificarlo y usarlo en tus bots.
