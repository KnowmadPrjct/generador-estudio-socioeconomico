# Generador de Estudio Socioeconómico

Una herramienta de un solo archivo HTML para generar plantillas en blanco de estudio socioeconómico listas para imprimir. Las llena a mano el profesional durante la entrevista o visita domiciliaria.

## Cómo abrirlo

Abre `generador-estudio-socioeconomico.html` directamente en Chrome, Firefox o Edge. No necesita servidor, instalación ni conexión a internet después de la primera carga de tipografías.

Para usarlo sin ninguna conexión de red: abre el archivo, espera a que carguen las fuentes una vez, e imprímelo. Las fuentes se sirven desde Google Fonts; si no hay internet, el documento imprime con el tipo de sistema alternativo (Arial/sans-serif), que es completamente legible.

## Cómo compartirlo

**Como archivo:** comparte `generador-estudio-socioeconomico.html` por correo, WhatsApp o Drive. El destinatario lo abre con doble clic.

**Como URL pública:** sube el archivo a cualquier servicio de hosting estático:
- [GitHub Pages](https://pages.github.com/) — sube a un repositorio público, activa Pages, listo.
- [Netlify Drop](https://app.netlify.com/drop) — arrastra la carpeta.
- [Cloudflare Pages](https://pages.cloudflare.com/) — conecta el repositorio o sube directo.

No requiere base de datos ni back-end.

## La regla de no persistencia

**Esta herramienta no guarda nada en el navegador — por diseño.**

El formulario recopila ingresos del hogar, condiciones de salud y composición familiar de personas en situación de vulnerabilidad. Guardar esos datos en `localStorage`, cookies u otro almacenamiento del navegador los dejaría visibles a quien use el mismo equipo después. Por eso no existe ninguna función de guardado automático.

El flujo correcto:
1. Generar la plantilla.
2. Imprimir o guardar como PDF desde el diálogo de impresión del navegador.
3. El archivo queda en el equipo del profesional. La herramienta no retiene nada.

Si necesitas verificarlo: `Select-String -Path .\generador-estudio-socioeconomico.html -Pattern 'localStorage|sessionStorage|indexedDB|document\.cookie'` debe devolver solo las líneas de comentario que mencionan la regla.

## Cómo funciona la configuración de marca

El panel **"Personalizar marca"** (colapsado por defecto, en la parte inferior del panel izquierdo) permite:

- Agregar logo, subtítulo, color de acento y líneas de pie de página.
- Exportar toda esa configuración — incluido el logo como base64 — a un archivo `.json`.
- Importar ese archivo en cualquier computadora para restaurar la configuración exacta.

**Flujo de distribución recomendado:**
1. Un coordinador o jefa de departamento configura la marca una vez.
2. Exporta `configuracion-marca.json`.
3. Envía ese archivo junto con `generador-estudio-socioeconomico.html` al equipo.
4. Cada integrante importa la configuración y genera desde su propia máquina.

No se requiere cuenta, servidor ni sincronización.

## Cómo agregar una jurisdicción

Todas las jurisdicciones viven en el objeto `JUR` dentro del `<script>` del archivo. Para agregar una:

1. Abre `generador-estudio-socioeconomico.html` en un editor de texto.
2. Localiza el objeto `JUR` (búsca `var JUR = {`).
3. Agrega una entrada nueva siguiendo exactamente la estructura de las existentes. Cada jurisdicción tiene:
   - `name` — nombre visible
   - `idDoc` — etiqueta del documento de identidad en `es` y `en`
   - `licenseLabel` — etiqueta de la cédula/colegiatura en `es` y `en`
   - `currency` — símbolo de moneda
   - `health` — arreglo de opciones del sistema de salud en `es` y `en`
   - `educ` — arreglo de niveles educativos en `es` y `en`
   - `docs` — lista de documentos requeridos en `es` y `en`
   - `privacy` — texto del aviso de privacidad con la ley aplicable en `es` y `en`
4. Agrega la opción correspondiente en el `<select id="jurisdiction">` del HTML.

Agregar un país es edición de datos, no de lógica.

## Salida bilingüe

El selector de idioma (Español / English / Bilingüe) es independiente del selector de jurisdicción. Un trabajador social en San Diego puede generar un formulario en español con convenciones de EE.UU., o un resumen en inglés de un estudio bajo normativa mexicana.

El modo **Bilingüe** muestra cada etiqueta con el término en español y debajo el término en inglés en letra más pequeña — un solo formulario que ambas partes pueden leer.

El inglés es una **traducción del mismo instrumento**, pensada para hogares bilingües y coordinación transfronteriza. No adapta el formato a convenciones de agencias estadounidenses (eso sería un preset de jurisdicción distinto con su propio mapa de secciones).

## Imprimir

Usa **Imprimir / PDF** en la barra de herramientas o Ctrl+P. El documento está diseñado para A4 y Carta; puedes cambiar el tamaño en el diálogo de impresión del navegador.

Para mejor resultado en Chrome: desactiva "Encabezados y pies de página" del navegador (el documento ya incluye los suyos) y deja "Gráficos de fondo" desactivado — el diseño es legible sin fondos de color.

## Descargo de responsabilidad

Los presets de jurisdicción reducen el trabajo de adaptación pero no eliminan la responsabilidad profesional. Verifica y adapta apartados, referencias legales, documentos requeridos y terminología según la normativa específica de tu país, estado/comunidad e institución antes de darle uso oficial.
