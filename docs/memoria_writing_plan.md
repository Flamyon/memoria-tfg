# Plan operativo de escritura de la memoria del TFG

**Título actualizado:** Explorando la complejidad y el caos en series temporales económicas  
**Enfoque:** desarrollo de una metodología/herramienta de análisis, validada con mapa logístico y aplicada después a volatilidad intradía de Bitcoin (`log_rv_past_12`, velas de 5 minutos)  
**Referencia metodológica:** Olmedo Fernández (2001)  
**Repositorios del proyecto:**

| Repositorio | Rol |
|-------------|-----|
| `btc-volatility` | Estudio técnico de validación (fases 0–14) |
| `mvp-web` | MVP web Streamlit autónomo (predicción operativa) |
| `tfg-memoria` | Memoria LaTeX (`Capitulos/*.tex`, `proyect.tex`) |

---

## 0. Estado de la documentación auxiliar en `tfg-memoria/docs`

La documentación auxiliar ya debe tratar el proyecto como compuesto por tres piezas: estudio técnico (`btc-volatility`), implementación (`mvp-web`) y memoria (`tfg-memoria`). Estado actual de los documentos de apoyo:

| Documento | Estado |
|-----------|---------|
| `Fases_segun_tesis.md` | Actualizado con Fase 14, bloque MVP y mapa 0–14 ↔ Olmedo |
| `Resumen_tesis_por_capitulos.md` | Actualizado para incluir HAR-logRV, MVP y diferencias frente a la tesis |
| Este plan | Guía operativa para pasar de documentación auxiliar a capítulos LaTeX |

**Acción pendiente ya dentro de la memoria:** redactar los capítulos manteniendo la jerarquía correcta: primero herramienta/metodología, después comprobación sintética con mapa logístico, después aplicación empírica a Bitcoin, cierre HAR y MVP.

---

## 1. Estado actual del TFG

### 1.1. Bloques de trabajo

| Bloque | Estado | Evidencia principal |
|--------|--------|---------------------|
| Formación teórica (Olmedo + dinámica no lineal) | Documentada en docs de mapeo; **no integrada** en capítulos LaTeX | `docs/Fases_segun_tesis.md`, `docs/Resumen_tesis_por_capitulos.md` |
| Comprobación sintética | **Completada** con mapa logístico limpio y con ruido | `phase13_logistic_map_validation_report.md` |
| Validación experimental | **Completada (14 fases)** | `btc-volatility/reports/FASES.md`, `phase0`–`phase14_*_report.md` |
| MVP web | **Implementado y funcional** | `mvp-web/` (Streamlit, tests, artefactos exportados) |
| Escritura memoria | Estructura LaTeX definida; **contenido pendiente** | Capítulos con `% TODO`; solo `resumen.tex` con borrador |

### 1.2. Arquitectura del proyecto (tres piezas)

```text
btc-volatility (investigación)
  fases 0–14 → informes, figuras, tablas, artefactos JSON/CSV/NPZ
       │
       │  scripts/export_model_artifacts.py  (desde btc-volatility o copia en mvp-web)
       ▼
mvp-web (aplicación)
  data/model_artifacts/  →  app Streamlit (runtime autónomo, sin importar btc-volatility)
       │
       ▼
tfg-memoria (documentación académica)
  metodología + comprobación sintética + aplicación BTC + MVP + conclusiones
```

### 1.3. Índice actual de la memoria (`proyect.tex`)

1. Resumen, agradecimientos, índices  
2. Introducción  
3. Definición de objetivos  
4. Antecedentes y marco teórico  
5. Planificación (`analtemporal.tex`)  
6. Requisitos  
7. Diseño  
8. Implementación del procedimiento de análisis  
9. Resultados y discusión  
10. Implementación del MVP web  
11. Pruebas y verificación  
12. Manual de usuario  
13. Conclusiones  
14. Anexos  
15. Bibliografía  

**Enfoque del índice:** no presentar Bitcoin como objetivo único. El índice debe separar: conceptos, procedimiento, comprobación sintética, aplicación empírica a BTC, cierre predictivo HAR y MVP.

