# Notas para la memoria

Cosas que hay que pasar a [Vertedero_memoria.docx](Vertedero_memoria.docx) o revisar en ella. Salen de la limpieza del Excel del 23/11/2026: lo que se quitó de las hojas y los cambios de método que todavía no están en la memoria. Cuando algo ya esté en la memoria, se borra de aquí.

## 1. Cambios de método que la memoria aún no recoge

Vienen del commit `81f4959` («canales y lixiviados nuevos»). Se decidió mantenerlos en el Excel.

### Apartado 6: lixiviados (Tabla 3 y texto)

Ahora el balance no resta la evapotranspiración: se infiltra el 55 % de **toda** la lluvia anual, no de la lluvia útil.

| Concepto | Memoria actual | Excel ahora |
|---|---|---|
| Lluvia que se reparte | Lluvia útil 263 mm (P − ETP, oct-mar) | P_T = 745,8 mm |
| Infiltración P_T·(1 − E_C) | 145 mm → 34.200 m³/año | 410,2 mm → 96.979 m³/año |
| Agua retenida (Cc − H_i) | 5.100 m³/año | 5.140 m³/año (igual) |
| **Lixiviado anual P_EM** | ≈ 29.000 m³/año (≈ 80 m³/día) | **≈ 91.840 m³/año (≈ 252 m³/día, 388 mm)** |

- El colector DN 500, los drenes DN 200 y la balsa (≈ 64.570 m³) **no cambian**, porque se dimensionan con el día de lluvia máxima de Gumbel.
- Hay que quitar de la memoria la ETP de Thornthwaite (≈ 1.086 mm) y la frase «solo sobra agua de octubre a marzo», o explicar por qué no se resta E_T. La fórmula P_EM = P_T − E_T ± E_C − Cc + H_i sigue citada.
- La hoja `Clima_AEMET` mantiene el cálculo de Thornthwaite, pero ya no la usa ninguna otra hoja (solo se toma de ella P_T). Si la memoria deja de usar la ETP, se pueden borrar esas columnas.

### Apartado 7: canales (Tabla 5, texto y figuras)

Ahora hay **un solo canal** perimetral que lleva todo el caudal.

| Concepto | Memoria actual | Excel ahora |
|---|---|---|
| Nº de canales | 2 (norte y sur) | **1** |
| Caudal de diseño | 8,15 m³/s por canal | 16,3 m³/s |
| Longitud | ≈ 1.186 m cada uno | ≈ 2.372 m (todo el perímetro) |
| A = Q/v (v = 3 m/s) | 2,72 m² | 5,44 m² |
| h / b calculados | 1,17 / 2,33 m | 1,65 / 3,30 m |
| R = h/2 | 0,58 m | 0,82 m |
| Pendiente necesaria S | 0,42 % | 0,26 % (< 0,5 %, OK) |
| Sección adoptada | 2,4 × 1,2 m + 0,3 m = 1,5 m | **3,3 × 1,7 m + 0,3 m = 2,0 m** |

- Las figuras 8 y 9 («canal norte (amarillo) y canal sur (naranja)») y su pie hablan de dos canales.

## 2. Información que se quitó del Excel y no está en la memoria

Ninguna es imprescindible. Se guarda por si se quiere usar.

- **Ubicación (antigua hoja 1, «Justificación» y «Puntos débiles»).** Lo demás ya está en el apartado 1.
  - La cantera está al pie de la sierra, en la vaguada que baja del oeste.
  - La caliza obliga a impermeabilizar igual (la memoria ya habla de la impermeabilización, pero no relaciona las dos cosas).
  - Comprobar los pozos cercanos, el planeamiento y el plan de restauración vigente de la cantera.
