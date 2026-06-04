# Mapeo inverso: fases del proyecto → partes de la tesis de Olmedo

Objetivo de este documento:

- Partir de cada fase de mi validación de modelo.
- Indicar qué capítulos/secciones de la tesis sirven como soporte teórico o metodológico.
- Ver qué tengo en común con la tesis y qué partes son propias de mi TFG.
- Usar esto como guía directa para escribir la memoria.

---

## FASE 0: Validación integral de datos

**Qué hago en mi proyecto:**
- Verifico columnas esperadas.
- Compruebo rango temporal.
- Valido frecuencia de 5 minutos.
- Reviso duplicados, huecos, nulos y precios positivos.
- Genero una base limpia antes de construir variables.

**Partes de la tesis relacionadas:**
- **Capítulo 4: Series temporales. Caracterización**.
  - Introducción al tratamiento de series temporales.
  - Necesidad de caracterizar la serie antes de modelizar o predecir.
- **Capítulo 10: Aplicación empírica al desempleo en España**.
  - Presentación de la serie empírica.
  - Descripción del periodo de observación.
  - Preparación inicial de los datos antes del análisis.

**Relación con la tesis:**
- Relación metodológica básica.
- La tesis presenta y prepara su serie de desempleo antes de aplicar herramientas no lineales.
- Mi fase es más informática y más explícita: incluye validaciones automáticas de integridad, frecuencia, duplicados y ausencia de leakage posterior.

**Qué me sirve para la memoria:**
- Justificar que todo análisis posterior depende de la calidad del dato inicial.
- Explicar que, antes de hablar de no linealidad o caos, hay que garantizar que la serie está bien construida.
- Esta fase puede ir en el bloque de **datos y preprocesamiento**.

**Conclusión:**
- La tesis no desarrolla una fase de validación de datos tan formal como la mía, pero el capítulo 10 cumple una función equivalente de presentación de la serie empírica.

---

## FASE 1: Construcción de variables de volatilidad realizada

**Qué hago en mi proyecto:**
- Construyo `log_close`.
- Calculo retornos logarítmicos.
- Calculo `r_t²`, `|r_t|`, rango high-low logarítmico, volumen y trades transformados.
- Construyo volatilidad realizada pasada y futura.
- Aplico transformación logarítmica a la volatilidad.
- Elimino filas sin histórico o sin futuro.
- Valido no-leakage.

**Partes de la tesis relacionadas:**
- **Capítulo 4: Series temporales. Caracterización**.
  - Transformaciones iniciales de la serie.
  - Caracterización antes de reconstruir o predecir.
- **Capítulo 6: Estacionariedad y no linealidad**.
  - Transformaciones para trabajar con series más tratables.
  - Estacionariedad y extracción de componentes.
- **Capítulo 10: Aplicación empírica**.
  - Transformación logarítmica.
  - Tratamiento de la serie antes de los contrastes y reconstrucción.

**Relación con la tesis:**
- La tesis transforma la serie de desempleo para hacerla más adecuada al análisis.
- Mi trabajo hace algo equivalente, pero adaptado a una serie financiera de alta frecuencia.
- La gran diferencia es que yo no trabajo directamente con precio, sino con una variable derivada: la volatilidad realizada logarítmica.

**Qué me sirve para la memoria:**
- Explicar por qué el precio de BTC no es la serie principal.
- Justificar que la volatilidad realizada es más adecuada para estudiar clustering, dependencia temporal y posible estructura no lineal.
- Introducir la notación de retornos y volatilidad realizada.

**Conclusión:**
- Esta fase es el equivalente financiero de la transformación empírica que la tesis hace con el desempleo. En mi memoria debe quedar claro que la serie final no aparece “gratis”: se construye con una lógica económica y estadística.

---

## FASE 2: Visualización temporal y estadísticos

**Qué hago en mi proyecto:**
- Represento precio, log-precio, retornos, valor absoluto de retornos, volatilidad realizada, volumen y trades.
- Calculo media, desviación típica, percentiles, asimetría y curtosis.
- Detecto eventos extremos.
- Confirmo visualmente clustering de volatilidad.

