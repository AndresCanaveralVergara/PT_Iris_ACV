# iris-data-challenge

Prueba técnica para el rol de **Líder de Datos**.

Este repositorio es una **plantilla**. Para empezar:

1. Haz clic en **"Use this template" → "Create a new repository"** y crea **tu propio repositorio público** a partir de esta plantilla.
2. Trabaja en **tu** repositorio con buenas prácticas (commits claros y frecuentes) y deja los **cambios finales** en la rama `master`.

## Contenido

- `aws-Resrcs/` — Infraestructura como código (CloudFormation).
- `sql/` — Scripts SQL (SQL Server).
- `spark/` — Job de PySpark y sus fuentes de datos (`spark/datos/`).

## Instrucciones completas

Qué hacer en cada módulo, cómo ejecutarlo, qué entregar y el plazo están en el
**documento de Word que te envió el reclutador**. Guíate por ese documento de principio a fin.

## Entrega

El **enlace de tu repositorio público** (con los cambios finales en `master`) y el **video**, tal
como lo indica el documento.

20-07-2026.

DESARROLLO DE PRUEBA TÉCNICA.

CANDIDATO A LÍDER DE DATOS/DATA MANAGEMENT: ANDRÉS CAÑAVERAL VERGARA.

1. ¿Qué herramientas de IA usé?
Utilicé Claude (Anthropic), en su versión en la nube a través de la interfaz de chat, como asistente principal durante todo el desarrollo de la prueba, tanto para el Módulo 2 (SQL) como para el Módulo 3 (PySpark).

2. ¿En qué partes usé IA y para qué?
Usé la IA de dos formas principales. Primero, como apoyo para diagnosticar los errores de cada script; le pasé el contexto del problema (por ejemplo, "el % de mora da valores imposibles" o "el job se queda en un bucle infinito") y trabajamos juntos identificando la causa raíz línea por línea antes de tocar el código. En segundo lugar, como apoyo para redactar y estructurar las correcciones (la limpieza de montos con formato colombiano, la normalización de segmentos con casing inconsistente, el join de TRM real por fecha, y la reescritura del job para eliminar los antipatrones de rendimiento).
Vale la pena mencionar que en ningún caso permití que la IA tomara decisiones de negocio por mí toda vez que cada corrección la validé ejecutándola yo mismo en OneCompiler (SQL) y en Google Colab (PySpark), revisando los resultados fila por fila contra los datos originales antes de aceptarla.

3. ¿Por qué la usé ahí y qué me aportó?
La usé principalmente para acelerar el diagnóstico técnico y evitar atascrme en detalles de sintaxis de SQL y PySpark que no manejo de memoria con la misma fluidez en ambos lenguajes al mismo tiempo. Me aportó velocidad para plantear hipótesis de por qué fallaba cada script, y me obligó a verificar cada hipótesis con evidencia real (corriendo el código) antes de aplicarla, en lugar de asumir que la primera explicación era la correcta. Además, fue de gran aporte para revalidar conocimientos técnicos como el "control de excepciones".

4. Un ejemplo de algo que la IA me dio y tuve que corregir o verificar.
Al normalizar el campo segmento del job de PySpark, la primera propuesta de la IA fue usar la función initcap() para unificar mayúsculas y minúsculas (por ejemplo, pasar "premium" a "Premium"). Al ejecutarlo, me di cuenta de que el segmento "PYME" (una sigla) quedaba mal transformado como "Pyme" en lugar de "PYME", lo que habría vuelto a generar el mismo bug original de segmentos que no coinciden con la lista esperada. Lo noté al revisar el show() del DataFrame después de aplicar la normalización y comparar visualmente contra los valores originales del CSV. La corrección fue reemplazar initcap() por un mapeo explícito de los 4 valores válidos del negocio, comparando siempre en mayúsculas.
