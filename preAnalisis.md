# Mineria de datos a datos bancarios
## Plan Propuesto

* Se busca el poder otorgar la mayor cantidad de créditos
* Cada crédito tiene un riesgo, por lo que se estimará dicho porcentaje de riesgo y con base al mismo se cobrará un interés.
* Se creará un sistema de preaprobación de créditos, esto para poder generar publicidad dirigida 
* Adicionalmente a la preaprobación se calculará una línea de crédito preaprobada.

### Fases de analisis
1) estimación de reglas de preaprobación, se bucara tener aprobado y no aprobado
2) Creación de modelo predictivo de variable de riesgo que sera un valor de 0-1
3) Calculo de linea de crédito preaprobada que sera un valor en moneda o unidades de crédito

## Reporte estadisticas de de información transformada

### transformaciones comunes
Se eliminan las columnas que no aportan información

* NUM_SOLICITUD
* CUENTA_ASIGNADA
* NUM_CREDITOS
* PEOR_HISTORIA_CREDITO

Se transforman datos que son interpretados como texto a valores numericos

* CAPACIDAD_TC (texto) -> CAPACIDAD_TC_NUM (numerico)
* CAPACIDAD_PAGO_TOTAL (texto) -> CAPACIDAD_PAGO_TOTAL_NUM (numerico)

Adicionalmente se interpretan los datos inexistente de estas 2 columnas a 'NaN', se visualiza '?'

* En CAPACIDAD_TC_NUM los valores 'NaN' representan el 69%

### transformaciones para fase de reglas de preaprobación

Se seleccionan las siguientes columnas las cuales corresponden a los datos que puede tener cualquier cliente que va a solicitar credito, tenga historial previo o no

* ESCOLARIDAD
* TIPO_VIVIENDA
* COMPROBANTES_INGRESOS
* EDAD
* SOLICITUDES_RECHAZADAS
* INGRESO_INFERIDO
* CLIENTE_CDE
* SEGMENTO_CLIENTE

La variable objetivo sera

* APROBACION_TC

* En APROBACION_TC se fusionan los valores pre-aprobado y aprobado

## Interpretación algoritmos usados

### Algoritmos usados en fase de reglas de preaprobación
Para esta fase se usaron los siguientes algoritmos
* Arbol
* Inducción de reglas CN2
* Mosaico
* Red neuronal
* kNN
#### Mosaico
En ese algoritmo se encontro el siguiente mosaico:
![Mosaico Punto descision](image/captura_1.png)

La iterpretacion del mismo es que el punto de descicion que concentra la mayoria de las solicitudes rechazadas es el PS1

![Mosaico segmento cliente](image/captura_2.png)

En este otro mosaico se puede ver la relación entre el segmento de cliente y la aprobación o rechazo de las solicitudes. Se puede ver que Aquellos clientes 
que no pertenecen a un segmento de cliente son mas rechazados, adicionalmente los segmentos Alto A-B-C y Medio A-B son los que tienen aprobación mas alta

![Mosaico solicitudes rechazadas](image/captura_3.png)

En este mosaico se ve la relación directa entre el numero de solicitudes rechazadas vs la aprobación, en este caso si hay al menos una solicitud es probable que sea rechazado el crédito.

#### Arbol
En este otro algoritmo se buscara ver algunas reglas que se pueden generar.

![Arbol_1](image/captura_4.png)

En este arbol se puede confirmar lo visto en el algoritmos del mosaico, Si hay mas de 0 solicitudes rechazadas la solicitud se rechazara, asi como lo de los segmentos de clientes que suelen ser aprobados.
Adicionalmente a lo anterior se pueden ver caracteristicas adicionales que deben ser tomadas en cuenta para la aprobación, dentro del segmento medio D o sin segmento estos tienen una probabilidad mayor de aprobación si el ingreso inferido es mayor a 7232, dentro de este se pueden ver las reglas particulares de los puntos de decision: En el caso de CN0 se toma en cuenta el tipo de vivienda, si es renta es menos probable ser aprobado a si es de los otros tipos, en el caso de PS1 importa mas el ingreso inferido el cual debe ser mayor.

#### CN2

Para complementar las reglas vistas en el algoritmo de arbol se usara el CN2 lo cual dio el siguiente resultado:

![CN2_1](image/captura_5.png)

Aqui se confirman las reglas vistas anteriormente sobre la influencia del segmento del ciente, el numero de solicitudes rechazadas y el punto de decision.

#### Red neuronal y Knn

Para estos algoritmos se hara uso de la prueba y comparación para poder saber cual es el mas conveniente.

![test_1](image/captura_6.png)

Se puede observar en la estimación usando los datos el algoritmo que tiene una precision mas alta es el del arbol seguido de la red neuronal.

![test_2](image/captura_7.png)

Haciendo una validación cruzada el mas preciso es el CN2, seguido de la red neuronal por lo que se pueden tomar en cuenta todas las reglas de CN2 para hacer estimaciones y usar la red neuronal para predecir de manera automatica la aprobación o rechazo de cada solicitud.


