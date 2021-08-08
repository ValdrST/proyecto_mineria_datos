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
Para esta fase se 
#### 