### 1.4. Serie principal, modelos y roles narrativos

| Elemento | Valor / rol | Fuente |
|----------|-------------|--------|
| Dato validado | `btc_5m_clean.csv`, 245 088 obs., 2024-01-01 – 2026-04-30 | Fase 0 |
| Features | `btc_5m_features.csv`, 244 752 obs. | Fase 1 |
| Serie principal \(v_t\) | `log_rv_past_12` | Fases 2–3 |
| Target predictivo | `log_rv_future_12` (horizonte 12 velas = 1 h) | Fases 11, 14 |
| Embedding no lineal | \(\tau=137\), \(m=5\) | Fase 8 |
| AR(49) | Benchmark lineal fuerte (filtro fase 6 + predicción) | Fases 6, 11 |
| kNN local | Predictor no lineal experimental; \(k=50\) (fase 11), \(k=200\) (fase 12, MVP) | Fases 11–12, MVP |
| **HAR-logRV compacto** | **Cierre predictivo operativo**; memoria 1 h / 4 h / 24 h | **Fase 14**, MVP |
| Mapa logístico | Comprobación sintética de la metodología | Fase 13 |

**Modelos finales del estudio** (texto de `FASES.md`): AR(49), Embedding(\(\tau=137, m=5\)), kNN (\(k=50\)–\(200\)), **HAR-logRV compacto exportable al MVP**.

### 1.5. Mensaje empírico defendible (actualizado)

No afirmar caos determinista en BTC. Distinción obligatoria:

| Tipo | Qué decir | Evidencia |
|------|-----------|-----------|
| **(a) Dependencia temporal** | Persistencia fuerte de volatilidad | ACF `log_rv_past_12` lag 1 ≈ 0,98 (Fase 4) |
| **(b) No linealidad / heterocedasticidad** | Dependencia en varianza, BDS, ARCH | Fases 2, 7 |
| **(c) Compatible con dinámica compleja** | AMI, PE, Lyapunov vs barajado; surrogados mixtos | Fases 8–10 |
| **(d) Caos determinista** | **No en BTC**; en logístico se comprueba que el procedimiento responde ante una dinámica conocida | Fase 13 |

**Predicción out-of-sample (muestra comparable, 5000 puntos, Fase 14):**

| Modelo | RMSE test | MAE | R² OOS | Rol |
|--------|-----------|-----|--------|-----|
| Persistencia | 0,9775 | 0,7629 | 0,403 | Baseline |
| kNN \(\tau137\_m5\_k200\) | 0,8765 | 0,6811 | 0,520 | No lineal experimental |
| AR(49) h=12 | 0,8641 | 0,6710 | 0,534 | Benchmark lineal fuerte |
| **HAR-logRV** | **0,8608** | **0,6691** | **0,537** | **Modelo práctico recomendado** |

Mejora HAR vs AR(49): ΔRMSE ≈ 0,0033 (~0,4 %). **No exagerar:** la diferencia es pequeña; HAR gana por simplicidad, interpretabilidad y exportabilidad al MVP.

**Matiz Fase 10 (surrogados):** vs barajado hay separación fuerte en PE y Lyapunov; vs phase-randomized/AAFT, Lyapunov y D2 no separan claramente → parte de la señal puede explicarse por estructura lineal/espectral.

**Matiz Fase 13 vs BTC:** en mapa logístico limpio, kNN (RMSE ≈ 0,098) supera AR(0)/media (≈ 0,357), aparece estructura geométrica más nítida y Rosenstein detecta divergencia positiva aunque no estime exactamente \(ln(2)\). En BTC, AR(49) y HAR capturan mejor la persistencia multiescala financiera que el kNN local.

### 1.6. MVP web (`mvp-web`)

