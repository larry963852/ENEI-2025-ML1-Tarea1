# Informe final

**Integrantes**
- dedostorcidos

**Diferencias entre OLS, Ridge y Lasso**
- OLS replica exactamente la solución cerrada y coincide con `LinearRegression`, pero deja coeficientes grandes para `MedInc` (California) y para variables climáticas/temporales (bicicletas), lo que lo vuelve sensible al ruido y a la multicolinealidad.
- Ridge mantiene todos los predictores pero reduce su magnitud; en California amortigua `AveRooms`, `AveBedrms` y los términos geográficos, mientras que en bicicletas suaviza el efecto de clima y hora sin anularlos.
- Lasso obliga a coeficientes cero para señales débiles: en California colapsa `AveOccup`, `Population` y parte de los términos polinomiales; en bicicletas elimina indicadores redundantes (clima suave, flags laborales) y deja solo los drivers principales.

**Efecto de la tasa de aprendizaje en descenso de gradiente**
- Con características estandarizadas, una tasa pequeña (0.01 en vivienda, 0.001 en bicicletas) converge lentamente pero de forma muy estable.
- La tasa mayor usada (0.1 en vivienda, 0.01 en bicicletas) alcanza el mínimo en pocas iteraciones sin desestabilizar el costo, aunque requiere vigilar posibles oscilaciones si se eleva más.
- En ambos conjuntos los parámetros finales coinciden con OLS dentro de la tolerancia numérica, validando la implementación.

**Impacto de la validación cruzada en la regularización**
- `RidgeCV` eligió penalizaciones suaves que prácticamente empatan el error de OLS mientras contienen la varianza al añadir rasgos polinomiales.
- `LassoCV` seleccionó alfas intermedios que promueven sparsity: reduce el error en vivienda gracias a eliminar redundancias y evita sobreajuste en bicicletas, sobre todo con expansiones cuadráticas.
- Los planes con polinomios grado 2 solo son estables con estas alfas óptimas; sin CV el modelo se vuelve inestable o sobreajustado.
