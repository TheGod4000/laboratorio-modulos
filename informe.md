# Laboratorio de Módulos JavaScript: CommonJS vs ES6

## Datos del Estudiante
- **Nombre:** Luis Alberto Godinez Martinez
- **Asignatura:** Desarrollo de Aplicaciones Web
- **Fecha:** 12 Feb 2026
- **Tiempo de desarrollo:** 2 horas

## 1. Comparativa CommonJS vs ES6

| Característica | CommonJS | ES6 Modules (ESM) |
| :--- | :--- | :--- |
| **Sintaxis de importación** | `const mod = require('./mod.js')` | `import mod from './mod.js'` |
| **Sintaxis de exportación** | `module.exports = { ... }` o `exports.fn = ...` | `export const fn = ...` o `export default ...` |
| **Carga (síncrona/asíncrona)** | **Síncrona**. Bloquea la ejecución hasta cargar. | **Asíncrona**. Se puede cargar en paralelo (ideal para red). |
| **Soporte en Node.js** | Nativo e histórico (por defecto en `.js`). | Nativo (requiere `"type": "module"` en `package.json` o `.mjs`). |
| **Soporte en navegador** | **No soportado nativamente** (requiere bundlers). | **Soportado nativamente** usando `<script type="module">`. |
| **Importación dinámica** | Se puede usar `require()` dentro de condicionales o funciones. | Usa la función `import()` que devuelve una **Promesa**. |
| **Alcance del módulo (scope)** | Archivo local (Node.js lo envuelve internamente en una función). | Archivo local, pero impone **Modo Estricto (`"use strict"`)** por defecto y previene filtraciones globales. |
| **Cacheo de módulos** | Se evalúa una vez y devuelve una **copia** estática del valor exportado. | Se evalúa una vez y devuelve una **referencia viva** (de solo lectura) al valor exportado. |

## 2. Análisis de Errores
- **Error 1:** `const { sumar } = require('./calculadora.js');`
  - **Causa/Solución:** Falla si el archivo es ES6 (`ERR_REQUIRE_ESM`). Solución: Usar `import { sumar } from './calculadora.js';`.
- **Error 2:** Mezcla de `export` y `module.exports`.
  - **Causa/Solución:** No se pueden mezclar sistemas modulares en un mismo archivo. Solución: Usar solo sintaxis ES6 o solo CommonJS.
- **Error 3:** `<script src="app.js"></script>` en el navegador.
  - **Causa/Solución:** El navegador no reconoce `import/export` en scripts clásicos. Solución: Añadir `type="module"`.
- **Error 4:** `import * from './modulo.js';`
  - **Causa/Solución:** Falta un identificador. Solución: `import * as alias from './modulo.js';`.

## 3. Respuestas a Reflexión
1. CommonJS es síncrono porque lee del disco duro local (rápido). ES6 es asíncrono para no bloquear la web mientras descarga archivos por red.
2. Usar `"type": "module"` en Node.js unifica la sintaxis entre frontend y backend, facilitando la reutilización de código.
3. El hoisting en ES6 asegura que todas las dependencias de los módulos se resuelvan estáticamente antes de que comience la ejecución del código.
4. Uso `default` para exportar la funcionalidad principal de un archivo, y `named` para exportar librerías de utilidades con múltiples funciones.
5. El `type="module"` aísla el scope de las variables, activa el modo estricto y habilita la sintaxis de importación/exportación en el navegador.

## 4. Conclusiones
El uso de sistemas de módulos es fundamental en el desarrollo moderno de JavaScript para mantener el código organizado, escalable y mantenible. A través de esta práctica, quedó clara la transición histórica del lenguaje: CommonJS resolvió la necesidad inicial de modularidad en el servidor (Node.js), mientras que ES6 Modules (ESM) se estableció como el estándar universal y moderno que unifica el ecosistema. Comprender las particularidades de carga estática vs dinámica, así como las restricciones de seguridad (como los problemas de CORS que previenen los módulos locales), es esencial para estructurar arquitecturas web robustas tanto del lado del cliente como del servidor.