| Aspecto | Detalle |
|---------|---------|
| Stack | Python, Streamlit, pandas, numpy, plotly, requests |
| Entrada | `streamlit run app.py` |
| Páginas | Inicio; Predicción; Diagnóstico; Comparación de modelos; Ayuda |
| Fuentes de datos | Binance API (1000 velas), CSV usuario (≤2000 filas), dataset ejemplo |
| Modelos en runtime | Persistencia, kNN (\(k=200\)), AR(49), HAR global, Mini-HAR local (experimental) |
| Artefactos | `data/model_artifacts/*.json/csv/npz` (exportados desde estudio) |
| Tests | 75 funciones `test_*` en 10 módulos (`tests/`) |
| Autonomía | No importa `btc-volatility` en ejecución |

**Recomendación del MVP:** `har_logrv_global` (`historical_metrics.json`, Fase 14).

**Limitaciones explícitas del MVP** (del README): no predice dirección, no es asesoramiento, no intervalos de confianza, no demuestra caos, walk-forward local ≠ validación histórica formal.

---

## 2. Lógica narrativa adaptada de Olmedo

Recorrido de la tesis: marco → herramientas → reconstrucción → estacionariedad/no linealidad → cuantificación → predicción → aplicación empírica.

**Adaptación al TFG (directa, sin tono filosófico largo):**

```text
Objetivo metodológico: desarrollar herramientas de análisis de series
→ Marco teórico autocontenido (sin dar conceptos por sabidos)
→ Comprobación sintética con mapa logístico (fase 13)
→ Aplicación empírica a BTC: datos y variable (fases 0–1)
→ Caracterización lineal y no lineal de BTC (fases 2–10)
→ Predicción local y robustez (fases 11–12)
→ Cierre predictivo HAR + MVP (fase 14 + mvp-web)
→ Conclusiones separando metodología, logístico, BTC, HAR y MVP
```

**Aportación respecto a Olmedo:** formulación como herramienta reproducible; comprobación sintética separada; aplicación a alta frecuencia BTC; anti-leakage; **Fase 14 HAR**; **MVP Streamlit**; interpretación más prudente sobre caos.

---

## 3. Inventario de resultados por fase

Referencia maestra: `btc-volatility/reports/FASES.md`. Detalle: `reports/phaseN_*_report.md`.

| Fase | Resultados citables | Figuras clave | Tablas / artefactos |
|------|---------------------|---------------|---------------------|
| 0 | 245 088 obs., sin gaps/nulos | — | `phase0_*_summary.csv` |
| 1 | 244 752 filas, sin leakage | — | `phase1_shape_summary.csv` |
| 2 | Curtosis \(r\) 53,6; episodio 2025-10-10 | `phase2_05_log_rv_past_12.svg` | `phase2_descriptive_statistics.csv` |
| 3 | `log_rv_past_12` elegida; estacionariedad imperfecta | rolling `log_rv` | `phase3_adf_results.csv`, `kpss_results.csv` |
| 4 | ACF vol. lag1 ≈ 0,98; \(r\) ≈ ruido blanco | ACF/PACF/periodograma vol. | `phase4_correlogram_summary.csv` |
| 5 | RP volatilidad con diagonales | `phase5_*_log_rv_past_12_rp.png` | `phase5_selected_windows.csv` |
| 6 | AR(49); residuos casi blancos en media | residuos ACF | `phase6_ar_order_selection.csv` |
| 7 | LB², ARCH-LM, BDS 36/36 | `phase7_bds_pvalues.svg` | `phase7_bds_results.csv` |
| 8 | \(\tau=137\), \(m=5\); Cao→14 descartado | AMI, embedding 2D | `phase8_selected_embedding_params.json` |
| 9 | D2≈3,83 vs 4,02 barajada; Lyap≈0,0212; PE≈0,895 | comparación original/barajada | `phase9_quantification_summary.json` |
| 10 | vs barajado: PE, Lyapunov extremos; vs phase-rand: Lyap similar | boxplots surrogados | `phase10_surrogate_summary.csv` |
| 11 | kNN \(k=50\) RMSE 0,894; AR 0,864 | métricas test | `phase11_test_metrics.csv` |
| 12 | \(m=14\) peor; \(k=200\) estable | RMSE por config | `phase12_config_comparison.csv` |
| 13 | kNN >> AR(0) en logístico; mapa transición; Lyap cualitativo | embedding, BIC AR, transición | `phase13_prediction_metrics.csv`, `phase13_ar_order_selection.csv` |
| **14** | **HAR RMSE 0,8608 < AR 0,8641 < kNN 0,8765** | `phase14_ar_knn_har_metrics.svg` | `phase14_har_coefficients.csv`, `har_logrv_model.json` |

