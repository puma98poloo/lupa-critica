# Entre líneas

App educativa en español para explorar un catálogo ampliado de sesgos y falacias. Incluye búsqueda, filtros, selección aleatoria, ejemplos, artículos enlazados, clips de YouTube con posición de reproducción y un analizador contextual opcional con IA.

## Requisitos

- Node.js 18 o posterior (usa `fetch` nativo; no requiere paquetes externos).
- Una clave de API de OpenAI para activar el análisis contextual. Sin clave, el servidor usa patrones locales básicos y explica sus límites.

## Inicio

1. (Opcional) Copia `.env.example` como `.env` y añade una clave en `OPENAI_API_KEY` para análisis contextual con IA.
2. Ejecuta `node server.js`.
3. Abre `http://localhost:4173`.

Puedes elegir otro modelo compatible con Structured Outputs configurando `OPENAI_MODEL` (el valor inicial es `gpt-6-astra`). La clave solo se lee en el servidor y no se envía al navegador. Sin clave, las coincidencias de texto se analizan con reglas locales simples; este modo puede omitir casos y producir falsos positivos.

## Publicación en Render

El archivo `render.yaml` configura un servicio web público gratuito con health check. Importa este proyecto en un repositorio Git conectado a Render y elige **New > Blueprint**. El diccionario y el analizador local funcionan sin clave; para análisis contextual, configura `OPENAI_API_KEY` como secreto en el panel de Render. No subas `.env` al repositorio.

## Privacidad

Al analizar con IA, el texto se envía a la API de OpenAI desde el servidor para generar la respuesta. Sin clave, el análisis local se hace en el servidor y el texto no se envía a un proveedor de IA. La app no conserva el texto en el servidor. El navegador guarda hasta quince análisis en `localStorage` de ese dispositivo; el control **Historial** permite borrarlos. Los datos no se sincronizan.

## Alcance y fuentes

Las detecciones son sugerencias educativas y no verifican hechos ni diagnostican estados mentales. Las fichas separan ejemplos prácticos de casos y hallazgos documentados. Los enlaces a artículos se abren en una pestaña nueva. Los enlaces de YouTube incluyen una posición de inicio; los clips y cortes disponibles pueden cambiar por decisión de quien publica o por región.

La API usa Responses con Structured Outputs para exigir una respuesta JSON compatible con el formato del analizador. Consulta la [guía oficial de Structured Outputs](https://developers.openai.com/api/docs/guides/structured-outputs?api-mode=responses).