**Partes de la tesis relacionadas:**
- **Capítulo 4: Series temporales. Caracterización**.
  - Análisis gráfico.
  - Herramientas generales de caracterización.
- **Capítulo 10: Aplicación empírica**.
  - Aplicación de herramientas generales.
  - Representación gráfica de la serie.
  - Primeras evidencias de patrones, cambios y comportamiento irregular.

**Relación con la tesis:**
- Coincidencia fuerte.
- La tesis empieza la aplicación empírica mirando la serie antes de aplicar técnicas más complejas.
- Mi fase hace lo mismo, pero con más salidas computacionales y con estadísticos descriptivos más sistemáticos.

**Qué me sirve para la memoria:**
- Escribir una sección de **análisis descriptivo inicial**.
- Mostrar que los retornos tienen colas pesadas y que la volatilidad se agrupa en periodos.
- Justificar por qué `log_rv_past_12` pasa a ser la serie principal.

**Conclusión:**
- Esta fase encaja directamente con el capítulo 4 y con el inicio del capítulo 10. Es una fase de observación inicial, no de demostración de caos.

---

## FASE 3: Tests de estacionariedad

**Qué hago en mi proyecto:**
- Aplico ADF y KPSS a precio, log-precio, retornos, valor absoluto de retornos y `log_rv_past_12`.
- Analizo momentos móviles.
- Comparo primera y segunda mitad de la muestra.
- Decido qué series son más adecuadas para análisis posterior.

**Partes de la tesis relacionadas:**
- **Capítulo 6: Series temporales. Estacionariedad y no linealidad**.
  - Estacionariedad.
  - Gráfico media-desviación típica.
  - Contrastes de raíces unitarias.
  - Extracción de componente cíclico.
- **Capítulo 10: Aplicación empírica**.
  - Detección de no estacionariedad.
  - Transformaciones para trabajar con una serie más estable.

**Relación con la tesis:**
- Coincidencia directa.
- La tesis insiste en que antes de aplicar técnicas de caos hay que comprobar la estacionariedad o, al menos, tratar el problema.
- Mi fase usa ADF/KPSS y rolling moments como versión práctica y moderna de esa idea.

**Qué me sirve para la memoria:**
- Definir estacionariedad de forma simple: media, varianza y dependencia temporal estables.
- Explicar por qué una serie no estacionaria puede inducir falsas señales de estructura.
- Justificar que el precio/log-precio no son adecuados como serie principal.
- Justificar que los retornos y la volatilidad realizada son más razonables.

**Conclusión:**
- Esta fase debe escribirse con apoyo claro en el capítulo 6. Es una fase de control metodológico: evita que el análisis no lineal se apoye en una serie mal condicionada.

---

## FASE 4: Análisis de correlación y periodograma

**Qué hago en mi proyecto:**
- Calculo ACF y PACF de retornos, valor absoluto de retornos y `log_rv_past_12`.
- Analizo retardos relevantes: 1, 12, 288 y 2016.
- Calculo periodogramas.
- Busco picos espectrales diarios y semanales.
- Confirmo que la volatilidad tiene persistencia fuerte.

**Partes de la tesis relacionadas:**
- **Capítulo 4: Series temporales. Caracterización**.
  - Análisis de la correlación lineal.
  - Función de autocorrelación.
  - Función de autocorrelación parcial.
  - Correlograma.
  - Análisis espectral.
  - Espectro poblacional y muestral.
  - Periodograma.
- **Capítulo 10: Aplicación empírica**.
  - Aplicación de herramientas generales a la serie real.

**Relación con la tesis:**
- Coincidencia muy fuerte.
- Este es uno de los puntos donde la tesis te da exactamente el marco que necesitas.
- La tesis no salta directamente a caos: primero caracteriza linealmente la serie.
- Yo hago lo mismo y además uso escalas naturales del mercado: hora, día y semana.

