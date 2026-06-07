# Resumen por capítulos de la tesis base

Documento de referencia: **Olmedo Fernández (2001), _Análisis de series temporales en el contexto de la economía dinámica no lineal y caótica. Aplicación a datos de la economía española_**.

Objetivo de este resumen:
- Reordenar el contenido de la tesis por capítulos, siguiendo un formato parecido a `FASES.md`.
- Detectar qué partes coinciden con tu validación de modelo.
- Ver qué bloques teóricos tendrás que escribir o adaptar en la memoria del TFG.
- Separar lo que es **marco teórico**, **metodología**, **aplicación empírica** y **predicción**.

---

## CAPÍTULO 1: Determinismo, azar y caos

**Contenidos:**
- Determinismo clásico.
- Azar epistemológico vs azar ontológico.
- Relación entre azar, incertidumbre e ignorancia.
- Caos determinista como ruptura de la dicotomía determinismo/aleatoriedad.
- Complejidad cuantitativa vs complejidad cualitativa.
- Paradigma lineal, equilibrio y estabilidad.
- Paradigma no lineal, inestabilidad, retroalimentación y tiempo histórico.
- Introducción de la complejidad en economía y econometría.

**Relación con mis fases:**
- Relación indirecta con todas las fases.
- Justifica por qué no basta con mirar solo modelos lineales.
- Da contexto filosófico y económico a la idea de estudiar BTC como sistema complejo.
- Conecta con la prudencia de mis conclusiones: comportamiento irregular no implica automáticamente azar puro ni caos demostrado.

**Output para mi memoria:**
- Bloque introductorio sobre determinismo, aleatoriedad, complejidad y caos.
- Justificación de por qué una serie económica/financiera puede requerir herramientas no lineales.
- Explicación de que no linealidad es condición necesaria, pero no suficiente, para caos.

**Conclusión:**
- Este capítulo sirve para la **motivación general** del TFG, no para la parte computacional.
- Debería resumirse mucho en la memoria: no copiar su enfoque filosófico largo, sino usarlo para abrir el problema.

---

## CAPÍTULO 2: Sistemas dinámicos y caos

**Contenidos:**
- Hitos clásicos de la teoría del caos:
  - Lorenz.
  - Smale.
  - Ruelle-Takens.
  - Li-Yorke.
  - Feigenbaum.
- Definición de sistema dinámico.
- Sistemas continuos y discretos.
- Sistemas autónomos y no autónomos.
- Sistemas lineales y no lineales.
- Sistemas deterministas y estocásticos.
- Solución, flujo, trayectoria y órbita.
- Sensibilidad a las condiciones iniciales.
- Propiedad de mezcla.
- Soluciones periódicas.
- Conjuntos invariantes.
- Atractores:
  - punto fijo;
  - ciclo límite;
  - órbita cuasiperiódica;
  - atractor extraño.
- Caos topológico.
- Ecuación logística.
- Diagrama de Feigenbaum.
- Universalidad y periodo 3.

**Relación con mis fases:**
- Relación fuerte con la **Fase 13**.
- La tesis usa la ecuación logística como ejemplo teórico; yo la uso como validación metodológica sintética.
- También conecta con las fases 8–10 porque la reconstrucción intenta representar una dinámica subyacente.
- La noción de órbita/trayectoria ayuda a explicar por qué se construyen vectores de estado.

**Output para mi memoria:**
- Definir sistema dinámico.
- Explicar diferencia entre sistema continuo y discreto.
- Explicar solución/orbita/trayectoria con ejemplos simples.
- Introducir sensibilidad a condiciones iniciales.
- Presentar el mapa logístico como caso controlado usado para validar el pipeline.

**Conclusión:**
- Este capítulo es clave para justificar la **Fase 13**.
- En la memoria conviene usarlo de forma aplicada: menos historia, más definiciones operativas.

---

## CAPÍTULO 3: Cuantificación del caos: dimensión fractal, entropía y exponentes de Liapunov