---

## 4. Guía por capítulo

### 4.1. Resumen (`resumen.tex`)

| Campo | Contenido |
|-------|-----------|
| Objetivo | 1 página: metodología, comprobación logística, aplicación BTC, HAR y MVP |
| Actualizar | Mantener BTC como aplicación empírica, no como objetivo único; no exagerar HAR ni caos |
| Archivos | Sección 1.5; `phase14_har_logrv_mvp_report.md`; `mvp-web/README.md` |

---

### 4.2. Introducción (`introduccion.tex`)

| Campo | Contenido |
|-------|-----------|
| Objetivo | Presentar el TFG como desarrollo de herramienta/metodología y aplicación real |
| Secciones | Contexto; Planteamiento; Naturaleza del trabajo (teoría + logístico + BTC + MVP); Estructura |
| Teoría | Breve: complejidad ≠ caos; volatilidad realizada; por qué en economía solo hay indicios |
| Figuras | Opcional: diagrama tres repositorios |
| Advertencias | No prometer señales de trading ni caos en BTC |

---

### 4.3. Objetivos (`defobjetivos.tex`)

**Objetivo general sugerido:** desarrollar y validar una metodología computacional para analizar series temporales con herramientas de dinámica no lineal; comprobarla con mapa logístico; aplicarla a volatilidad intradía de BTC; cerrar con modelo HAR exportable y MVP demostrativo.

**Objetivos específicos (alineados con fases):**

1. Explicar los conceptos sin asumir tribunal especialista.  
2. Validar la metodología con mapa logístico (13).  
3. Validar y construir series de volatilidad realizada para BTC (0–1).  
4. Caracterizar dependencia lineal y estacionariedad (2–4).  
5. Contrastar no linealidad y reconstruir espacio de estados (5–8).  
6. Cuantificar indicadores con controles surrogados (9–10).  
7. Evaluar predicción local kNN vs benchmarks (11–12).  
8. **Implementar HAR-logRV y exportarlo al MVP (14).**  
9. **Desarrollar MVP web autónomo para predicción operativa (`mvp-web`).**

**Aportación principal:** herramienta metodológica reproducible inspirada en Olmedo → control sintético + BTC alta frecuencia + **separación análisis dinámico / cierre HAR / MVP**.

---

### 4.4. Antecedentes (`analanteced.tex`)

| Sección `.tex` | Teoría | Fases | Olmedo |
|----------------|--------|-------|--------|
| Complejidad, caos | Definiciones; no linealidad necesaria no suficiente | — | Cap. 1 (resumido) |
| Sistemas dinámicos | Mapa logístico, sensibilidad | 13 | Cap. 2 |
| Series financieras | Vol. realizada, clustering, HAR (Corsi) | 1–2, **14** | Cap. 9 (sustituido) |
| Caracterización | ACF, PACF, periodograma, RP | 2, 4, 5 | Cap. 4 |
| Estacionariedad / no lin. | ADF/KPSS, BDS, ARCH | 3, 6, 7 | Cap. 6 |
| Reconstrucción | Takens, AMI, FNN, Cao | 8 | Cap. 5 |
| Cuantificación | D2, Rosenstein, PE, surrogados | 9, 10 | Caps. 3, 7 |
| Predicción | kNN local, sesgo-varianza; **HAR multiescala** | 11–12, **14** | Cap. 8 + literatura HAR |
| Relación Olmedo / aportación | Tabla comparativa | 0–14 | — |

**Nuevo bloque teórico obligatorio:** modelo HAR-logRV (ecuación Fase 14); **no** confundir con demostración de caos.

