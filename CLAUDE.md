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
| [Vertedero_calculos.xlsx](Vertedero_calculos.xlsx) | Cálculos. Hojas `1_Ubicacion` … `7_Canales`, `Gumbel`, `Clima_AEMET`, `Resumen`. Ver «Formato del Excel». |
| [notas_para_memoria.md](notas_para_memoria.md) | Pendientes de la memoria y decisiones asumidas. Borrar cada punto cuando esté hecho. |
| [Vertedero_memoria.docx](Vertedero_memoria.docx) | Memoria entregable: apartados 1-7 + Bibliografía [1]-[14]. 5 figuras (visor, biogás, lixiviados, relieve, ortofoto) y 8 tablas. Tablas con columnas «Concepto / Valores (Unidades)», figuras y tablas con pie numerado automático («Figura .», «Tabla .» son campos SEQ, no texto roto). |
| [diagramas/](diagramas/) | `diagrama_biogas.png` (malla al tresbolillo, 171 chimeneas) y `diagrama_lixiviados.png` (espina de pez, DN 500 + 57 drenes DN 200). Van insertados en la memoria. |
| `Tema 8.pptx.pdf` | Apuntes del tema de vertederos (Gallardo y Colomer, UJI). **Es la referencia del método que espera el profesor** (Gumbel con tabla μn/σn, canales con C = 1, b = 2h, Manning). Ref. [12]. |
| `BOE-A-2020-7438-consolidado.pdf` | RD 646/2020 de vertederos. Ref. [11]. |
| `5_2ic_fom_consolidada_norma.pdf` | Norma 5.2-IC de drenaje superficial (Fomento). Tabla 3.1: n de Manning = 0,015 (hormigón in situ, 0,013-0,017). Ref. [13]. |
| [rescate_b8ba7bb/](rescate_b8ba7bb/) | Copia de la memoria del commit `b8ba7bb` («graficas cambiadas», de Gema) y sus imágenes extraídas, guardada como respaldo. No es la versión de trabajo. |

## Valores clave actuales (para comprobar coherencia Excel ↔ memoria)

- Superficie 236.425 m² (≈ 23,6 ha), perímetro ≈ 2.372 m, profundidad 35 m (casi dos curvas de 20 m del visor GVA), volumen ≈ 8,27 Mm³.
- Población A1 Marina Alta (padrón 2025, ARGOS) 198.258 hab; residuos 2025 98.969 t → 1,37 kg/hab·día; rechazo a vertedero 38,95 % → ≈ 38.550 t/año.
- Densidad 0,9 t/m³ → 7,45 Mt. Crecimiento g ≈ 2,1 % (CAGR 2023-2025). Vida útil ≈ 193 años sin crecimiento, ≈ 78 años con n = ln(1 + g·C/R0)/ln(1 + g).
- Biogás: R = 25 m, tresbolillo s = 2R·cos30º ≈ 43 m, 146 teóricas, **171 colocadas** (contadas en el diagrama).
- Lixiviados: balance P_EM = P_T − E_T ± E_C − Cc + H_i. P_T 746 mm, E_T Thornthwaite 1.086 mm → lluvia útil 263 mm (oct-mar), escorrentía 45 % (118 mm), infiltración 145 mm → 34.200 m³; retención (0,30 − 0,18) × 42.800 m³ = 5.100 m³ → ≈ 29.050 m³/año (≈ 80 m³/día). Punta con Pd de Gumbel en 24 h → 0,37 m³/s, v = 2 m/s → colector DN 500; drenes DN 200 cada 20 m (57 × 81 m + 730 m ≈ 5.350 m). Balsa = 2 × 32.300 ≈ 64.600 m³ (MITECO).
- Gumbel: 20 años (2006-2025; AEMET 8057C Pego desde 2010, 2006-2009 con CERRA/Open-Meteo), x̄ 101,2 mm, s 32,8 mm, μn 0,5236, σn 1,0628, F = 0,995 → T = 200 años, **Pd = 248 mm**.
- Canales (Excel): **un solo canal** perimetral. Pd en 1 h, C = 1, Q = I·A ≈ 16,3 m³/s, v = 3 m/s, b = 2h → h 1,65 m, b 3,30 m; Manning n = 0,015 → S ≈ 0,26 % < 0,5 %. Adoptado 3,3 × 1,7 m + 0,3 m = 2,0 m. Las figuras 4 y 5 (relieve y ortofoto) muestran el canal único alrededor de todo el contorno; se redibujaron con PIL sobre las imágenes originales, porque no hay MDT.

