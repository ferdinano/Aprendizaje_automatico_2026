# Informe de Proyecto de Machine Learning: Predicción de tipo de cambio, tasa de interes y Créditos.

## 1. Análisis Exploratorio y Regresión Lineal

**Observaciones de la gráfica:**

![Grafico Regresion Linela](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/Regresion%20Lineal.png)

El gráfico de dispersión relaciona los montos de préstamos para "Construcción" (eje X) con el "Tipo de Cambio" (eje Y)Se observa claramente la formación de distintos grupos o "regímenes" económicos (marcados por colores: violeta, rojo y verde claro). 
**Análisis:** La relación no es estrictamente lineal en todo el dominio.Se ve un crecimiento exponencial o escalonado. Cuando el tipo de cambio se dispara (puntos rojos y verdes, superando los $800), el volumen de préstamos nominales en construcción aumenta significativamente, lo cual tiene sentido en un contexto inflacionario donde los montos en pesos crecen.



## 2. Modelo Support Vector Regression (SVR) - Objetivo 1
**Objetivo:** Predecir el Tipo de Cambio y la Tasa de Interés a partir de un volumen dado de préstamos.

**SVR sin ajuste (GridSearchCV):** En la primera gráfica de evaluación, vemos que las predicciones (puntos violetas y naranjas) forman líneas casi horizontales y no siguen la "Línea Ideal" diagonal. Esto indica un **fuerte subajuste **. El modelo por defecto no logró capturar la complejidad de los datos.

![Grafico SVR](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/SRV%20sin%20parametro%20enC.png)

**SVR con ajuste de hiperparámetros (Parámetro "C" vía GridSearchCV):** Al optimizar el parámetro de penalización "C", el modelo mejora drásticamente[cite: 3]. [cite_start]Los puntos ahora se alinean mucho mejor sobre la diagonal roja[cite: 3]. [cite_start]Esto demuestra la importancia crítica de `GridSearchCV` para encontrar el equilibrio exacto en los hiperparámetros[cite: 3].
![Grafico SVR](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/SRV%20con%20parametro%20enC.png)

* [cite_start]**Prueba de SVR:** Al ingresar un diccionario con un alto volumen de créditos, el modelo predijo un escenario macroeconómico complejo: Tipo de Cambio de $1253.30 ARS y Tasa del 70.46%[cite: 4]. [cite_start]Lo más valioso aquí es la **regla de negocio asociada**: el sistema detecta que la tasa supera el 65% y arroja una alerta pertinente recomendando "Congelar colocación de préstamos a tasa fija y exigir mayores garantías", demostrando gran utilidad práctica para la gestión de riesgos[cite: 4].
![Grafico SVR](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/SRV.png)
---

## 3. Modelo Árbol de Decisión (Multi-Output) - Objetivo 2
[cite_start]**Objetivo:** Predecir la demanda en todas las líneas de crédito ingresando un Tipo de Cambio y Tasa de Interés (Prueba de Estrés Macro)[cite: 7].

![Grafico SVR](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/Arbol.png)

* [cite_start]**Gráfico y Evaluación del Árbol:** La evaluación arroja un ajuste casi perfecto, con valores de $R^2$ superiores a 0.99 en casi todas las categorías (ej. Construcción 0.9887)[cite: 6]. [cite_start]Como estudiante de machine learning, debo advertir que, aunque el gráfico muestre los puntos exactamente sobre la "Línea Ideal", esto suele ser un síntoma de **sobreajuste (overfitting)** si estamos evaluando sobre los datos de entrenamiento[cite: 6]. [cite_start]El árbol ha memorizado los datos[cite: 6].
![Grafico SVR](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/Analisis%20Arbol%20prueba.png)
* [cite_start]**Prueba del Árbol de Decisiones:** Ingresamos el escenario "estresado" que nos devolvió el modelo SVR anterior (TC: $1253.3, Tasa: 70.46%)[cite: 7]. [cite_start]El árbol logra devolver los montos proyectados exactos para cada línea (Construcción, Refacción, Autos, etc.)[cite: 7]. [cite_start]A pesar del posible sobreajuste, operativamente funciona muy bien para devolver un "snapshot" de cómo se vería la cartera de créditos en ese escenario macroeconómico específico.