---

### 4.5. Planificación (`analtemporal.tex`)

| Campo | Contenido |
|-------|-----------|
| Fases | 0–14 + formación + memoria + MVP |
| Herramientas | Python (`btc-volatility`), Streamlit (`mvp-web`), LaTeX |
| TODO | Fechas y horas reales si no están documentadas |

---

### 4.6. Requisitos (`requisitos.tex`)

| Bloque | Requisitos verificables |
|--------|-------------------------|
| Datos | Columnas, frecuencia 5m, UTC, precios > 0 (fase 0; `mvp-web` validación) |
| Pipeline | No leakage; splits temporales; Theiler (fases 11–12) |
| Fase 14 | HAR ajustado solo en train; test comparable 5000 pts |
| MVP | Artefactos obligatorios (`config.py`); 5 modelos; disclaimer; no reentrenar AR/kNN desde web salvo Mini-HAR |

---

### 4.7. Diseño (`diseno.tex`)

| Campo | Contenido |
|-------|-----------|
| Pipeline | Módulos `src/` por dominio: `volatility.py`, `state_space.py`, `local_prediction.py`, `phase14_har_logrv_mvp.py` |
| MVP | Capas: carga → features → `ModelRegistry` → UI; exportación artefactos |
| Figuras | Diagrama flujo datos; diagrama desacoplado btc-volatility ↔ mvp-web |

---

### 4.8. Implementación del procedimiento (`implementacion.tex`)

**Añadir secciones LaTeX pendientes:**

- `\section{Validación metodológica con mapa logístico}` → Fase 13  
- `\section{Modelo HAR-logRV y exportación al MVP}` → Fase 14  
- Reescribir `\section{Resultado final...}` → síntesis 11–14 + rol de cada modelo  

| Sección | Fase | Script | Informe |
|---------|------|--------|---------|
| Validación datos | 0 | `build_btc_5m_clean.py` | `phase0_validation_report.md` |
| Variables | 1 | `build_phase1_features.py` | `phase1_feature_engineering_report.md` |
| Descriptivos | 2 | `phase2_general_tools.py` | `phase2_general_tools_report.md` |
| Estacionariedad | 3 | `phase3_stationarity.py` | `phase3_stationarity_report.md` |
| ACF/espectro | 4 | `phase4_correlogram_spectrum.py` | `phase4_correlogram_spectrum_report.md` |
| Recurrencia | 5 | `phase5_initial_recurrence.py` | `phase5_initial_recurrence_report.md` |
| AR | 6 | `phase6_linear_filtering.py` | `phase6_linear_filtering_report.md` |
| No linealidad | 7 | `phase7_nonlinearity_tests.py` | `phase7_nonlinearity_report.md` |
| Reconstrucción | 8 | `phase8_state_space_reconstruction.py` | `phase8_state_space_reconstruction_report.md` |
| Cuantificación | 9 | `phase9_dynamics_quantification.py` | `phase9_dynamics_quantification_report.md` |
| Surrogados | 10 | `phase10_surrogate_tests.py` | `phase10_surrogate_tests_report.md` |
| Predicción kNN | 11 | `phase11_local_state_space_prediction.py` | `phase11_local_state_space_prediction_report.md` |
| Robustez | 12 | `phase12_prediction_sensitivity.py` | `phase12_prediction_sensitivity_report.md` |
| Mapa logístico | 13 | `phase13_logistic_map_validation.py` | `phase13_logistic_map_validation_report.md` |
| **HAR + MVP export** | **14** | **`phase14_har_logrv_mvp.py`** | **`phase14_har_logrv_mvp_report.md`** |

---

### 4.9. Resultados y discusión (`resultados.tex`)

