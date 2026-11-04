# Datos complementarios del Módulo 5

Todos los archivos son datos oficiales y públicos, descargados el 02-11-2026. Los notebooks leen estos archivos desde disco; no se descarga nada durante la ejecución.

| Archivo | Fuente | Frecuencia y cobertura | Filas | Uso sugerido |
|---|---|---|---|---|
| `ipc_ecuador_nacional_1969_2026.csv` | INEC, IPC nacional general, serie empalmada (base jul 2025 – jun 2026 = 100) | Mensual, ene 1969 – ago 2026 | 692 | Serie conductora del módulo: inflación mensual |
| `ipc_ecuador_ccif_ciudades_2005_2026.csv` | INEC, IPC empalmado por división y grupo de consumo (CCIF), nacional, 2 regiones y 9 ciudades | Mensual, ene 2005 – jun 2026 (Sto. Domingo desde 2015) | 140 568 | Panel: 47 series por dominio × 12 dominios; Random Forest con muchas series |
| `macro_ecuador_mensual.csv` | Selección del BCE + IPC del INEC desde 1990 (la versión completa desde 1969 es `../series_economicas.csv`) | Mensual, 1990 – 2026 | 443 | Respaldo |
| `bce_iem_series.csv` | BCE, Información Estadística Mensual (BCEData), formato largo | Mensual, trimestral, anual y semanal | 530 590 | Catálogo completo para elegir otras series |
| `bce_iem_catalogo.csv` | Índice del archivo anterior: grupo, frecuencia, unidad, serie, número de observaciones | — | 3 637 series | Buscar una serie antes de cargarla |
| `petroleo_wti_brent_diario.csv` | EIA (EE. UU.), precios spot WTI y Brent, vía repositorio `datasets/oil-prices` | Diaria, 1986 – oct 2026 | 10 224 | Serie larga para Machine Learning y pronóstico diario |

## Columnas de `../series_economicas.csv` y `macro_ecuador_mensual.csv`

| Columna | Unidad | Desde | Obs. |
|---|---|---|---|
| `ipc_indice`, `ipc_var_mensual` | Índice / % | 1990 (en el archivo nacional, 1969) | 440 |
| `tasa_activa_ref_pct`, `tasa_pasiva_ref_pct` | % | ene 2015 | 143 |
| `liquidez_m2_musd` | Millones USD | ene 2000 | 320 |
| `reservas_internacionales_musd` | Millones USD | ene 2000 | 321 |
| `exportaciones_fob_musd`, `exportaciones_petroleras_musd`, `importaciones_fob_musd`, `balanza_comercial_musd` | Millones USD FOB | ene 1990 | 440 |
| `riesgo_pais_pb` | Puntos básicos (EMBI, promedio del mes) | ene 2000 | 321 |
| `precio_crudo_oriente_usd`, `precio_wti_usd` | USD por barril | ene 2000 | 320 |
| `salario_real_indice` | Índice | ene 2002 | 297 |

## Advertencias

- **IPC antes de 2000:** incluye la hiperinflación previa a la dolarización (variaciones mensuales de hasta 14 %). Para pronosticar la inflación actual conviene usar desde 2001 o 2005 y tratar 1999–2000 como cambio estructural.
- **Empalme del IPC:** desde julio 2026 el INEC usa una nueva base (jul 2025 – jun 2026 = 100); las series anteriores están empalmadas por el INEC.
- **Tasas de interés referenciales:** solo desde 2015 (143 observaciones); úsalas como variable de contexto, no como serie principal.
- **Balanza comercial:** cambia de signo y tiene saltos grandes; es más difícil de pronosticar que el IPC o las exportaciones.
- **WTI:** el promedio mensual de la EIA y el del BCE difieren en pocos dólares en algunos meses por la fuente y el método de promedio.
- **Tamaño:** `bce_iem_series.csv` pesa unos 61 MB; si se sube a GitHub, comprimirlo o usar solo `macro_ecuador_mensual.csv`.

## Fuentes

- INEC, Índice de Precios al Consumidor 2026 (tabulados y series empalmadas): https://www.ecuadorencifras.gob.ec/indice-de-precios-al-consumidor-2026/
- BCE, BCEData – Información Estadística Mensual: https://contenido.bce.fin.ec/bcedata/
- EIA vía https://github.com/datasets/oil-prices