![Grafico SVR](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/comparacion%20de%20arbol%20y%20SRV.png)

---

## 4. Segmentación con K-Means (Análisis No Supervisado)
[cite_start]**Objetivo:** Agrupar los momentos históricos en regímenes económicos para definir políticas de crédito[cite: 10].
![Grafico SVR](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/kmeans.png)
* [cite_start]**Gráfico K-Means (k=3):** El algoritmo agrupó exitosamente la relación Tasa de interés vs. Tipo de cambio en tres clústeres bien diferenciados por sus centroides (X rojas)[cite: 9]:

    * [cite_start]*Grupo 0 (Violeta):* Tasas bajas e históricamente tipo de cambio bajo (Estabilidad)[cite: 9, 10].
    * [cite_start]*Grupo 2 (Amarillo):* Tipo de cambio medio pero tasas disparadas (Riesgo/Shock de tasas)[cite: 9, 10].
    * [cite_start]*Grupo 1 (Verde/Teal):* Tipo de cambio muy alto con tasas en una franja media-alta (Escenario de devaluación asimilada/volátil)[cite: 9, 10].
* [cite_start]**Prueba K-Means:** Al ingresar un nuevo dato (TC: 1300, Tasa: 70.0), el modelo lo clasifica correctamente en el Clúster 1 (Escenario Volátil) y dispara una recomendación automatizada: *"Luz amarilla, ajustar plazos"*[cite: 10]. [cite_start]Es una excelente implementación para categorizar la coyuntura rápidamente[cite: 10].
![Grafico SVR](https://github.com/ferdinano/Aprendizaje_automatico_2026/blob/main/Predicion%20tipo%20de%20cambio/reports/figures/Kmean%20prueba.png)
---

## 5. Conclusión Final y Recomendaciones

Tras realizar este proyecto y probar los distintos enfoques, esta es mi recomendación para resolver los objetivos propuestos:

1.  **Para el Objetivo 1 (Predecir monto de préstamos según nueva Tasa y Tipo de Cambio):**
    * [cite_start]**Mejor enfoque:** El **Árbol de Decisiones** demostró ser muy capaz para manejar la salida múltiple (predecir todas las carteras de crédito a la vez)[cite: 7]. 
    * [cite_start]*Recomendación de mejora:* Dado que las métricas sugieren sobreajuste ($R^2$ muy altos), recomendaría utilizar un ensamble basado en árboles, como **Random Forest Regressor** (o limitar la profundidad máxima `max_depth` del árbol actual con GridSearchCV)[cite: 6]. Esto ayudará a que las predicciones de préstamos frente a escenarios macroeconómicos nuevos generalicen mejor y no sean tan rígidas.

2.  **Para el Objetivo 2 (Predecir Tasa y Tipo de Cambio en base al volumen inyectado):**
    * [cite_start]**Mejor enfoque:** El modelo **SVR (Support Vector Regression) optimizado con GridSearchCV** es el ganador definitivo aquí[cite: 3]. [cite_start]La optimización del parámetro `C` demostró que este algoritmo es sumamente robusto para entender cómo el volumen de pesos en la calle (préstamos) presiona o predice los valores macroeconómicos (tasa y dólar)[cite: 3, 4].

**Conclusión General del Proyecto:** El ecosistema desarrollado es muy potente. [cite_start]Combinar la capacidad predictiva de los algoritmos supervisados (SVR y Árboles) con las reglas de negocio y clasificación de riesgo arrojadas por **K-Means**, resulta en una herramienta analítica completa que no solo predice números, sino que dicta acciones concretas (como exigir más garantías o acortar plazos) basándose en los datos históricos del mercado[cite: 4, 10].
