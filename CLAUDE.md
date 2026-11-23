# Práctica vertedero – Cantera de Penyalba (Pego)

Trabajo de la asignatura SJN002 *Aprovechamiento y valorización de residuos* (Máster en Eficiencia Energética y Sostenibilidad, UJI). Lo hacen Marc y Gema; ambos hacen commits. Todo en **español** (el docx tiene el idioma fijado a es-ES).

## Enunciado ([captura_enunciado.png](captura_enunciado.png))

1. Buscar una zona apta para el vertido (https://visor.gva.es/visor/)
2. Establecer el perímetro del vertedero, profundidad y volumen aproximado
3. En función de la zona de gestión, calcular los habitantes equivalentes a los que se dará servicio
4. Calcular la vida útil del vertedero
5. Diseñar la red de chimeneas de evacuación de biogás
6. Diseñar la red de tuberías de evacuación del lixiviado
7. A partir del método de GUMBEL, dimensionar los canales perimetrales de evacuación de pluviales

Cada punto del enunciado es un apartado de la memoria y una hoja del Excel con el mismo número.

## Archivos

| Archivo | Qué es |
|---|---|
| [Vertedero_calculos.xlsx](Vertedero_calculos.xlsx) | Cálculos. Hojas `1_Ubicacion` … `7_Canales`, `Gumbel`, `Clima_AEMET`, `Resumen`. Celdas amarillas con texto azul = datos de entrada; el resto, fórmulas enlazadas entre hojas. Lleva capturas pegadas (imágenes) en varias hojas. |
| [Vertedero_memoria.docx](Vertedero_memoria.docx) | Memoria entregable: apartados 1-7 + Bibliografía [1]-[12]. Tablas con columnas «Concepto / Valores (Unidades)», figuras y tablas con pie numerado automático («Figura .», «Tabla .» son campos SEQ, no texto roto). |
| [diagramas/](diagramas/) | `diagrama_biogas.png` (malla al tresbolillo, 171 chimeneas) y `diagrama_lixiviados.png` (espina de pez, DN 500 + 57 drenes DN 200). Van insertados en la memoria. |
| `Tema 8.pptx.pdf` | Apuntes del tema de vertederos (Gallardo y Colomer, UJI). **Es la referencia del método que espera el profesor** (Gumbel con tabla μn/σn, canales con C = 1, b = 2h, Manning). Ref. [12]. |
| `BOE-A-2020-7438-consolidado.pdf` | RD 646/2020 de vertederos. Ref. [11]. |
| `5_2ic_fom_consolidada_norma.pdf` | Instrucción 5.2-IC de drenaje superficial (Fomento). De aquí sale n de Manning = 0,015 del hormigón. Aún no está citada en la bibliografía. |
| [rescate_b8ba7bb/](rescate_b8ba7bb/) | Copia de la memoria del commit `b8ba7bb` («graficas cambiadas», de Gema) y sus imágenes extraídas, guardada como respaldo. No es la versión de trabajo. |

## Valores clave actuales (para comprobar coherencia Excel ↔ memoria)

- Superficie 236.425 m² (≈ 23,6 ha), perímetro ≈ 2.372 m, profundidad 35 m (casi dos curvas de 20 m del visor GVA), volumen ≈ 8,27 Mm³.
- Población A1 Marina Alta (padrón 2025, ARGOS) 198.258 hab; residuos 2025 98.969 t → 1,37 kg/hab·día; rechazo a vertedero 38,95 % → ≈ 38.550 t/año.
- Densidad 0,9 t/m³ → 7,45 Mt. Crecimiento g ≈ 2,1 % (CAGR 2023-2025). Vida útil ≈ 193 años sin crecimiento, ≈ 78 años con n = ln(1 + g·C/R0)/ln(1 + g).
- Biogás: R = 25 m, tresbolillo s = 2R·cos30º ≈ 43 m, 146 teóricas, **171 colocadas** (contadas en el diagrama).
- Lixiviados: balance P_EM = P_T − E_T ± E_C − Cc + H_i (guía IHOBE). P_T 746 mm, ETP Thornthwaite 1.086 mm, lluvia útil 263 mm, escorrentía 45 %, H_i 20 %, Cc 0,30 → ≈ 29.000 m³/año. Punta con Pd de Gumbel en 24 h → 0,37 m³/s, v = 2 m/s → colector DN 500; drenes DN 200 cada 20 m (57 × 81 m + 730 m ≈ 5.350 m). Balsa = 2 × 32.300 ≈ 64.600 m³ (MITECO).
- Gumbel: 20 años (2006-2025; AEMET 8057C Pego desde 2010, 2006-2009 con CERRA/Open-Meteo), x̄ 101,2 mm, s 32,8 mm, μn 0,5236, σn 1,0628, F = 0,995 → T = 200 años, **Pd = 248 mm**.
- Canales: Pd en 1 h, C = 1, Q = I·A ≈ 16,3 m³/s → 8,15 m³/s por canal (norte y sur). v = 3 m/s, b = 2h → h 1,17 m, b 2,33 m; Manning n = 0,015 → S ≈ 0,42 % < 0,5 %. Adoptado 2,4 × 1,2 m + 0,3 m de resguardo.

## Forma de trabajar

- **Excel y memoria van siempre juntos**: si cambia un dato o un método en el Excel, actualizar el apartado, las tablas y las cifras del texto de la memoria (y el `Resumen`, y los diagramas si cambian longitudes o unidades). Comprobar que los números coinciden.
- Editar con Python (`openpyxl` para el xlsx, `python-docx` para el docx; ambos instalados). En Windows usar `python -X utf8` para que no falle la salida por consola.
  - openpyxl **no recalcula** fórmulas: tras modificar el Excel, los valores cacheados quedan vacíos hasta abrirlo y guardarlo en ONLYOFFICE/Excel. Calcular los números aparte para la memoria.
  - Al guardar con openpyxl hay que conservar las imágenes pegadas en las hojas; comprobar que siguen ahí.
  - En el docx, editar a nivel de *runs*/párrafos sin romper estilos, campos SEQ de los pies ni imágenes.
- Estilo de la memoria: frases cortas, tono de estudiante de máster, valores de anteproyecto («≈»), coma decimal y punto de miles, citas como [n] a la bibliografía. Nada de párrafos inflados.
- Preferir el método del Tema 8 cuando haya varias opciones; normativa de apoyo: RD 646/2020, MITECO (recomendaciones vertederos V1.2), IHOBE (balances hídricos), 5.2-IC.
- Commits en español, mensaje corto con lista de lo cambiado por archivo/hoja/apartado (ver `git log`). Los binarios no tienen diff: describir los cambios en el mensaje.
- `.gitignore` excluye los ficheros de bloqueo de ONLYOFFICE/Word (`~$*`, `.~lock.*#`). Si existe uno, el archivo está abierto: avisar antes de sobrescribirlo.

## Pendientes conocidos

- `Resumen!B14` («Caudal de diseño por canal») = `'7_Canales'!#REF!` → debería apuntar al caudal por canal (Q total / 2; hoy `7_Canales` solo tiene el total en B9).
- Notas «para IA» dentro del Excel, a resolver y luego borrar:
  - `4_VidaUtil!D10`: la ecuación n = ln(1+g·C/R0)/ln(1+g) solo debe aparecer en el Word; quitarla del Excel.
  - `7_Canales!D19`: el n de Manning sale de la 5.2-IC (`5_2ic_fom_consolidada_norma.pdf`); citarla en la memoria (nueva referencia) y borrar la nota.
- Comentario obsoleto en `Gumbel!B1` («Serie ORIENTATIVA…»): la serie ya es real (AEMET + CERRA).
- Notas sueltas de trabajo en el Excel (`2_Geometria!K17:K20`, `3_Habitantes!H35`, `7_Canales!A31:A32`, `6_Lixiviados!A51:E63`) que ya están incorporadas a la memoria.
- La serie de Gumbel tiene 20 años y el MITECO recomienda ≥ 25 (ya se reconoce en la memoria).
