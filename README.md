# Informe del proyecto: Modelos lineales y regularizacion

## Integrantes del equipo
- CHAMORRO ALVA MELVIN
- GARCIA IRAITA LUCY 
- LUNA CARRERA MARISOL

## Configuración del entorno

1. Abre una terminal en la carpeta del proyecto.
2. Crea un entorno virtual con:
    ```bash
    python3 -m venv .venv
    ```
3. Activa el entorno virtual:
    - En Linux/macOS:
      ```bash
      source .venv/bin/activate
      ```
    - En Windows:
      ```bash
      .venv\Scripts\activate
      ```
4. Instala las dependencias con:
    ```bash
    pip install -r requirements.txt
    ```
## Hallazgos principales

### Diferencias entre OLS, Ridge y Lasso
- OLS sirve como linea base y ofrece el mejor ajuste cuando el numero de variables es moderado y no hay penalizacion; sin embargo, es sensible a colinealidad y puede producir coeficientes de gran magnitud.
- Ridge conserva todas las variables pero reduce su magnitud de manera uniforme. En el cuaderno se observa que produce un ligero descenso del error de prueba y coeficientes mas estables frente a cambios en los datos.
- Lasso fuerza algunos coeficientes exactamente a cero. En nuestros experimentos, Lasso mantiene un desempeno similar a Ridge con la ventaja de seleccionar un subconjunto mas compacto de variables, sobre todo cuando se incluyen polinomios.

### Efecto de la tasa de aprendizaje en descenso de gradiente
- Con `alpha = 0.001` el costo disminuye de forma constante pero lenta, necesitando muchas iteraciones para acercarse al optimo.
- Con `alpha = 0.01` se logra un balance ideal: la curva del costo baja rapido y se estabiliza cerca del valor obtenido por la forma cerrada.
- Con `alpha = 0.1` el metodo oscila y tarda en estabilizarse; ilustra que un paso demasiado grande puede alejarse del valle antes de corregirse.

### Influencia de k-fold en la eleccion de la regularizacion
- Se utilizo `KFold` con cinco particiones. RidgeCV y LassoCV exploran automaticamente la malla logaritmica de valores de `alpha` y devuelven la opcion con menor error medio.
- El alpha elegido por validacion cruzada logro mejores metricas que seleccionar un valor a mano, ademas de evitar utilizar el conjunto de prueba para tomar decisiones.
- En las caracteristicas polinomiales la validacion cruzada recomendo alphas mas altos, lo que estabilizo los coeficientes y evito sobreajuste severo.