**Qué me sirve para la memoria:**
- Antes de presentar ACF, definir covarianza y autocorrelación.
- Antes de PACF, explicar que mide dependencia parcial eliminando retardos intermedios.
- Antes del periodograma, explicar que transforma la serie al dominio de frecuencias para detectar ciclos.
- Concluir que los retornos son poco predecibles linealmente, pero la volatilidad sí tiene persistencia.

**Conclusión:**
- Esta fase es de las más fáciles de conectar con la tesis. El capítulo 4 debería ser la base teórica principal para escribirla.

---

## FASE 5: Gráficos de recurrencia de ventanas representativas

**Qué hago en mi proyecto:**
- Selecciono ventanas quiet, high-volatility, recent y middle.
- Normalizo cada ventana.
- Construyo recurrence plots para `r`, `|r|` y `log_rv_past_12`.
- Comparo patrones visuales.
- Detecto diagonales y bloques de persistencia en la volatilidad.

**Partes de la tesis relacionadas:**
- **Capítulo 4: Series temporales. Caracterización**.
  - Gráfico de recurrencia como herramienta general.
- **Capítulo 6: Estacionariedad y no linealidad**.
  - Gráfico de recurrencia como herramienta para detectar no linealidad o patrones no triviales.
- **Capítulo 7: Cuantificación de la dinámica caótica**.
  - Análisis de cuantificación a partir del gráfico de recurrencia.
- **Capítulo 10: Aplicación empírica**.
  - Uso de recurrencia en la aplicación al desempleo.

**Relación con la tesis:**
- Coincidencia directa.
- La tesis usa recurrencia como herramienta visual y como apoyo a la caracterización no lineal.
- Mi trabajo usa recurrencia antes de reconstruir el espacio de estados, como diagnóstico exploratorio.

**Qué me sirve para la memoria:**
- Explicar que un recurrence plot marca cuándo dos estados/valores son similares.
- Enfatizar que no prueba caos por sí solo.
- Usarlo como evidencia visual de persistencia, cambios de régimen y estructura temporal.
- Comparar la textura de retornos frente a la de volatilidad.

**Conclusión:**
- Esta fase conecta con capítulos 4, 6, 7 y 10. En la memoria debe presentarse como visualización de estructura, no como prueba concluyente.

---

## FASE 6: Filtrado lineal AR(p)

**Qué hago en mi proyecto:**
- Divido train/test.
- Ajusto modelos AR(p) con p entre 1 y 100.
- Selecciono AR(49) por BIC.
- Obtengo residuos.
- Analizo ACF/PACF de residuos.
- Aplico Ljung-Box.
- Comparo recurrencia de residuos frente a la serie original.

**Partes de la tesis relacionadas:**
- **Capítulo 6: Estacionariedad y no linealidad**.
  - Contrastes de no linealidad.
  - Necesidad de distinguir dependencia lineal y no lineal.
  - Linealidad en media y en varianza.
- **Capítulo 7: Cuantificación de la dinámica caótica**.
  - Contrastes complementarios.
  - Contraste de los residuos de Brock.
  - Comparación de estructura tras eliminar componentes lineales.
- **Capítulo 8: Predicción**.
  - Comparación con modelos lineales.
- **Capítulo 10: Aplicación empírica**.
  - Comparación de técnicas y uso de modelos lineales como referencia.

**Relación con la tesis:**
- Relación fuerte, aunque mi implementación es más explícita.
- La tesis trata la necesidad de no confundir no linealidad con dependencia lineal no eliminada.
- Mi fase crea un benchmark lineal y una serie de residuos para preguntar si queda estructura más allá de AR.

**Qué me sirve para la memoria:**
- Explicar por qué no basta con aplicar BDS o reconstrucción directamente a la serie original.
- Justificar el AR como filtro lineal de referencia.
- Presentar BIC como criterio de selección de orden.
- Explicar que si los residuos conservan estructura, hay motivación para analizar no linealidad residual.

