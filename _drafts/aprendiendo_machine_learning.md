---
layout: post
title: "Aprendiendo Machine learning"
description: "Mis notas sobre machine learning"
category: daata-science
tags: [pyhton, data-science, machine-learning]
---

A continuacion, voy a empezar a estudiar Machine Learning, aprendiendo desde lo basico, pasando por cada tipo de algoritmo
temas matematicos y aplicando ejemplos en python.

Para mi aprendizaje, estoy siguiendo:
* El libro Introduction to statistical learning with R.
* Para hacerlo mas llevadero, el curso de [edx de microsoft](https://courses.edx.org/courses/course-v1:Microsoft+DAT203.2x+1T2018a/course/),
que cuenta con muy buenos videos y buenas explicaciones. ademas que de aqui voy a sacar los data sets y ejemplos para ir aprendiend.


## Conceptos Basicos:

**Metodos supervisados:**
El aprendizaje supervisado es una técnica para deducir una función a partir de datos de entrenamiento. Los datos de entrenamiento consisten de pares de objetos (normalmente vectores): una componente del par son los datos de entrada y el otro, los resultados deseados. La salida de la función puede ser un valor numérico (como en los problemas de regresión) o una etiqueta de clase (como en los de clasificación). El objetivo del aprendizaje supervisado es el de crear una función capaz de predecir el valor correspondiente a cualquier objeto de entrada válida después de haber visto una serie de ejemplos, los datos de entrenamiento. Para ello, tiene que generalizar a partir de los datos presentados a las situaciones no vistas previamente.
generalmente requiere generar un modelo estadistico para predecir o estimar una salida, basada en una o mas entradas.

**Metodos No supervisados:**
Con los metodos no supervisados, hay entradas pero no salidas supervisadas; se busca aprender cual es la relacion y estructura de los datos.

### Metodos Supervisados


* Llamaremos variables independenties o predictores a los $$X = (x_{1},x_{2},x_{2},....,x_{p})$$, estos son los datos de entrada, $$X$$ es un array de tamaño $$p$$,
e $$Y$$ el valor de salida o variable dependiente. como ejemplo podemos ver a $$x_{1}=edad$$ , $$x_{2}=nivel de educacion$$  $$Y=sueldo$$.
por lo tanto, teniendo informacion de varias personas, con sus datos de edad, nivel de educacion y sueldo. Podemos tratar de usar esta informacion para generar un modelo y  predecir el sueldos.
* En nuestro mundo ideal queremos encontrar una funcion tal que dandole valores de entrada nos de la prediccion:

    $$ Y = f(x) + e $$

    donde $$f$$ es una funcion que no conocemos y $$e$$ es un error.

* Como generar una funcion que sea exactamente la que necesitamos es imposible en la mayoria de los casos, vamos a tratar de estimar a $$f$$

$$ \hat{Y} = \hat{f}(X) $$


Donde $$\hat{f}$$ es una estimacion de nuestra $$f$$ ideal, e $$\hat{Y}$$ es la prediccion de $$Y$$.

* La Exactitud de $$\hat{Y}$$ como predicion de $$y$$, depende de dos cantidades:
     * **Error reducible:** En general $$\hat{f}$$ no sera una estimacion perfecta de $$f$$ y esta inexactitud introduce errores, este error es reducible ya que podemos utilizar la tecnica mas apropiada para estimar a $$f$$, con esto mejorar a $$\hat{f}$$, es el error introducido por el modelo.
     * **Error irreducible:** Aun que podamos obtener la mejor prediccion de $$f$$, nuestra prediccion aun asi tendra error, ya que $$Y$$ es una funcion de $$f$$ y de $$e$$  $$Y = f(x) +  e$$ que por definicion no puede ser predicido usando $$X$$. En otras palabras, nuestro metodo usara un numero finito de datos para generar el modelo,  es posible que por la ausencia de algunas variables importantes que no esten presentes en $$X$$, nunca podamos predecir a $$Y$$ con exactitud, tambien puede haber error en la muestra, a la hora de carga de datos etc.


$$ E(Y-\hat{Y})^2 = E(f(x) + e - \hat{f}(x))^2 = [f(x) - \hat{f}(x)]^2 + Var(e)$$


Donde $$E(Y-\hat{Y})^2$$, es el valor esperado o media del cuadrado de diferencia entre la prediccion, y el valor real de $$Y$$. y $$Var(e)$$ es la varianza asociada al error irreducible.
  * $$[f(x) - \hat{f}(x)]^2$$: es el error reducible.
  * $$Var(e)$$: es el error irreducible.
  
#### Inferencia

Muchas veces, vamos a querer saber como Y es afectado  por $$x_{1},....,x_{p}$$, Vamos a querer estimar $$f$$, pero no necesariamente hacer predicciones de $$Y$$.
Mas especificamente vamos a querer entender la relacion entre $$X$$ e $$Y$$, como $$Y$$ cambia como una funcion de $$x_{1},x_{2},x_{2},....,x_{p}$$.

#### Metodos parametrizados

Los metodos parametrizados se basan en dos pasos:
  1. Se asume una forma funcional de f, por ejemplo podemos asumir que f es de forma lineal, de esta manera reducimos mucho la busqueda del modelo.
  2. Una vez que el modelo y forma de la funcion fue elegido, debemos entrenar el modelo, con los datos de entrenamiento.

Se llama parametrico ya que reducimos el problema a estimar parametros, por ejemplo si usamos una f lineal, debemos estimar los coeficientes del polinomio.
Una desventaja potencial de estos modelos es que el modelo elegido no va a encajar nunca perfectamente con la verdadera forma de $$f$$, por lo tanto la estimacion puede ser pobre.
Podriamos tratar de elefir modelos mas `flexibles`, que puedan adecuarse a differentes posibles formas de $$f$$, pero adecuar a un modelo mas flexible requiere calcular mas paremetros.
Esto puede llevar a un problema conocido como overfitting (sobreadecuar los datos).

#### Metodos no parametrizados

Estos metodos no hacen suposiciones directas sobre $$f$$, en cambio tratan de buscar una estimacion de $$f$$  que se acerque a los datos, lo mas que se pueda.
Algunas ventajas de estos metodos es que al no hacer supociciones de $$f$$ se pueden encontrar varias formas precisas para adecuarse a $$f$$.
La Gran desventaja que tienen estos metodos, es que al no reduci el problema de estimar a f a encontrar unos parametros, un numero mucho mayor de observaciones es necesario para estimar $$f$$.
Tambien el cientifico de datos tiene que elegir con cuanta suavidad va a adecuarse a los datos.. ya que podria pasarse y hacer un overfit (sobreadecuarse a los datos), y no generaria buenas predicciones.
 
 
### Seleccionando el modelo adecuado
 
Una tarea muy importante es la de, dado un data set, decidir cual es el modelo o metodo que produce el mejor resultado. Esta seleccion es una de las partes mas desafiantes de el aprendizaje estadistico.

Para poder evaluar la performance de un metodo un un data set especifico, necesitamos medir cuan cercana es la prediccion a los datos observados.

#### Medidas de Problemas de Regresion
  * Haciendo regression la medida mas comun es `mean square error (MSE)`.

  $$ MSE = \frac{1}{n}\sum_{1}^{n}(y_{i} - \hat{f}(x_{i}))^2 $$
  
  Donde $$\hat{f}(x_{i})$$ es la prediccion de da $$\hat{f}$$ para la i-esima  observacion.
   
  * MSE sera pequeña si la prediccion esta muy cerca de los valores reales, y sera grande si para alguna observacion las predicciones y los valores reales differen mucho.
  * Tenemos dos tipos de MSE:
    * **Trainging MSE**: generada a partir de los datos usados para entrenar nuestro modelo, la cual no nos interesa mucho, ya que nosotros queremos saber si predice bien, con datos no usados para entrenar.
    * **Testing MSE**: generada a partir de los datos usados para testear nuestro modelo (generalmente a un conjunto de datos usaremos una parte de ellos para trainning y otra parte para usar como testing).
  * Debemos encontrar un modelo donde la Testing MSE es lo mas pequeña que se pueda.
  * Generalmente tendremos un conjunto de datos para entrenar nuestro modelo y otro conjunto para testearlo, debemos siempre que se pueda, obtener MSE con los datos de testing.
  * En caso que no haya datos de Testing por alguna razon, usaremos trainging MSE, aun que no hay garantias que un metodo con baja trainging MSE tenga baja Testing MSE. Un metodo con baja trainging MSEE puede llevar a overfittear el modelo.
  * A medida que un modelo se hace mas flexible la trainging MSE decrese, pero no necesariamente asi la test MSE, esto sucede por que el metodo trabaja muy duro para encontrar patrones en el training data, y puede elegir patrones que fueron causados por razones aleatorias, en vez de tomar la verdadera forma de $$f$$. 
  Cuando se hace un overfit del trainging data, test MSE sera muy grande ya que los supuestos encontrados en el trainging data no estan en el testing data..
  * Dado un valor $$x_{0}$$, podemos descomponer el valor esperado de la MSE en tres componentes:

    $$ E(y_{0} - \hat{f}(x_{0})^2 = Var(\hat{f}(x_{0})) + [Bias(\hat{f}(x_{0})]^2 + Var(e) $$
    
    * $$E(y_{0} - \hat{f}(x_{0})^2$$ es el valor esperado de la MSE, seria el promedio de las MSEs, si repetidamente estimamos a $$f$$ usando un gran numero de training sets y luego los evaluamos en $$x_{0}$$.
    * Esta Ecuacion nos dice que para minizar el error esperado, debemos seleccionar un metodo que simultaneamente obtenga baja *varianza*  y bajo *Bias*.
    * **Varianza** ($$Var(\hat{f}(x_{0}))$$): se refiere a la cantidad que $$\hat{f}$$ cambiara si la estimamos usando diferentes trainging data sets, utilizando differentes data sets, obtendremos diferentes $$\hat{f}$$.
    Pero idealmente la estimacion de $$f$$ no deberia variar mucho usando diferentes trainging data sets, por lo tanto si un metodo tiene alta varianza, luego pequeños cambios en el data set puede genrar grandes cambios en $$\hat{f}$$
    En General, mientras mas flexible es un metodo mas varianza tendra.
    * ** Bias** ($$Bias(\hat{f}(x_{0})$$): Hace referencia al error que es introducido al querer aproximar un error de la vida real, que puede ser extremadamente complicado, por un metodo mas simple.
    Por ejemplo si queremos usar regresion lineal para un un problema que no es lineal, vamos a tener un alto Bias, ya que no importa que trainging data set usemos, el modelo seleccionado no es el mejor.
    en general, mientras mas felxible es un metodo menos Bias tendra.

#### Medidas de Problemas de Clasificacion

  * Muchos de los conceptos usados para regression tambien sirven en los problemas de clasificacion, como el problema bias-varianza.
  * Ahora los valores de $$ Y = (y_{1},..,y_{n})), son cualitativos.
  * El enfoque mas comun usado en estos casos para cuantificar la exactitud de nuestra estimacion $$\hat{f}$$ es el **trainging error rate**:
    
    $$ \frac{1}{n}\sum_{1}^{n}I(y_{i} \neq \hat{y_{i}}) $$
    
    donde $$ \hat{y_{i}} $$, es la prediccion de la clase de etiqeta para la i-esima observacion y $$I(y_{i} \neq \hat{y_{i}})$$ indica 1 si son distintos, 0 caso contrario.
    Porlo tanto, esta ecuacion computa la fraccion de clasificaciones incorrectas, se llama *trainging error rate*, ya que se utiliza el trainging data set.
  * Por otro lado tenemos el **test error rate**, con un set de observaciones de test de la forma $$(x_{0}, y_{0})$$:
  
    $$ AveI(y_{i} \neq \hat{y_{i}}) $$
    
    Donde $$ \hat{y_{i}} $$ es la clase predecida que resulta de aplicar $$x_{0}$$ al predictor.
  * un Buen predictor es aquel que tiene un **test error rate** Bajo.
  * el **test error rate** es minimo, por un simple clasificador que asigna a cada observacion la clase mas probable, dado sus valores de prediccion (X).
    en otras palabras debemos asignar la clase J a una observacion de prueba  con vector de prediccion $$ x_{0} $$, cuando la siguiente funcion es maxima:
    
    $$ P(Y=j | X=x_{0}) $$
    
    Es una probabilidad condicional, es la prbabilidad de asginar el label J dado que tenemos el vector de preccion $$x_{0}$$. Este clasificador es llamado **Bayes Classsier**.
  
  * La prediccion  del clasificador de bayes esta determinado por el limite de decision de bayes (**bayes decision boundary**), este limite demarca en donde cae cada prediccion, si tenemos solo dos datos 
    
    $$ P(Y=1|X=x_{0}) > 0.5 $$ 
   
    tomaremos 1 si esta prediccion es mayor a 0.5, por lo tanto 0.5 es el limite de decision.
   
  * EL clasificador de bayes produce el menor test error rate, llamado **Bayes test error rate**, para $$X = x_{0}$$, el error sera:
   
    $$ 1 - E(max_{j}(P(Y=j|X=x_{0})))$$
    
    en general:
  
    $$ 1 - E(max_{j}(P(Y=j|X)))$$
    
   donde se promedia la probabilidad sobre todos los valores posibles de X.
  * El *Bayes error rate* es analogo al **error irreducible**.
  
  * En la teoria siempre vamos querer usar el clasificador bayesiano, pero para los datos reales en general no conocemos la distribucion condicional de $$Y$$ dado $$X$$, asi que computar el calsificador bayesiano es imposible.
  * Por lo tanto el clasificador bayesiano sirve como un standart para comparar otros metodos.
  * Uno de los metodos usados es KNN (K-neares neighboors) classifier, que dado un entero positivo K y una observacion de test $$x_{0}$$, este clasificador:
    1. primero identifica los K puntos que esten mas cercanos a $$x_{0}$$, representados por $$N_{0}$$
    2. luego estima la probabilidad condicional para la clase $$j$$  como una fraccion de los puntos en $$N_{0}$$ donde su valor sea igual a $$j$$:
    
    $$ P(Y = j|X = x_{0}) = \frac{1}{K}\sum_{i \epsilon  N_0}I(y_{i} = j) $$
    
    3.Luego KNN aplica la regla de bayes y elije la clase con mayor probabilidad.
  * la eleccion del K tendra un gran impacto en KNN, a medida que K crece se tiene menos flexibilidad y produce un limite de decicion cercano a una linea, esto produce un baja varianza pero alto Bias
    
 
 