| Sección `.tex` | Fases | Figuras recomendadas (cuerpo) |
|----------------|-------|-------------------------------|
| Caracterización inicial | 0–5 | `phase2_05`, `phase4_log_rv_acf`, `phase5_quiet_log_rv_rp` |
| Filtrado lineal | 6 | `phase6_residuals_acf` |
| Evidencia no lineal | 7 | `phase7_bds_pvalues` |
| Reconstrucción | 8 | `phase8_ami_original_vs_shuffled`, `phase8_embedding_2d` |
| Cuantificación | 9–10 | `phase9_original_vs_shuffled`, `phase10_surrogate_boxplots_entropy` |
| Predicción local | 11–12 | `phase11_test_metrics_comparison`, `phase12_test_rmse_by_config` |
| **Comparación final de modelos** | **14** | **`phase14_ar_knn_har_metrics.svg`**, coeficientes HAR |
| Validación sintética | 13 | `phase13_transition_map_clean`, `phase13_embedding_2d_clean` vs `phase8_embedding_2d` |
| Discusión caos | 9–10, 13 | Texto; no figura única |
| Interpretación global | 0–14 | Tabla resumen modelos (sección 1.5) |

**Conclusiones permitidas en Resultados:**

- HAR mejora ligeramente a AR(49) y claramente a kNN en muestra comparable.  
- kNN confirma predictibilidad local pero no domina en BTC.  
- Reconstrucción + cuantificación: evidencia (c), no (d).  
- Logístico: el procedimiento detecta estructura cuando la dinámica es conocida.

**Advertencias:** no presentar HAR como prueba de caos; no ocultar mejora marginal HAR vs AR; mencionar solapamiento `rv_past`/`rv_future`.

---

### 4.10. MVP web (`mvpweb.tex`)

| Campo | Contenido |
|-------|-----------|
| Objetivo | Prototipo operativo que materializa Fase 14 y expone modelos del estudio |
| Secciones | Objetivo; Funcionalidades; Arquitectura (`app.py`, `pages/`, `src/`); Integración artefactos; UI por página; Flujo usuario; Limitaciones |
| Archivos | `mvp-web/README.md`, `app.py`, `pages/*.py`, `src/model_registry.py`, `scripts/export_model_artifacts.py`, `scripts/validate_artifacts.py` |
| Figuras | Capturas UI (TODO: generar al redactar); figuras embebidas en `assets/historical_validation/` |
| Tablas | Modelos y requisitos de filas; métricas de `historical_metrics.json` |
| Conclusiones | MVP funcional; HAR recomendado; autonomía runtime; no sustituye validación formal |

---

### 4.11. Pruebas (`pruebas.tex`)

| Ámbito | Evidencia |
|--------|-----------|
| Pipeline | Informes fases 0, 1, 11, 14 (anti-leakage) |
| MVP | `tests/` (75 tests): predictors, walk-forward, integración, artefactos |
| Exportación | `validate_artifacts.py` |

---

### 4.12. Manual (`manual.tex`)

| Bloque | Comandos |
|--------|----------|
| Pipeline | Ejecutar `src/phaseN_*.py` en orden 0→14 |
| Export MVP | `python scripts/export_model_artifacts.py` (desde repo con datos) |
| MVP | `pip install -r requirements.txt && streamlit run app.py` |
| Tests MVP | `python3 -m pytest tests/` |

---

### 4.13. Conclusiones (`conclusiones.tex`)

| Sección | Mensaje |
|---------|---------|
| Validación modelo | Pipeline 0–13 coherente; BTC ambiguo para caos |
| Predictiva | HAR-logRV mejor modelo práctico; AR fuerte; kNN aporta pero no lidera |
| MVP | Herramienta demostrativa exportada; limitaciones legales/técnicas |
| Futuro | GARCH/EGARCH, más activos, intervalos, IAAFT completo, etc. |

---

### 4.14. Anexos (`anexos.tex`)

| Anexo | Contenido |
|-------|-----------|
| Glosario | AMI, HAR, Theiler, AAFT, etc. |
| Relación tesis | Tabla 0–14 ↔ Olmedo ya consolidada en `Fases_segun_tesis.md` |
| Detalle fases | Parámetros completos 0–14 |
| Tablas extendidas | BIC AR 1–100, BDS completo, k 2–200, surrogados |
| Instalación | `btc-volatility` + `mvp-web` |
| Estructura repos | Árbol de tres repositorios |