**Contenidos:**
- Dimensión fractal.
- Curva de Koch como ejemplo.
- Dimensión de Hausdorff.
- Dimensión box-counting.
- Dimensión de información.
- Dimensión de Liapunov.
- Dimensión de autosimilaridad.
- Exponentes de Liapunov:
  - caso unidimensional;
  - estabilidad de puntos fijos;
  - estabilidad de ciclos;
  - caso multidimensional;
  - significado de exponente positivo.
- Entropía:
  - entropía de Shannon;
  - entropía métrica;
  - relación entre desorden, información y sensibilidad.

**Relación con mis fases:**
- Relación directa con la **Fase 9**.
- Mi Fase 9 calcula:
  - dimensión de correlación aproximada;
  - Lyapunov por Rosenstein;
  - entropía de permutación.
- La tesis desarrolla el marco teórico general de esas métricas.
- Mi trabajo añade comparación explícita con serie barajada y lectura más prudente.

**Output para mi memoria:**
- Definir qué intenta medir cada indicador:
  - dimensión: complejidad geométrica;
  - Lyapunov: divergencia local de trayectorias;
  - entropía: irregularidad/información.
- Aclarar que estos indicadores no prueban caos por sí solos en datos financieros.
- Justificar por qué se comparan con barajados/surrogados.

**Conclusión:**
- Este capítulo es el soporte teórico de mi bloque de cuantificación.
- En mi memoria debe aparecer, pero con una advertencia clara: en BTC estos indicadores son **exploratorios**, no demostraciones.

---

## CAPÍTULO 4: Series temporales. Caracterización

**Contenidos:**
- Series temporales: caracterización, modelización y predicción.
- Caracterización gráfica.
- Correlograma.
- Función de autocorrelación, ACF.
- Función de autocorrelación parcial, PACF.
- Análisis espectral.
- Espectro poblacional.
- Espectro muestral.
- Periodograma.
- Gráfico de recurrencia.
- Caracterización directa vía espacio de estados.
- Caracterización indirecta vía predicción.
- Redes neuronales como enfoque de aprendizaje.

**Relación con mis fases:**
- Relación directa con:
  - **Fase 2:** visualización temporal y estadísticos.
  - **Fase 4:** ACF, PACF y periodograma.
  - **Fase 5:** gráficos de recurrencia.
  - **Fase 11:** caracterización indirecta mediante predicción.
- Es el capítulo más parecido a la primera mitad de mi validación.
- La tesis usa estas herramientas para preparar la serie antes del análisis no lineal; yo hago lo mismo con BTC.

**Output para mi memoria:**
- Definir media, varianza, covarianza y autocorrelación antes de usar ACF.
- Explicar ACF y PACF como herramientas de dependencia lineal.
- Explicar periodograma como herramienta de periodicidad/frecuencia.
- Explicar gráficos de recurrencia como visualización de patrones repetidos.
- Justificar la elección de `log_rv_past_12` como serie principal.

**Conclusión:**
- Este capítulo es fundamental para escribir la parte metodológica de mis fases 2, 4 y 5.
- Aquí encaja justo lo que comentó el tutor: antes de usar ACF/PACF/periodograma hay que dar contexto matemático.

---

## CAPÍTULO 5: Series temporales. Reconstrucción

**Contenidos:**
- Reconstrucción del espacio de estados.
- Funciones conjugadas.
- Absorción topológica.
- Inmersión.
- Absorción diferencial.
- Teorema de Whitney.
- Teorema de Takens.
- Principio de invariancia.
- Reconstrucción por retardos.
- Enfoque matricial del embedding.
- Elección del tiempo de retardo:
  - información mutua;
  - descomposición en valores singulares.
- Elección de la dimensión de embedding:
  - falsos vecinos cercanos;
  - método de Cao;
  - invariantes del atractor;
  - SVD.

**Relación con mis fases:**
- Relación directa con la **Fase 8**.
- Mi Fase 8 reproduce la estructura metodológica:
  - selección de `tau` con AMI;
  - selección de `m` con FNN;
  - contraste con Cao;
  - construcción del embedding;
  - visualización 2D/3D;
  - comparación con serie barajada.
