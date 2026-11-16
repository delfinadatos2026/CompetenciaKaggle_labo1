# CompetenciaKaggle_labo1

Este repo tiene como objetivo replicar mis corridas en la competencia de Kaggle de la materia Laboratorio de Implementación I como Analista Jr.

El objetivo de la competencia es que el modelo prediga los clientes de un banco que se darán de baja en dos meses. Los famosos "BAJA+2". Al conocerlos se maximiza nuestra función de Ganancia.

Para iniciar mis corridas utilicé el workflow suministrado por la cátedra a los Senior, y modifiqué los bloques de código del dataset y la competencia de Kaggle. Lo adapté para usar el dataset junior y participar de la competencia de Kaggle junior ya que quería integrar en mi modelo la optimización bayesiana y el semillerío. Este último le da más estabilidad al tablero público de Kaggle. Durante todas mis corridas usé la siguiente semilla primigenia: `200017`, y un semillerío de `30`. También a recomendación de mi propio experimento utilicé `5` hiperparámetros en la optimización bayesiana durante todas las corridas.

Las modificaciones y decisiones que tomé se basaron:
- Algunos de los videos de experimentos colaborativos de mis compañeros (no alcancé a probar todos)
- Los resultados que iba obteniendo en el tablero público de Kaggle
- Mi propio criterio construido en dos meses de cursada de la materia (la inteligencia artificial no participó en la toma de decisiones).

¿Con qué empiezo? Para responderme esta pregunta saqué conclusiones de cada video y comencé a probar.

# Modelo seleccionado para la predicción final (Comparativo con z719)

| Etapa / Parámetro | z719 - senior modificado para junior | Comparativo a: Cuarta Corrida |
| :--- | :--- | :--- |
| **Preprocesamiento_Dataset** | | |
| **Catastrophe_Analysis** | MICE[cite: 1] | MICE[cite: 1] |
| **Data_Drifting** | deflación[cite: 1] | deflación[cite: 1] |
| **FE_Intra_manual** | | Sin modificaciones[cite: 1] |
| **FE_Historico** | Lags y deltas de orden 1 y 2[cite: 1] | - Lags y deltas de orden 1 y 2 con N/A los meses de pandemia ampliada, 03/2020-10/2020 (Problema #5)<br>- Tendencias históricas (Problema #4)[cite: 1] |
| **FE_Variables_Random_Forest** | | Sin modificaciones[cite: 1] |
| **FE_Canaritos** | - ratio: 0,2<br>- desvío: 2[cite: 1] | - ratio: 0,2<br>- desvío: 2[cite: 1] |
| **Modelado** | | |
| **Training_Strategy** | - testing: (NO HAY)<br>- validation: 202107<br>- training: 201901 - 202105 (se considera el 20% de los continua)[cite: 1] | - testing: (NO HAY)<br>- validation: 202107<br>- training: 201901 a 202105 SIN MESES DE PANDEMIA AMPLIADA #Problema 5 (se considera el 100% de los continua ya que era lo recomendado para los Junior)[cite: 1] |
| **Hyperparameter Tuning** | | |
| **PARAM$hyperparametertuning$num_iterations** | 100[cite: 1] | 500[cite: 1] |
| **PARAM$hyperparametertuning$hs <- makeParamSet(** | | Aumenté las iteraciones a 500 a consecuencia de que amplié rangos de: -num_iterations, -num_leaves, y -learning_rate[cite: 1] |
| **num_iteration** | (2 a 10) = 4 a 1024 (enteros)[cite: 1] | (3 a 10,5)[cite: 1] |
| **num_leaves** | (2 a 11) = 4 a 2048 (enteros)[cite: 1] | (2 a 11.5) = 4 a 2896 (enteros)[cite: 1] |
| **learning_rate** | (-7 a -0.1) = (0,0078125 a 0,933033)[cite: 1] | (-9 a -1) = (0.001953 a 0.5)[cite: 1] |
| **feature_fraction** | (0.05 a 0.90)[cite: 1] | (0.05 a 0.90)[cite: 1] |
| **min_sum_hessian_in_leaf** | (-10 a 10) = 0,0009765625 a 1024[cite: 1] | (-10 a 10) = 0,0009765625 a 1024[cite: 1] |
| **Producción** | | |
| **Final_Training** | de 201901 a 202107[cite: 1] | de 201901 a 202107 SIN MESES DE PANDEMIA AMPLIADA #Problema 5[cite: 1] |
| **Training - Semillerío** | 10[cite: 1] | 30[cite: 1] |
| **Scoring** | 202109[cite: 1] | 202109[cite: 1] |
| **Semilla** | 102191[cite: 1] | 200017[cite: 1] |
| **Nro. experimento** | 9100/9500[cite: 1] | 9104[cite: 1] |
| **Kaggle - Cortes** | 1800-2400[cite: 1] | 1400-2400[cite: 1] |

---

> ### Resultados Kaggle y Entrega Final (`Cuarta Corrida` - Exp. `9104`)
>
> * **Nombre script:** `Cuarta_corrida_final_senior_junior4,5y12`[cite: 1]
> * **Tiempo de corrida:** *(sin completar)*[cite: 1]
> * **Mejor Ganancia de Kaggle - Público:** `99.605`[cite: 1]
> * **Corte con mejor Ganancia - Público:** `1700`[cite: 1]
> * **Mejor Ganancia de Kaggle - Privado:** `91.193`[cite: 1]
> * **Corte con mejor Ganancia - Privado:** `1400`[cite: 1]
>
> **Mejores HP:**[cite: 1]
> * `num_iteration`: `9.0862056`[cite: 1]
> * `num_leaves`: `11.0593401`[cite: 1]
> * `learning_rate`: `-7.0547474`[cite: 1]
> * `feature_fraction`: `0.2451082`[cite: 1]
> * `min_sum_hessian_in_leaf`: `2.8795635`[cite: 1]
>
> ### Definición entrega final
> Para la decisión final consideré el experimento que arrojaba ganancias más estables y el corte que mayor ganancia tuvo en el público. Con el diario del lunes estas decisiones son fuertemente cuestionadas por mí misma y la búsqueda de alguna metodología con mayor criterio y resultado está siendo investigada.[cite: 1]