---

## 5. Orden de redacción recomendado

| Orden | Capítulo | Motivo |
|-------|----------|--------|
| 1 | Objetivos | Fija alcance (14 fases + MVP + prudencia caos) |
| 2 | Antecedentes (§ HAR, reconstrucción, predicción) | Desbloquea Resultados e Implementación |
| 3 | Implementación (fases 0–14) | Trabajo ya hecho; incluye Fase 14 nueva |
| 4 | **Resultados** | Núcleo empírico; integrar tabla Fase 14 |
| 5 | **MVP web** | Código disponible; enlaza con Fase 14 |
| 6 | Conclusiones | Con Resultados + MVP cerrados |
| 7 | Introducción + Resumen | Sintesis final |
| 8 | Diseño + Requisitos + Pruebas + Manual | Formalización |
| 9 | Planificación | TODO fechas |
| 10 | Anexos + bibliografía | Al estabilizar referencias |

**Paralelizable:** Implementación fases 0–10 ↔ Antecedentes teórico; MVP ↔ Manual usuario.

---

## 6. Cuerpo principal vs anexos

| Contenido | Cuerpo | Anexo |
|-----------|--------|-------|
| Ecuación HAR y coeficientes principales | ✓ | Coeficientes completos + validación |
| Tabla comparativa AR / kNN / HAR (5000 pts) | ✓ | `test_full` 34512 pts |
| Embedding, surrogados, mapa logístico (1 figura c/u) | ✓ | Resto de figuras fase |
| Arquitectura MVP (diagrama + flujo) | ✓ | Capturas pantalla completas |
| Código `phase14_har_logrv_mvp.py` | Referencia | Listing opcional |
| 75 tests MVP | Resumen | Lista por módulo |
| Mapeo fase ↔ Olmedo 0–14 | Tabla resumen | ✓ detalle |
| `export_model_artifacts.py` | Párrafo en MVP | ✓ pseudocódigo |

---

## 7. Matriz de trazabilidad

| Capítulo memoria | Fases | Cap. Olmedo | Archivos clave |
|------------------|-------|-------------|----------------|
| Introducción | — | 1, 9 | `FASES.md` |
| Objetivos | 0–14 + MVP | 10 | — |
| Antecedentes § finanzas/HAR | 1–2, 14 | 9→sustit. | `phase14_har_logrv_mvp_report.md` |
| Antecedentes § dinámica no lineal | 5–10 | 4–7 | informes fases 7–10 |
| Antecedentes § logístico | 13 | 2 | `phase13_logistic_map_validation_report.md` |
| Implementación | 0–14 | 4–8, 10 | `src/phase*.py` |
| Resultados § caracterización | 0–5 | 4, 10 | fases 2–5 |
| Resultados § no lineal | 6–7 | 6 | fases 6–7 |
| Resultados § reconstrucción/cuantif. | 8–10 | 5, 7 | fases 8–10 |
| Resultados § predicción local | 11–12 | 8 | fases 11–12 |
| **Resultados § cierre HAR** | **14** | 8 (parcial) | **`phase14_*`**, **`har_logrv_model.json`** |
| Resultados § control sintético | 13 | 2 | fase 13 |
| MVP web | 14 (+ refs 8, 11–13) | 8, 10 | **`mvp-web/`** |
| Pruebas | 0, 1, 11, 14, MVP | — | `tests/`, informes |
| Conclusiones | 0–14, MVP | 11 | síntesis §1.5 |
| Anexo relación tesis | 0–14 | 1–11 |`Fases_segun_tesis.md` |

---

## 8. Reglas de estilo

### 8.1. Tono

1. Español académico claro; evitar grandilocuencia y muletillas vacías.  
2. Presente histórico para trabajo realizado; condicional para hipótesis no probadas.  
3. Separar **tres hilos narrativos:** (i) análisis dinámico no lineal; (ii) competición predictiva; (iii) MVP operativo.