- La tesis usa Takens como base teórica de la reconstrucción, igual que debería aparecer en mi memoria.

**Output para mi memoria:**
- Explicar qué es reconstruir el espacio de estados.
- Definir el vector retardado:
  - `X_t = [x_t, x_{t-tau}, ..., x_{t-(m-1)tau}]`.
- Explicar por qué hay que elegir `tau` y `m`.
- Explicar AMI, FNN y Cao sin excesivo detalle técnico.
- Justificar que mi `m=5` es operativo, no una dimensión real demostrada del sistema.

**Conclusión:**
- Este capítulo es probablemente el más importante para mi bloque de reconstrucción.
- La memoria debe copiar la lógica, pero no la seguridad: en BTC no debo afirmar que he encontrado un atractor determinista limpio.

---

## CAPÍTULO 6: Series temporales. Estacionariedad y no linealidad

**Contenidos:**
- Estacionariedad.
- Gráfico media-desviación típica.
- Contrastes de raíces unitarias.
- Extracción del componente cíclico.
- Contrastes de no linealidad:
  - gráfico de recurrencia;
  - BDS;
  - biespectro de Hinich;
  - Keenan;
  - Tsay;
  - RESET de Ramsey;
  - no linealidad en media;
  - no linealidad en varianza;
  - efectos ARCH;
  - contraste de Kaplan.
- Nivel de significación.
- Potencia de los contrastes.

**Relación con mis fases:**
- Relación directa con:
  - **Fase 3:** estacionariedad ADF/KPSS y rolling moments.
  - **Fase 6:** filtrado lineal AR y análisis de residuos.
  - **Fase 7:** Ljung-Box, ARCH-LM, BDS y barajado.
- La tesis usa varios contrastes; mi pipeline selecciona menos, pero más adecuados al tiempo y al enfoque computacional del TFG.
- Mi trabajo añade una separación más clara entre serie original y residuos del filtro lineal.

**Output para mi memoria:**
- Definir estacionariedad en media y varianza.
- Explicar por qué una serie no estacionaria puede falsear análisis posteriores.
- Justificar ADF/KPSS como contraste práctico.
- Explicar BDS como contraste de independencia/no linealidad, no como prueba directa de caos.
- Explicar ARCH-LM y Ljung-Box sobre cuadrados como evidencia de dependencia en varianza.

**Conclusión:**
- Este capítulo justifica mis fases 3, 6 y 7.
- Para la memoria no hace falta meter todos los tests de la tesis; mejor explicar bien los que realmente he usado.

---

## CAPÍTULO 7: Series temporales. Cuantificación de la dinámica caótica

**Contenidos:**
- Cuantificación del atractor reconstruido.
- Dimensión de correlación.
- Problemas de correlación temporal.
- Limitaciones de la dimensión de correlación.
- Estimación de exponentes de Liapunov:
  - método de Wolf;
  - métodos indirectos;
  - redes neuronales.
- Entropía métrica.
- Tasa de entropía coarse-grained.
- Análisis cuantitativo de recurrencia.
- Contrastes complementarios:
  - residuos de Brock;
  - shuffling;
  - datos subrogados;
  - elección de hipótesis nula;
  - elección del estadístico discriminante.

**Relación con mis fases:**
- Relación directa con:
  - **Fase 9:** D2, Lyapunov, entropía.
  - **Fase 10:** barajado, phase-randomized y AAFT.
- La tesis usa shuffling y subrogados como refuerzo de las métricas de caos.
- Mi trabajo hace algo muy parecido, pero aplicado a BTC y con una lectura más conservadora.

**Output para mi memoria:**
- Explicar Grassberger-Procaccia/D2 de forma breve.
- Explicar Rosenstein como aproximación práctica al máximo exponente de Lyapunov.
- Explicar entropía de permutación como alternativa computacional simple.
- Explicar datos barajados y subrogados:
  - barajado conserva marginal y destruye orden;
  - phase randomization conserva espectro aproximadamente;
  - AAFT conserva marginal y estructura lineal aproximada.