**Conclusión:**
- Esta fase es una mejora metodológica clara respecto a una lectura ingenua de la tesis. Sirve para separar dependencia lineal fuerte de estructura no lineal potencial.

---

## FASE 7: Contrastes de no linealidad

**Qué hago en mi proyecto:**
- Aplico Ljung-Box sobre cuadrados.
- Aplico ARCH-LM sobre residuos.
- Aplico BDS en ventanas representativas.
- Comparo ACF de cuadrados original frente a barajada.
- Uso residuos del AR y serie original.

**Partes de la tesis relacionadas:**
- **Capítulo 6: Series temporales. Estacionariedad y no linealidad**.
  - Contraste BDS.
  - Linealidad en media y varianza.
  - Contrastes de efectos de no linealidad en varianza.
  - Nivel de significación y potencia de los contrastes.
  - Otros contrastes: Hinich, Keenan, Tsay, RESET, Kaplan.
- **Capítulo 7: Cuantificación de la dinámica caótica**.
  - Contrastes complementarios.
  - Shuffling.
  - Datos subrogados.
- **Capítulo 10: Aplicación empírica**.
  - Contrastes de no linealidad en la serie real.

**Relación con la tesis:**
- Coincidencia directa.
- La tesis revisa más contrastes de los que yo uso.
- Mi trabajo selecciona una batería más compacta: BDS, ARCH-LM, Ljung-Box sobre cuadrados y barajado.
- Es mejor tener menos tests bien interpretados que muchos tests difíciles de defender.

**Qué me sirve para la memoria:**
- Explicar que BDS rechaza independencia, no demuestra caos.
- Explicar que ARCH-LM y Ljung-Box sobre cuadrados detectan dependencia en varianza.
- Conectar esta fase con el fenómeno financiero de clustering de volatilidad.
- Usar el barajado como control empírico del orden temporal.

**Conclusión:**
- Esta fase está muy respaldada por el capítulo 6. La interpretación debe ser prudente: evidencia de dependencia no lineal/heterocedasticidad, no demostración de caos.

---

## FASE 8: Reconstrucción del espacio de estados

**Qué hago en mi proyecto:**
- Calculo información mutua media para elegir `tau`.
- Selecciono `tau = 137` como primer mínimo local.
- Calculo falsos vecinos cercanos.
- Uso Cao como contraste.
- Selecciono `m = 5` como dimensión práctica.
- Construyo el embedding retardado.
- Visualizo proyecciones 2D/3D.
- Comparo AMI original frente a barajada.

**Partes de la tesis relacionadas:**
- **Capítulo 5: Series temporales. Reconstrucción**.
  - Teorema de Takens.
  - Reconstrucción por retardos.
  - Enfoque matricial del embedding.
  - Elección del tiempo de retardo.
  - Método de la información mutua.
  - Elección de la dimensión de absorción.
  - Falsos vecinos.
  - Método de Cao.
  - Método de invariantes del atractor.
- **Capítulo 10: Aplicación empírica**.
  - Reconstrucción del espacio de estados en la serie de desempleo.

**Relación con la tesis:**
- Coincidencia máxima.
- Esta fase es prácticamente la traducción computacional directa del capítulo 5.
- La diferencia clave es interpretativa: en mi caso `m=5` no se vende como dimensión verdadera del atractor, sino como dimensión operativa.

**Qué me sirve para la memoria:**
- Explicar el vector de retardos:
  - `X_t = [x_t, x_{t-τ}, ..., x_{t-(m-1)τ}]`.
- Explicar qué problema resuelve Takens: reconstruir una dinámica no observada completamente usando una sola variable medida.
- Explicar AMI, FNN y Cao.
- Justificar la ventana efectiva de memoria de 45.7 horas.
- Incluir la discrepancia con Cao como limitación metodológica.

**Conclusión:**
- Esta fase debe apoyarse casi por completo en el capítulo 5. Es uno de los bloques centrales de la memoria.

---

## FASE 9: Cuantificación dinámica