### 8.2. Evidencia

4. Toda cifra con fuente (`phaseN_*` o `historical_metrics.json`).  
5. Etiquetar (a)(b)(c)(d) al interpretar.  
6. No inferir caos de BDS, D2, Lyapunov positivo ni de kNN > persistencia.

### 8.3. Modelos predictivos

7. **HAR-logRV:** “modelo práctico recomendado”; mejora **ligera** vs AR(49).  
8. **AR(49):** “benchmark lineal fuerte”; central en fases 6 y 11.  
9. **kNN:** “predictor no lineal experimental”; vinculado a reconstrucción (fases 8–12).  
10. **Mini-HAR (MVP):** “recalibración local experimental”; no reemplaza validación histórica.

El Bloque 5 dice que kNN no supera AR (correcto para fases 11–12). En el Bloque 7 añade que HAR supera marginalmente a AR. En la memoria hay que dejar claro el orden temporal: primero kNN vs AR; después Fase 14 cierra con HAR.

### 8.4. MVP y responsabilidad

11. Repetir disclaimer: no asesoramiento, no dirección de precio, no caos demostrado.  
12. Distinguir validación histórica formal (fases 11–14) vs walk-forward en ventana cargada (MVP).

### 8.5. Olmedo

13. Citar como referencia metodológica; no copiar extensión filosófica cap. 1.  
14. HAR no está en Olmedo: citar literatura de volatilidad realizada / Corsi.

### 8.6. Tabla de formulaciones

| Evitar | Preferir |
|--------|----------|
| “BTC es caótico” | “evidencia mixta; compatible con estructura temporal no trivial” |
| “HAR demuestra caos” | “HAR captura memoria multiescala de volatilidad” |
| “kNN es el mejor modelo” | “kNN mejora persistencia; HAR y AR lideran en test formal” |
| “El MVP valida el TFG” | “El MVP lleva a la práctica el modelo exportado de Fase 14” |
| “AR(49) pierde siempre” | “AR(49) sigue siendo benchmark fuerte; HAR mejora marginalmente en Fase 14” |

### 8.7. Frase guía

> El TFG desarrolla una metodología de análisis de series temporales con dinámica no lineal, la comprueba en un sistema caótico conocido, la aplica con cautela a volatilidad de BTC y cierra con un **modelo HAR exportable** y un **MVP web**. En BTC no se demuestra caos determinista; se documentan indicios, utilidad predictiva parcial y límites.

---

## 9. Checklist por capítulo

- [ ] Cifras respaldadas por informe/tabla/figura del repo  
- [ ] Distinción (a)(b)(c)(d) donde corresponda  
- [ ] Fase 14 citada en Resultados, Implementación, MVP y Conclusiones  
- [ ] MVP descrito con archivos reales de `mvp-web/`  
- [ ] No afirmar caos en BTC  
- [ ] Mejora HAR vs AR cuantificada sin exagerar  
- [ ] Limitaciones en el mismo apartado que el resultado  
- [ ] `pfcbib.bib` incluye Olmedo, Takens, Rosenstein, BDS, **HAR/Corsi**  
- [ ] `implementacion.tex` ampliado con secciones 13 y 14  

---

## 10. Próximos pasos inmediatos

1. **Actualizar estructura LaTeX:** añadir secciones Fase 13 y 14 en `implementacion.tex`; posible sección “Comparación HAR” en `resultados.tex`.  
2. **Revisar `resumen.tex`** con tríada: análisis no lineal + HAR + MVP.  
3. **Redactar Objetivos** (1–2 h) como primer capítulo operativo.  
4. **Copiar al `img/` de memoria** figuras clave: `phase14_ar_knn_har_metrics.svg`, `phase8_embedding_2d.svg`, capturas MVP.  
5. **Bibliografía:** añadir referencia HAR (Corsi, 2009) en `pfcbib.bib`.

---

*Plan revisado tras incorporación de Fase 14 (HAR-logRV) y MVP Streamlit en `mvp-web`. No sustituye la redacción de capítulos.*