- Incluir limitaciones: muestra finita, ruido, no estacionariedad, elección de `tau`, `m`, Theiler window y rango de ajuste.

**Conclusión:**
- Este capítulo es el puente entre reconstrucción y afirmaciones sobre dinámica caótica.
- En mi TFG debe usarse para reforzar una conclusión prudente: hay estructura temporal, pero no demostración fuerte de caos determinista en BTC.

---

## CAPÍTULO 8: Series temporales. Predicción

**Contenidos:**
- Predicción en series temporales.
- Relación entre predicción y exponente de Lyapunov.
- Predicción en el espacio de estados reconstruido.
- Enfoque global:
  - predictor polinómico;
  - bases radiales.
- Enfoque local:
  - vecinos próximos;
  - media de vecinos;
  - media ponderada;
  - regresión local.
- Métodos directos e indirectos.
- Dilema sesgo-varianza.
- Redes neuronales:
  - feedforward;
  - recurrentes;
  - FIR.
- Caracterización mediante predicción.
- Predicción en presencia de ruido:
  - amplificación;
  - distorsión;
  - límites de predecibilidad.

**Relación con mis fases:**
- Relación directa con:
  - **Fase 11:** predicción local kNN.
  - **Fase 12:** robustez de k, m y tau.
  - **Fase 14:** modelo HAR-logRV como cierre predictivo práctico.
  - **MVP web:** materialización operativa de la predicción.
- La tesis compara predicción local, modelos lineales y redes neuronales.
- Mi trabajo compara media histórica, persistencia, AR(49), kNN y HAR-logRV.
- Mi resultado es más prudente: kNN mejora persistencia, pero no supera AR(49); HAR-logRV mejora ligeramente a AR(49) y queda como modelo práctico recomendado por simplicidad, interpretabilidad y exportación al MVP.

**Output para mi memoria:**
- Explicar predicción local en espacio reconstruido.
- Definir vecino próximo y media de k vecinos.
- Explicar el papel de `k`:
  - k pequeño: más local, más varianza;
  - k grande: más suave, más sesgo.
- Conectar con sesgo-varianza.
- Presentar AR como benchmark lineal.
- Presentar HAR-logRV como modelo de memoria multiescala de volatilidad realizada:
  - última hora (`log_rv_past_12`);
  - últimas 4 horas (`log_rv_past_48`);
  - último día (`log_rv_past_288`).
- Separar validación histórica formal y uso operativo en MVP.
- Interpretar que mejorar a persistencia no equivale a demostrar caos.

**Conclusión:**
- Este capítulo justifica mis fases 11, 12 y parte de la Fase 14.
- En la memoria debería ser una sección aplicada y clara: “si la reconstrucción o la memoria multiescala contienen información útil, deben mejorar referencias simples y lineales”.

---

## CAPÍTULO 9: No linealidades en el mercado de trabajo

**Contenidos:**
- Características del desempleo.
- Factores macroeconómicos del crecimiento del desempleo.
- Productividad.
- Tipo de interés real.
- Shocks de demanda.
- Precios de importación e impuestos.
- Sindicatos.
- Beneficios del desempleo.
- Desajuste oferta-demanda.
- Dinámica empleo/desempleo con curvas de oferta y demanda.
- Oferta de trabajo no lineal.
- Demanda de trabajo no lineal.
- Enfoque de flujos.
- Tasa de salida del desempleo no lineal.
- Ajuste salarial no lineal.

**Relación con mis fases:**
- Relación débil con mi validación de modelo.
- Este capítulo sirve a la tesis para justificar su variable empírica: desempleo.
- En mi TFG, el equivalente sería justificar por qué estudiar BTC/volatilidad realizada tiene sentido como sistema financiero complejo.
- No hay una fase técnica equivalente directa.

**Output para mi memoria:**
- No copiar este contenido.
- Usarlo solo como modelo de estructura:
  - primero justificar la variable económica;
  - después aplicar herramientas.