**Qué hago en mi proyecto:**
- Estimo dimensión de correlación con Grassberger-Procaccia.
- Estimo Lyapunov máximo aproximado con Rosenstein.
- Calculo entropía de permutación.
- Uso submuestras por coste computacional.
- Comparo original frente a barajada.
- Concluyo que hay estructura, pero no prueba fuerte de caos.

**Partes de la tesis relacionadas:**
- **Capítulo 3: Cuantificación del caos**.
  - Dimensión fractal.
  - Exponentes de Liapunov.
  - Entropía.
- **Capítulo 7: Series temporales. Cuantificación de la dinámica caótica**.
  - Dimensión de correlación.
  - Problemas por correlación temporal.
  - Inconvenientes de la dimensión de correlación.
  - Exponentes de Liapunov.
  - Entropía métrica.
  - Contrastes complementarios.
- **Capítulo 10: Aplicación empírica**.
  - Cuantificación del caos en la serie real.

**Relación con la tesis:**
- Coincidencia directa.
- La tesis proporciona el marco conceptual de las medidas.
- Mi fase usa versiones computacionales concretas y más prudentes:
  - D2 aproximada.
  - Rosenstein en vez de una estimación teórica perfecta.
  - Entropía de permutación en vez de entropía métrica clásica.

**Qué me sirve para la memoria:**
- Explicar qué mide cada indicador:
  - D2: complejidad geométrica del atractor reconstruido.
  - Lyapunov: divergencia local de trayectorias cercanas.
  - Entropía: irregularidad/orden temporal.
- Añadir claramente las limitaciones.
- Explicar por qué comparar con barajado es obligatorio.

**Conclusión:**
- Esta fase se apoya en capítulos 3 y 7. La frase clave para la memoria debería ser: “los indicadores sugieren estructura dinámica no trivial, pero no permiten afirmar caos determinista en BTC”.

---

## FASE 10: Contrastes con barajado y datos subrogados

**Qué hago en mi proyecto:**
- Genero series barajadas.
- Genero series phase-randomized.
- Genero series AAFT.
- Comparo D2, Lyapunov y entropía.
- Calculo percentiles, p-values empíricos y estadísticos de separación.
- Evalúo si la estructura se explica solo por marginal o por dependencia lineal.

**Partes de la tesis relacionadas:**
- **Capítulo 7: Series temporales. Cuantificación de la dinámica caótica**.
  - Contraste de shuffling.
  - Contraste de datos subrogados.
  - Elección de hipótesis nula.
  - Elección del estadístico discriminante.
- **Capítulo 10: Aplicación empírica**.
  - Comparación con permutaciones y subrogados en la aplicación real.

**Relación con la tesis:**
- Coincidencia muy fuerte.
- La tesis usa shuffling/subrogados como refuerzo de las métricas de caos.
- Mi fase formaliza esto de forma más computacional y reproducible.
- Además, separo tres niveles:
  - barajado: destruye orden temporal.
  - phase randomization: conserva estructura lineal/espectral aproximada.
  - AAFT: conserva marginal y estructura lineal aproximada.

**Qué me sirve para la memoria:**
- Explicar que no basta con comparar contra ruido blanco.
- Definir la hipótesis nula de cada tipo de surrogate.
- Interpretar los resultados como evidencia de estructura temporal y posible componente no lineal, pero no caos por sí solo.
- Usar esta fase como defensa metodológica fuerte frente a críticas.

**Conclusión:**
- Esta fase es una extensión moderna del capítulo 7. Es clave para evitar vender como “caos” lo que podría ser dependencia lineal o distribución no gaussiana.

---

## FASE 11: Predicción local kNN

**Qué hago en mi proyecto:**
- Divido train, validation y test.
- Comparo media histórica, persistencia, AR(49), 1-NN y kNN.
- Busco vecinos en el espacio reconstruido sin leakage.
- Uso Theiler window.
- Selecciono `k=50` por validación.
- Evalúo en test.
- Compruebo que kNN mejora persistencia, pero no supera AR(49).

