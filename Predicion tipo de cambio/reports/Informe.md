# Informe de Proyecto de Machine Learning: Predicción de tipo de cambio, tasa de interes y Créditos.

## 1. Análisis Exploratorio y Regresión Lineal

**Observaciones de la gráfica:**

![Grafico](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/Regresion%20Lineal.png)

El gráfico de dispersión relaciona los montos de préstamos para "Construcción" (eje X) con el "Tipo de Cambio" (eje Y)Se observa claramente la formación de distintos grupos marcados por colores: violeta, rojo y verde claro. 
La relación no es estrictamente lineal en todo el dominio.Se ve un crecimiento exponencial o escalonado. Cuando el tipo de cambio se dispara (puntos rojos y verdes, superando los $800), el volumen de préstamos nominales en construcción aumenta significativamente, lo cual tiene sentido en un contexto inflacionario donde los montos en pesos crecen.



## 2. Modelo Support Vector Regression (SVR) - Objetivo 1
**Objetivo: Predecir el Tipo de Cambio y la Tasa de Interés a partir de un volumen dado de préstamos.

**SVR sin ajuste (GridSearchCV):En la primera gráfica de evaluación, vemos que las predicciones (puntos violetas y naranjas) forman líneas casi horizontales y no siguen la "Línea Ideal" diagonal. Esto indica un fuerte subajuste. El modelo por defecto no logró capturar la complejidad de los datos.

![Grafico](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/SRV%20sin%20parametro%20enC.png)

**SVR con ajuste de hiperparámetros** (Parámetro "C" vía GridSearchCV):Al optimizar el parámetro de penalización "C", el modelo mejora drásticamente. Los puntos ahora se alinean mucho mejor sobre la diagonal roja. Esto demuestra la importancia crítica de `GridSearchCV` para encontrar el equilibrio exacto en los hiperparámetros.

![Grafico](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/SRV%20con%20parametro%20enC.png)

**Comparacion de K_means y SVR:** Al ingresar un diccionario con un alto volumen de créditos, el modelo predijo un escenario complejo: Tipo de Cambio de $1253.30 ARS y Tasa del 70.46%. Lo más valioso aquí es la **regla asociada**: el sistema detecta que la tasa supera el 65% y arroja una alerta pertinente recomendando "Congelar colocación de préstamos a tasa fija y exigir mayores garantías", demostrando gran utilidad práctica para la gestión de riesgos.

![Grafico](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/SRV.png)


## 3. Modelo Árbol de Decisión (Multi-Output) - Objetivo 2
**Objetivo:** Predecir la demanda en todas las líneas de crédito ingresando un Tipo de Cambio y Tasa de Interés.

![Grafico](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/Arbol.png)

**Gráfico y Evaluación del Árbol:** La evaluación arroja un ajuste casi perfecto, con valores de $R^2$ superiores a 0.99 en casi todas las categorías (ej. Construcción 0.9887).

![Grafico](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/Analisis%20Arbol%20prueba.png)

  **Prueba del Árbol de Decisiones:** Ingresamos el escenario "estresado" que nos devolvió el modelo SVR anterior (TC: $1253.3, Tasa: 70.46%). El árbol logra devolver los montos proyectados exactos para cada línea (Construcción, Refacción, Autos, etc.). A pesar del posible sobreajuste, operativamente funciona muy bien.

![Grafico](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/comparacion%20de%20arbol%20y%20SRV.png)



## 4. Segmentación con K-Means (Análisis No Supervisado)
**Objetivo:** Agrupar los momentos históricos en regímenes económicos para definir políticas de crédito.

![Grafico](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/kmeans.png)

**Gráfico K-Means (k=3):** El algoritmo agrupó exitosamente la relación Tasa de interés vs. Tipo de cambio en tres clústeres bien diferenciados por sus centroides (X rojas):

**Grupo 0 (Violeta):** Tasas bajas e históricamente tipo de cambio bajo (Escenario estable).
**Grupo 1 (Amarillo):** Tipo de cambio medio pero tasas disparadas (Escenario Volatil).
**Grupo 2 (Verde/Teal):** Tipo de cambio muy alto con tasas en una franja media-alta (Escenario de Riesgo).

**Prueba K-Means:** Al ingresar un nuevo dato (TC: 1300, Tasa: 70.0), el modelo lo clasifica correctamente en el Clúster 1 (Escenario Volátil) y dispara una recomendación automatizada: *"Luz amarilla, ajustar plazos".Es una excelente implementación para categorizar la coyuntura rápidamente.

![Grafico](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/Kmean%20prueba.png)

---

## 5. Conclusión Final y Recomendaciones

El ecosistema desarrollado es muy potente. Combinar la capacidad predictiva de los algoritmos supervisados (SVR y Árboles) con las reglas de negocio y clasificación de riesgo arrojadas por **K-Means**, resulta ser una herramienta completa que no solo predice números, sino que dicta acciones concretas (como exigir más garantías o acortar plazos) basándose en los datos históricos del mercado.