- En mi caso, habría que escribir un bloque propio sobre:
  - mercados financieros;
  - BTC;
  - volatilidad;
  - clustering;
  - alta frecuencia;
  - posible no linealidad.

**Conclusión:**
- Este capítulo no se traslada casi nada al TFG salvo la idea de contextualizar la variable.
- Para mi memoria, el capítulo equivalente debería ser “Contexto financiero y volatilidad de BTC”.

---

## CAPÍTULO 10: No linealidad y caos en la evolución del desempleo en España. Aplicación a la predicción

**Contenidos:**
- Aplicación empírica completa.
- Serie usada:
  - paro registrado mensual en España;
  - INEM;
  - enero de 1964 a marzo de 2001;
  - 447 observaciones.
- Visualización de la serie.
- Gráfico de recurrencia.
- Detección de no estacionariedad.
- Transformación logarítmica.
- Diferenciación o componente cíclica para trabajar con una serie más estacionaria.
- Contrastes de no linealidad.
- Reconstrucción del espacio de estados.
- Selección de retardo y dimensión.
- Cuantificación del caos:
  - dimensión de correlación;
  - Lyapunov;
  - entropía;
  - recurrencia;
  - falsos vecinos;
  - Cao.
- Comparación con permutaciones.
- Contraste con datos subrogados.
- Predicción:
  - vecinos próximos;
  - media de vecinos;
  - media ponderada;
  - regresión lineal local;
  - redes neuronales;
  - comparación con modelo lineal.
- Conclusión empírica de la tesis:
  - presencia de no linealidad;
  - indicios de caos;
  - dimensión de absorción alrededor de 6;
  - predicción no lineal útil en ciertos horizontes.

**Relación con mis fases:**
- Es el capítulo más parecido a mi validación completa.
- Equivalencias principales:
  - selección y preparación de datos → **Fases 0–1**.
  - visualización y estadísticos → **Fase 2**.
  - estacionariedad → **Fase 3**.
  - ACF/PACF/periodograma/recurrencia → **Fases 4–5**.
  - filtrado lineal y residuos → **Fase 6**.
  - no linealidad → **Fase 7**.
  - reconstrucción → **Fase 8**.
  - cuantificación → **Fase 9**.
  - shuffling/subrogados → **Fase 10**.
  - predicción local → **Fases 11–12**.
  - validación sintética logística → **Fase 13**, que la tesis usa más como teoría previa que como validación separada.
  - cierre predictivo HAR-logRV → **Fase 14**, aportación propia basada en literatura de volatilidad realizada.
  - aplicación web → **MVP**, implementación práctica posterior al estudio técnico.

**Output para mi memoria:**
- Este capítulo puede servir como plantilla narrativa:
  1. Presentar serie.
  2. Caracterizarla.
  3. Transformarla si hace falta.
  4. Comprobar estacionariedad.
  5. Comprobar dependencia lineal.
  6. Comprobar no linealidad.
  7. Reconstruir espacio de estados.
  8. Cuantificar dinámica.
  9. Comparar con barajados/subrogados.
  10. Evaluar predicción.
  11. Cerrar con un modelo práctico exportable.
  12. Explicar la implementación operativa sin confundirla con la validación teórica.
- En mi memoria, la diferencia central será que BTC ofrece resultados más ambiguos que el desempleo de la tesis.
- Mi conclusión debe ser menos fuerte: estructura temporal y predictibilidad parcial, pero no prueba concluyente de caos. La Fase 14 y el MVP deben presentarse como cierre práctico, no como demostración adicional de caos.

**Conclusión:**
- Este capítulo es el equivalente directo a mi bloque de “Validación de modelo”.
- Mi trabajo está más desarrollado computacionalmente en validación, robustez y control sintético, pero debe mantener una interpretación más cauta.

---

## CAPÍTULO 11: Conclusiones