**Partes de la tesis relacionadas:**
- **Capítulo 8: Series temporales. Predicción**.
  - Predicción en espacio de estados.
  - Enfoque local.
  - Método de vecinos próximos.
  - Media de vecinos.
  - Métodos directos e indirectos.
  - Dilema sesgo-varianza.
  - Predicción en presencia de ruido.
- **Capítulo 10: Aplicación empírica**.
  - Comparación de técnicas de predicción.
  - Predicción local y comparación con técnicas alternativas.

**Relación con la tesis:**
- Coincidencia directa.
- La tesis dedica un capítulo entero a predicción y luego la aplica empíricamente.
- Mi fase implementa la parte local con controles modernos de train/validation/test y anti-leakage.
- Mi resultado es más escéptico: hay predictibilidad local, pero el AR sigue ganando.

**Qué me sirve para la memoria:**
- Explicar que una reconstrucción útil debería aportar capacidad predictiva.
- Definir kNN local en espacio reconstruido.
- Explicar por qué se compara contra persistencia y AR.
- Explicar el papel de Theiler window para evitar vecinos trivialmente cercanos en el tiempo.
- Interpretar que mejorar persistencia no equivale a demostrar caos.

**Conclusión:**
- Esta fase se apoya casi totalmente en el capítulo 8. En la memoria debe cerrar el ciclo: caracterización → reconstrucción → cuantificación → predicción.

---

## FASE 12: Robustez de parámetros `k`, `m` y `tau`

**Qué hago en mi proyecto:**
- Amplío la búsqueda de `k` hasta 200.
- Comparo `m=5` frente a `m=14`, motivado por Cao.
- Mantengo `tau=137`.
- Evalúo si la configuración principal era estable.
- Confirmo que `m=5` funciona mejor que `m=14` para predicción local.
- Confirmo que AR(49) sigue siendo mejor.

**Partes de la tesis relacionadas:**
- **Capítulo 5: Reconstrucción**.
  - Elección de dimensión de embedding.
  - FNN y Cao.
  - Sensibilidad a los parámetros de reconstrucción.
- **Capítulo 8: Predicción**.
  - Dilema sesgo-varianza.
  - Vecinos próximos.
  - Predicción en presencia de ruido.
  - Influencia de los parámetros en la predecibilidad.
- **Capítulo 10: Aplicación empírica**.
  - Comparación de técnicas y parámetros en la aplicación real.

**Relación con la tesis:**
- Relación metodológica clara, aunque mi fase es más de robustez computacional.
- La tesis discute la elección de parámetros; yo hago una comprobación empírica posterior.
- Esta fase refuerza que `m=5` es una decisión práctica, no una verdad teórica.

**Qué me sirve para la memoria:**
- Presentar esta fase como análisis de sensibilidad.
- Explicar que aumentar dimensión no siempre mejora: puede aparecer curse of dimensionality.
- Conectar `k` con sesgo-varianza.
- Defender que las conclusiones no dependen únicamente de una elección arbitraria de parámetros.

**Conclusión:**
- Esta fase no tiene un capítulo único equivalente, pero se apoya en los capítulos 5 y 8. Es una aportación propia importante de mi validación.

---

## FASE 13: Validación metodológica con mapa logístico caótico

**Qué hago en mi proyecto:**
- Genero una serie sintética con el mapa logístico `x[t+1] = 4 x[t](1-x[t])`.
- Añado versiones con ruido pequeño y moderado.
- Repito selección de `tau`, `m`, embedding, Lyapunov, entropía y predicción local.
- Compruebo que el pipeline detecta estructura clara en un sistema caótico conocido.
- Comparo comportamiento sintético con BTC.

**Partes de la tesis relacionadas:**
- **Capítulo 2: Sistemas dinámicos y caos**.
  - Ecuación logística.
  - Universalidad.
  - Periodo 3.
  - Diagrama de Feigenbaum.
  - Sensibilidad a condiciones iniciales.
- **Capítulo 3: Cuantificación del caos**.
  - Lyapunov, dimensión y entropía en sistemas caóticos.
