# Ojo de Sauron
> Sistema híbrido en C y Assembly para captura de pantalla simulada con fines de investigación en seguridad.

## Descripción
Desarrollé un demostrador técnico que integra lenguaje de alto nivel (C) con ensamblador (x86-64) para interactuar con el sistema operativo a bajo nivel. El propósito principal es educativo: mostrar cómo se puede acceder al framebuffer, realizar llamadas al sistema y capturar la actividad de la pantalla sin depender de librerías intermedias. El proyecto enfatiza la transparencia operativa, el control directo del hardware y la conciencia sobre riesgos de seguridad.

## Stack / Arquitectura
El proyecto sigue una arquitectura híbrida donde la lógica de control reside en C y las rutinas críticas (captura de pantalla, acceso a memoria de video, invocación de syscalls) se escriben en Assembly. Esta separación permite:
- **Optimización manual** en las secciones sensibles a latencia.
- **Reutilización** del código de alto nivel para la gestión de errores y flujo principal.
- **Demostración clara** de la interfaz entre lenguajes mediante la convención de llamadas del sistema (System V AMD64).

**Componentes principales:**
- `main.c`: orquesta la captura, manejo de argumentos y salida.
- `screencap.asm`: rutina en ensamblador que lee el framebuffer (simulado o real mediante `/dev/fb0`).
- `syscall.asm`: macros y wrappers para llamadas al sistema (`open`, `read`, `write`).

## Implementación
Se utiliza **NASM** como ensamblador y **GCC** para enlazar el objeto resultante con el código C. La comunicación entre ambos lenguajes se realiza a través de la pila y registros siguiendo el ABI estándar. La captura de pantalla se implementa de forma **simulada** (lee un archivo de prueba o un dispositivo de framebuffer virtual) por razones éticas y de portabilidad, pero el código está preparado para interactuar con hardware real bajo autorización explícita.

## Estado actual
El prototipo funciona completamente en entornos Linux (x86_64) como prueba de concepto:
- Captura de un bloque de píxeles y volcado a un archivo PPM.
- Demostración de llamadas al sistema desde Assembly.
- Ejemplo de integración compilable con `make`.
- Documentación de las técnicas empleadas y advertencias de uso ético.

## Proyección
La evolución del sistema podría incluir:
- Soporte para diferentes profundidades de color y formatos de píxel.
- Captura en tiempo real con compresión básica.
- Detección de cambios en pantalla (diferencias entre frames).
- Versión multiplataforma (Windows usando GDI o DirectX).
- Integración con herramientas de monitoreo educativo (con permiso explícito).

## Extra
- El nombre y la estética están inspirados en el **Ojo de Sauron** de *El Señor de los Anillos*, como metáfora de la vigilancia y el análisis profundo del sistema.
- El código Assembly está comentado línea por línea con fines didácticos.

## Paleta de colores (banner y branding)
- `#0a0a0a` (negro absoluto)
- `#ffffff` (blanco para texto principal)
- `#ff3300` / `#ffaa00` (acentos del “fuego” del ojo, usados en el degradado del banner)

## Fuentes
- **Títulos**: `'Segoe UI', Arial, Helvetica, sans-serif` (con espaciado)
- **Código**: `'Fira Code', 'Courier New', monospace`