**Contenidos:**
- Complejidad en economía.
- Complejidad cualitativa vs cuantitativa.
- Retroalimentación.
- Enfoque sistémico.
- Importancia de la no linealidad.
- Complejidad endógena vs exógena.
- Características de un sistema determinista caótico.
- Mercado de trabajo como sistema complejo.
- Detección de no linealidad y caos en series económicas.
- Líneas futuras de investigación.

**Relación con mis fases:**
- Relación con el cierre global del TFG.
- Conecta con la conclusión final de mis fases:
  - hay estructura temporal;
  - hay dependencia no lineal o no puramente lineal;
  - hay predictibilidad parcial;
  - no se demuestra caos de forma fuerte en BTC;
  - el pipeline sí funciona en el mapa logístico sintético.
  - HAR-logRV es el modelo práctico recomendado para la aplicación;
  - el MVP convierte el pipeline en una herramienta demostrativa y reproducible.

**Output para mi memoria:**
- Inspiración para el capítulo de conclusiones.
- Separar resultados técnicos de interpretación:
  - qué se ha detectado;
  - qué no se puede afirmar;
  - qué limitaciones hay;
  - qué trabajo futuro queda.
- Posibles líneas futuras:
  - ampliar el MVP con intervalos de incertidumbre;
  - despliegue web del MVP si se quiere pasar de prototipo local a demo pública;
  - otros activos;
  - otras frecuencias;
  - modelos GARCH/EGARCH;
  - redes neuronales;
  - embeddings alternativos;
  - predicción multi-horizonte;
  - validación con más periodos de mercado.

**Conclusión:**
- Este capítulo sirve como modelo de cierre.
- En mi TFG la conclusión debe ser más escéptica que la tesis: el objetivo no es vender caos, sino validar una metodología computacional.

---

## CAPÍTULOS 12 Y 13: Índice de figuras y bibliografía

**Contenidos:**
- Índice de figuras.
- Bibliografía.

**Relación con mis fases:**
- No tienen equivalencia metodológica directa.
- Sí sirven como referencia para:
  - construir lista de figuras;
  - citar correctamente;
  - ordenar bibliografía.

**Output para mi memoria:**
- Preparar un índice de figuras si la plantilla lo requiere.
- Crear el `.bib` con las referencias usadas:
  - Takens;
  - Grassberger-Procaccia;
  - Rosenstein;
  - Theiler;
  - Kantz/Schreiber;
  - BDS;
  - literatura de volatilidad financiera;
  - Corsi/HAR para volatilidad realizada;
  - tesis de Olmedo.

**Conclusión:**
- Son partes formales, no metodológicas.
- Deben tratarse al final de la escritura de la memoria.

---

# Mapa rápido de equivalencias tesis ↔ mis fases

| Bloque de la tesis | Capítulos | Equivalente en mis fases |
|---|---:|---|
| Motivación: determinismo, azar, complejidad | 1 | Introducción y motivación |
| Sistemas dinámicos y caos | 2 | Marco teórico + Fase 13 |
| Medidas de caos | 3 | Fase 9 |
| Caracterización de series | 4 | Fases 2, 4, 5 |
| Reconstrucción por retardos | 5 | Fase 8 |
| Estacionariedad y no linealidad | 6 | Fases 3, 6, 7 |
| Cuantificación dinámica y contrastes | 7 | Fases 9, 10 |
| Predicción no lineal | 8 | Fases 11, 12 |
| Cierre predictivo práctico | 8 + literatura HAR | Fase 14 |
| Contexto económico aplicado | 9 | Contexto financiero/BTC en mi memoria |
| Aplicación empírica completa | 10 | Fases 0–14 + MVP |
| Conclusiones | 11 | Cierre de resultados, MVP y trabajo futuro |
| Bibliografía/figuras | 12–13 | Parte formal de la memoria |

---

# Qué cosas tengo claramente en común con la tesis