- **Capítulo 5: Reconstrucción**.
  - Reconstrucción por retardos.
- **Capítulo 7: Cuantificación de series reconstruidas**.
  - Aplicación de medidas de cuantificación.
- **Capítulo 8: Predicción**.
  - Predicción local en dinámica reconstruida.

**Relación con la tesis:**
- Relación conceptual muy fuerte.
- La tesis usa el mapa logístico como ejemplo teórico dentro del marco de caos.
- Mi trabajo lo convierte en una fase experimental de validación metodológica.
- Esta es una aportación importante de mi TFG: comprobar el pipeline en un sistema donde sí se conoce la dinámica subyacente.

**Qué me sirve para la memoria:**
- Usar el mapa logístico como experimento de control.
- Explicar que si el método detecta estructura en el mapa logístico, pero en BTC los resultados son ambiguos, la ambigüedad viene del dato real, no necesariamente de que el pipeline esté mal.
- Mostrar el efecto del ruido sobre reconstrucción y predicción.

**Conclusión:**
- Esta fase se apoya sobre todo en el capítulo 2, pero conecta con toda la metodología posterior. Es una pieza fuerte para defender la validez del enfoque computacional.

---

# Mapa resumen fase → tesis

| Fase de mi proyecto | Parte principal de la tesis | Relación |
|---|---|---|
| Fase 0: validación de datos | Cap. 4 y Cap. 10 | Preparación de la serie empírica |
| Fase 1: variables de volatilidad | Cap. 4, Cap. 6 y Cap. 10 | Transformación y construcción de serie tratable |
| Fase 2: visualización y estadísticos | Cap. 4 y Cap. 10 | Caracterización inicial |
| Fase 3: estacionariedad | Cap. 6 y Cap. 10 | Control previo a no linealidad/caos |
| Fase 4: ACF, PACF, periodograma | Cap. 4 y Cap. 10 | Dependencia lineal y análisis espectral |
| Fase 5: recurrencia | Cap. 4, Cap. 6, Cap. 7 y Cap. 10 | Visualización de estructura temporal |
| Fase 6: filtro AR y residuos | Cap. 6, Cap. 7, Cap. 8 y Cap. 10 | Separar dependencia lineal de posible no linealidad |
| Fase 7: contrastes no lineales | Cap. 6, Cap. 7 y Cap. 10 | BDS, varianza condicional, shuffling |
| Fase 8: reconstrucción | Cap. 5 y Cap. 10 | Takens, AMI, FNN, Cao, embedding |
| Fase 9: cuantificación dinámica | Cap. 3, Cap. 7 y Cap. 10 | D2, Lyapunov, entropía |
| Fase 10: surrogados | Cap. 7 y Cap. 10 | Shuffling, phase randomization, AAFT |
| Fase 11: predicción kNN | Cap. 8 y Cap. 10 | Predicción local y benchmarks |
| Fase 12: robustez | Cap. 5, Cap. 8 y Cap. 10 | Sensibilidad a parámetros |
| Fase 13: mapa logístico | Cap. 2, Cap. 3, Cap. 5, Cap. 7 y Cap. 8 | Validación sintética del pipeline |

---

# Agrupación por bloques de memoria

## Bloque 1: Datos y variable de estudio

**Fases:** 0, 1 y 2.

**Tesis relacionada:** capítulos 4 y 10.

**Qué escribir:**
- Origen de los datos.
- Validación de integridad.
- Construcción de retornos y volatilidad realizada.
- Estadísticos descriptivos.
- Justificación de `log_rv_past_12` como serie principal.

---

## Bloque 2: Caracterización lineal y estacionariedad

**Fases:** 3 y 4.

**Tesis relacionada:** capítulos 4 y 6.

**Qué escribir:**
- Estacionariedad.
- ADF/KPSS.
- Media, varianza, covarianza.
- ACF/PACF.
- Periodograma.
- Interpretación: retornos poco autocorrelados, volatilidad persistente.

---

## Bloque 3: Evidencia exploratoria de estructura no lineal

