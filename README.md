# Módulo 5 — Econometría y Forecasting con IA

Material de clase del **Diplomado en Big Data e Inteligencia Artificial** (CEC EPN).

Siete jornadas para aprender a **pronosticar series económicas del Ecuador con datos oficiales**: componentes de una serie, validación cronológica, ARIMA y SARIMA, Machine Learning para series de tiempo, modelos híbridos, escenarios e interpretación económica. Como en el Módulo 3, cada tema se explica primero **a mano, con números pequeños**, y después en Python, paso a paso y con el código comentado.

## Contenido

```
modulo5_econometria_forecasting_ia/
├── README.md
├── presentaciones/      diapositivas de los días 1 a 7 en PDF (sin código)
├── notebooks/           un notebook por jornada y el proyecto final
└── datos/
    ├── series_economicas.csv     tabla mensual principal (1969 – 2026)
    └── complementarios/          series completas del INEC, BCE y EIA
```

## Ruta por jornada

| Día | Presentación | Notebook | Contenidos | Evaluación | Estado |
|---|---|---|---|---|---|
| 0 (asinc.) | — | `00_Dia0_Fechas_y_Series_en_Pandas` | Fechas, índice temporal, `shift`, `diff`, `pct_change`, `rolling`, `resample` | Diagnóstica al inicio del Día 1 | listo |
| 1 | `Dia_01_Series_Tiempo` | `01_Dia1_Componentes_y_Pronosticos_Simples` | 1.1–1.4 Frecuencia, tendencia, estacionalidad, descomposición, atípicos, ACF a mano, ingenuo y promedio móvil | — | listo |
| 2 | `Dia_02_Validacion_Temporal` | `02_Dia2_Validacion_y_Estacionariedad` | 1.5, 2.1–2.3 Corte cronológico, horizontes, AR y MA, diferenciación, ADF | Actividad 1 (20 pts) | listo |
| 3 | `Dia_03_ARIMA` | `03_Dia3_ARIMA_SARIMA` | 2.4–2.5, 3.1 Ajuste, residuos, intervalos; VAR solo conceptual | Actividad 2 (20 pts, `Actividad2_ARIMA`) | listo |
| 4 | `Dia_04_Forecasting_ML` | `04_Dia4_Random_Forest_para_Series` | 3.2–3.4 Tabla de rezagos, TimeSeriesSplit, pronóstico recursivo y directo | — | listo |
| 5 | `Dia_05_Pronostico_Macroeconomico` | `05_Dia5_Hibridos_y_Contexto_Macro` | 3.5, 4.1–4.3 Híbrido ARIMA + RF, indicadores macro, cambios estructurales | Actividad 3 (20 pts) | listo |
| 6 | `Dia_06_Escenarios` | `06_Dia6_Backtesting_y_Escenarios` | 4.4–5.2 Origen móvil, escenarios, script de actualización (Módulo 4) | Inicio del proyecto | listo |
| 7 | `Dia_07_Taller_Final` | `07_Dia7_Taller_Proyecto` | 5.3–5.5 Notebook base del proyecto | Proyecto final (40 pts) | listo |

### Cómo está organizado cada notebook

Los mismos pasos del Módulo 3, adaptados a series de tiempo:

1. **Mirar la serie**: fechas, frecuencia, faltantes y gráfica.
2. **Preparar paso a paso**: índice de fechas, variaciones, diferencias.
3. **Línea base**: último valor e ingenuo estacional.
4. **El método a mano**, con 12 meses.
5. **Modelo simple** con statsmodels o scikit-learn.
6. **Métricas a mano y con la librería**, Train frente a Validation **en orden cronológico**.
7. **Hiperparámetros uno por uno** y combinaciones con `for`.
8. **Resultado final**: Test una sola vez y pronóstico con intervalo.
9. **Comparación final** de todos los métodos.

Nunca se usa una partición aleatoria: los últimos meses siempre quedan para evaluar.

## Preparación y ejecución

1. Instala **Python 3.10 o posterior** con Jupyter (por ejemplo, con Anaconda).
2. Instala las librerías: `numpy`, `pandas`, `matplotlib`, `scikit-learn`, `statsmodels`, `sktime` y `joblib`.
3. Abre la carpeta en Jupyter y ejecuta cada notebook **en orden, de arriba hacia abajo**. Las rutas encuentran `datos/` tanto desde la raíz como desde `notebooks/`.

Los notebooks no descargan nada: todos los datos están en `datos/`.

## Datos

`datos/series_economicas.csv` tiene una fila por mes (enero 1969 – noviembre 2026) y una columna por indicador; cada columna empieza cuando la fuente empieza a publicarla.

| Columna | Fuente | Unidad | Desde | Obs. |
|---|---|---|---|---|
| `ipc_indice`, `ipc_var_mensual` | INEC, IPC nacional empalmado | Índice / % | 1969 | 692 |
| `exportaciones_fob_musd`, `exportaciones_petroleras_musd`, `importaciones_fob_musd`, `balanza_comercial_musd` | BCE | Millones USD FOB | 1990 | 440 |
| `riesgo_pais_pb` | BCE (EMBI, promedio del mes) | Puntos básicos | 2000 | 321 |
| `reservas_internacionales_musd`, `liquidez_m2_musd` | BCE | Millones USD | 2000 | 320–321 |
| `precio_crudo_oriente_usd`, `precio_wti_usd` | BCE | USD por barril | 2000 | 320 |
| `salario_real_indice` | BCE | Índice | 2002 | 297 |
| `tasa_activa_ref_pct`, `tasa_pasiva_ref_pct` | BCE | % | 2015 | 143 |

En `datos/complementarios/` están las fuentes completas: el IPC por división y ciudad (140 568 filas), las 3 637 series de la Información Estadística Mensual del BCE y los precios diarios del petróleo WTI y Brent desde 1986. Procedencia y advertencias en [`datos/complementarios/README.md`](datos/complementarios/README.md).

**Advertencia principal:** el IPC antes de 2001 incluye la hiperinflación previa a la dolarización (hasta 14 % mensual). Para pronosticar la inflación actual conviene usar la serie desde 2005 y estudiar 1999–2000 como cambio estructural.

## Bibliografía

- Hyndman, R. y Athanasopoulos, G. (2021). *Forecasting: Principles and Practice* (3.ª ed.). <https://otexts.com/fpp3/>
- Wooldridge, J. (2021). *Introductory Econometrics: A Modern Approach*. Cengage Learning.
- Hamilton, J. (2020). *Time Series Analysis*. Princeton University Press.

## Uso responsable

Los datos son públicos (INEC, BCE y EIA). Un pronóstico no es una predicción segura: siempre se presenta con su error, su intervalo y sus límites. Una correlación entre indicadores no prueba causalidad.

---
Docente: Jonathan Rosero Soto