**Coincidencias fuertes:**
- Uso de series temporales económicas/financieras.
- Planteamiento desde dinámica no lineal y caos.
- Caracterización inicial de la serie.
- Transformaciones para hacer la serie más tratable.
- Análisis gráfico.
- ACF/PACF.
- Análisis espectral/periodograma.
- Gráficos de recurrencia.
- Estacionariedad.
- Contrastes de no linealidad.
- Reconstrucción por retardos.
- Selección de `tau`.
- Selección de `m`.
- Falsos vecinos.
- Cao.
- Dimensión de correlación.
- Lyapunov.
- Entropía.
- Barajado/shuffling.
- Datos subrogados.
- Predicción local por vecinos.
- Comparación con modelo lineal.

**Diferencias importantes:**
- La tesis trabaja con desempleo mensual y 447 observaciones.
- Mi trabajo trabaja con BTC a 5 minutos y más de 245.000 observaciones.
- La tesis afirma indicios de caos con más fuerza.
- Mi validación es más prudente: detecta estructura temporal y predictibilidad parcial, pero no caos concluyente.
- Mi pipeline incluye una validación sintética explícita con mapa logístico.
- Mi pipeline añade un cierre HAR-logRV que no procede de la tesis, sino de la literatura específica de volatilidad realizada.
- Mi trabajo termina en un MVP Streamlit funcional, no solo en una validación empírica.
- Mi trabajo tiene un componente computacional más claro:
  - scripts;
  - CSV;
  - SVG;
  - JSON;
  - validación anti-leakage;
  - train/validation/test;
  - exportación de artefactos;
  - tests automatizados;
  - MVP web autónomo.

---

# Qué debería escribir en mi memoria a partir de esto

## Bloques teóricos mínimos

1. Determinismo, azar, caos y complejidad.
2. Sistemas dinámicos discretos.
3. Series temporales financieras y volatilidad.
4. Caracterización lineal:
   - media;
   - varianza;
   - covarianza;
   - ACF;
   - PACF;
   - periodograma.
5. Estacionariedad.
6. Recurrencia.
7. No linealidad.
8. Reconstrucción de Takens.
9. AMI, FNN y Cao.
10. Dimensión de correlación, Lyapunov y entropía.
11. Datos barajados y subrogados.
12. Predicción local kNN y benchmarks.
13. Validación sintética con mapa logístico.
14. HAR-logRV y memoria multiescala de volatilidad realizada.
15. Arquitectura del MVP como implementación del modelo exportado.

## Bloques empíricos mínimos

1. Datos BTC.
2. Limpieza y validación.
3. Construcción de volatilidad realizada.
4. Selección de serie principal.
5. Caracterización.
6. Estacionariedad.
7. Análisis lineal.
8. Recurrencia.
9. Filtrado AR.
10. Contrastes no lineales.
11. Reconstrucción.
12. Cuantificación.
13. Surrogados.
14. Predicción local.
15. Robustez.
16. Mapa logístico.
17. HAR-logRV y comparación final de modelos.
18. Implementación MVP.
19. Conclusiones.

---

# Conclusión global

La tesis de Olmedo tiene una estructura muy parecida a lo que he hecho, pero en otro dominio y con menos validación computacional moderna. La mayor coincidencia está en el recorrido metodológico:

```text
caracterizar serie
→ estudiar estacionariedad
→ detectar dependencia/no linealidad
→ reconstruir espacio de estados
→ cuantificar dinámica
→ comparar con barajados/subrogados
→ evaluar predicción
```

Mi validación de modelo encaja muy bien como versión computacional actualizada de esa lógica. La diferencia clave es interpretativa: en la memoria no conviene afirmar que BTC sea caótico. Lo defendible es:

```text
La serie de volatilidad realizada de BTC muestra estructura temporal, dependencia en varianza y cierta predictibilidad. Las herramientas de dinámica no lineal revelan patrones compatibles con una dinámica compleja, pero los resultados no permiten concluir de forma fuerte la existencia de caos determinista. La validación con mapa logístico confirma que el pipeline sí detecta estructura caótica cuando el sistema subyacente es conocido. Como cierre aplicado, HAR-logRV captura de forma simple la memoria multiescala de la volatilidad y se exporta a un MVP web que demuestra la viabilidad operativa del estudio.
```