- **Población estacional (antigua hoja 3).** La Marina Alta tiene ≈ 136.860 plazas turísticas: https://lamarina.eldiario.es/2023/09/27/el-potencial-turistico-de-la-marina-alta-en-cifras-136-860-plazas-de-alojamiento/. Podría citarse como limitación de usar solo el padrón.
- **Crecimiento de residuos (antigua hoja 3).** Había una nota: «se podría hacer una regresión lineal para predecir los residuos». Se usó la CAGR.
- **Gumbel.** La tabla de origen incluía también 2005 (38 mm, CERRA), que no entra en la serie 2006-2025. La tabla tenía los años desplazados una fila; ya está corregido y las fechas llevan su año real.
- **Lluvia anual AEMET (antigua hoja 6).** A 2021 le falta junio y a 2022 le falta abril, así que AEMET no da el total anual de esos años. La P_T se calcula con las medias mensuales, como ya dice la memoria.
- **Thornthwaite (pie de la hoja Clima_AEMET).** ETP = 16·L·(10·T/I)^a, con I = Σ(T/5)^1,514 y L el factor de horas de luz (tabla de 40º N; Pego está a 38,9º N). Lluvia útil = agua que sobra en los meses en que llueve más de lo que se evapora. Solo sirve si se mantiene la ETP en el apartado 6.

## 3. Fuentes y notas que había junto a cada valor del Excel

Se quitó la columna «Fuente / nota» de todas las hojas. Casi todo ya está en la memoria con su referencia [n]. Sirve para comprobar que cada dato tiene su fuente citada.

| Hoja | Dato | Fuente / nota |
|---|---|---|
| 1_Ubicacion | Longitud −0,1065º | Negativo = oeste |
| 2_Geometria | Superficie y perímetro | Medidos en el visor GVA [1] |
| 2_Geometria | Profundidad 35 m | Curvas de nivel de 20 m, borde más bajo |
| 3_Habitantes | Residuos 2023, 2024 y 2025 | Consorci Mare [3] |
| 3_Habitantes | Población (padrón 2025) | ARGOS (GVA) [2] |
| 3_Habitantes | Rechazo a vertedero 38,95 % | Consorci Mare, 2024 [4] |
| 4_VidaUtil | Densidad 0,9 t/m³ | Habitual entre 0,75 y 1 (**sin fuente citada en la memoria**) |
| 5_Biogas | Radio de influencia R = 25 m | «Según normativa» (**la memoria no dice qué norma**) |
| 5_Biogas | Distancia entre filas | Filas desplazadas s/2 |
| 5_Biogas | 171 chimeneas | Contadas en el diagrama |
| 6_Lixiviados | P_T | AEMET 8057C Pego, 2020-2025 [5] |
| 6_Lixiviados | Escorrentía 45 % | IHOBE (2015), tabla 5 [7] |
| 6_Lixiviados | Humedad H_i 20 % | IHOBE (2015), tabla 6 (Tchobanoglous) [7, 10] |
| 6_Lixiviados | Capacidad de campo 0,30 | Modelo HELP (Schroeder et al., 1994) [9] |
| 6_Lixiviados | Separación de drenes 20 m | Típico 20-30 m |
| 6_Lixiviados | Colector 730 m, 57 drenes de 81 m | Medidos y contados en el diagrama (4.626 m / 57 drenes) |
| 6_Lixiviados | Pendiente 2 % | MITECO: mínimo 2 % [8] |
| 6_Lixiviados | Capa drenante de grava 20-40 mm, 50 cm | MITECO [8]; RD 646/2020 [11] |
| 6_Lixiviados | Colector DN 500 | DN comercial inmediatamente superior |
| 6_Lixiviados | Dren DN 200 | Diámetro práctico para limpieza |
| 6_Lixiviados | Balsa | MITECO: capacidad mínima = día de lluvia máxima; se construye el doble [8] |
| 7_Canales | C = 1 | Toda la lluvia escurre |
| 7_Canales | n de Manning 0,015 | Norma 5.2-IC, tabla 3.1 [13] |
| Gumbel | μn = 0,5236, σn = 1,0628 | Tabla del Tema 8 para n = 20 [12] |
| Gumbel | Pd de 2006-2009 | CERRA (Open-Meteo) [6] |
| Gumbel | Pd de 2010 | AEMET 8057C, año incompleto [5] |
| Gumbel | Pd de 2011-2025 | AEMET 8057C [5] |
| Clima_AEMET | Toda la tabla | AEMET OpenData, estación 8057C (Pego). Celdas vacías = mes sin dato [5] |

- La memoria no dice que **2010 es un año incompleto** en AEMET. Se podría añadir en el apartado 7.