**Fases:** 5, 6 y 7.

**Tesis relacionada:** capítulos 4, 6 y 7.

**Qué escribir:**
- Recurrence plots.
- Filtrado AR.
- Residuos.
- Ljung-Box sobre cuadrados.
- ARCH-LM.
- BDS.
- Barajado.
- Interpretación: estructura temporal y dependencia en varianza, no caos demostrado.

---

## Bloque 4: Reconstrucción y cuantificación dinámica

**Fases:** 8, 9 y 10.

**Tesis relacionada:** capítulos 3, 5, 7 y 10.

**Qué escribir:**
- Takens.
- Embedding retardado.
- AMI para `tau`.
- FNN/Cao para `m`.
- D2.
- Lyapunov.
- Entropía.
- Shuffling y surrogados.
- Interpretación prudente.

---

## Bloque 5: Predicción local y robustez

**Fases:** 11 y 12.

**Tesis relacionada:** capítulo 8 y capítulo 10.

**Qué escribir:**
- Predicción local en espacio reconstruido.
- kNN.
- Benchmarks: media, persistencia, AR.
- Train/validation/test.
- Robustez de `k` y `m`.
- Resultado: kNN mejora persistencia, pero no supera AR.

---

## Bloque 6: Validación sintética

**Fase:** 13.

**Tesis relacionada:** capítulo 2 y conexión con capítulos 3, 5, 7 y 8.

**Qué escribir:**
- Mapa logístico como sistema caótico conocido.
- Aplicación del mismo pipeline.
- Comparación con BTC.
- Conclusión: el método funciona en caos controlado; BTC exige interpretación prudente.

---

# Qué fases son más “tesis pura” y cuáles son más aportación propia

## Muy alineadas con la tesis

- Fase 3: estacionariedad.
- Fase 4: ACF/PACF/periodograma.
- Fase 5: recurrencia.
- Fase 8: reconstrucción por retardos.
- Fase 9: cuantificación dinámica.
- Fase 10: barajado y subrogados.
- Fase 11: predicción local.

## Adaptaciones financieras propias

- Fase 1: construcción de volatilidad realizada.
- Fase 2: selección de `log_rv_past_12` como serie principal.
- Fase 6: filtro AR(49) como benchmark/residuo explícito.
- Fase 7: ARCH-LM y dependencia en varianza centrada en volatilidad financiera.

## Aportaciones computacionales claras

- Fase 0: validación integral de datos.
- Fase 6: pipeline reproducible de filtrado AR.
- Fase 10: surrogados sistemáticos con métricas y p-values empíricos.
- Fase 11: train/validation/test con no-leakage.
- Fase 12: robustez de parámetros.
- Fase 13: validación sintética completa.

---

# Conclusión global del mapeo inverso

La validación de modelo sigue casi la misma lógica metodológica que la tesis, pero aplicada a BTC y con una capa computacional más fuerte:

```text
validar datos
→ construir una serie adecuada
→ caracterizarla
→ comprobar estacionariedad
→ analizar dependencia lineal
→ buscar indicios de no linealidad
→ reconstruir espacio de estados
→ cuantificar dinámica
→ comparar con barajados/subrogados
→ evaluar predicción
→ validar el pipeline en un sistema sintético conocido
```

La tesis sirve como columna vertebral teórica. Mi trabajo añade tres diferencias importantes:

1. **Dato financiero de alta frecuencia:** BTC a 5 minutos, no desempleo mensual.
2. **Mayor control computacional:** validación, no-leakage, train/validation/test, salidas reproducibles.
3. **Interpretación más prudente:** estructura temporal y predictibilidad parcial sí; caos determinista en BTC, no demostrado.

La frase que debería guiar la memoria es:

```text
El objetivo no es demostrar que BTC sea caótico, sino explorar hasta qué punto las herramientas de dinámica no lineal permiten caracterizar, reconstruir y predecir parcialmente la volatilidad realizada, comparando siempre contra referencias lineales y controles sintéticos.
```