## Formato del Excel

Las hojas se limpiaron el 23/11/2026: sin textos explicativos, sin imágenes y sin notas sueltas. Las explicaciones van en la memoria.
- Columna A estrecha como margen. Título en B1 (negrita, azul `1F4E79`). Bloques con barra azul `1F4E79` y texto blanco que hace de cabecera: Concepto | Valor | Ud. **Sin columna de fuentes ni notas**: las fuentes van en la memoria (la lista antigua está en notas_para_memoria.md).
- Datos de entrada: texto azul sobre amarillo claro (`FFF2CC`). Resultados clave: negrita sobre azul claro (`DDEBF7`). El resto, fórmulas en negro. Separadores finos grises y sin líneas de cuadrícula.
- Formatos estándar (`#,##0`, `#,##0.0`, `0.00`, `0.0%`) y unidades con superíndice (m², m³).
- `Gumbel`: serie 2006-2025 (año, Pd, fecha) en B:D y el ajuste en H:J. `Clima_AEMET`: tabla mensual en B:T, con la P_T total en `I17`.
- No volver a meter en el Excel explicaciones, fuentes ni notas.
- Para recalcular y guardar los valores en caché: `soffice --headless --calc --convert-to xlsx` (LibreOffice está instalado). Para revisarlo a ojo, convertirlo a PDF.

## Forma de trabajar

- **Excel y memoria van siempre juntos**: si cambia un dato o un método en el Excel, actualizar el apartado, las tablas y las cifras del texto de la memoria (y el `Resumen`, y los diagramas si cambian longitudes o unidades). Comprobar que los números coinciden.
- Editar con Python (`openpyxl` para el xlsx, `python-docx` para el docx; ambos instalados). En Windows usar `python -X utf8` para que no falle la salida por consola.
  - openpyxl **no recalcula** fórmulas: tras modificar el Excel, los valores cacheados quedan vacíos hasta abrirlo y guardarlo en ONLYOFFICE/Excel. Calcular los números aparte para la memoria.
  - Al guardar con openpyxl hay que conservar las imágenes pegadas en las hojas; comprobar que siguen ahí.
  - En el docx, editar a nivel de *runs*/párrafos sin romper estilos, campos SEQ de los pies ni imágenes.
- Estilo de la memoria: un hilo argumentativo fácil de seguir y sin rodeos. Cada apartado sigue el orden objetivo → datos → cálculo → resultado, con las ecuaciones en línea aparte y centradas y una tabla resumen. Frases cortas, valores de anteproyecto («≈»), coma decimal y punto de miles, citas como [n]. Datos sacados de capturas → mejor en tabla que en imagen.
- Maquetación: cada apartado (2-7) y la Bibliografía empiezan en página nueva; pies de tabla encima y de figura debajo (campos SEQ); tablas con cabecera gris y filas que no se parten. Revisar la paginación convirtiendo a PDF con LibreOffice.
- Preferir el método del Tema 8 cuando haya varias opciones; normativa de apoyo: RD 646/2020, MITECO (recomendaciones vertederos V1.2), IHOBE (balances hídricos), 5.2-IC.
- Commits en español, mensaje corto con lista de lo cambiado por archivo/hoja/apartado (ver `git log`). Los binarios no tienen diff: describir los cambios en el mensaje.
- `.gitignore` excluye los ficheros de bloqueo de ONLYOFFICE/Word (`~$*`, `.~lock.*#`). Si existe uno, el archivo está abierto: avisar antes de sobrescribirlo.

## Pendientes conocidos

- Ver [notas_para_memoria.md](notas_para_memoria.md).
- Si alguien deja en un archivo una nota «para IA», hacer lo que pide y después borrarla.
- La serie de Gumbel tiene 20 años y el MITECO recomienda ≥ 25 (la memoria ya lo reconoce).
