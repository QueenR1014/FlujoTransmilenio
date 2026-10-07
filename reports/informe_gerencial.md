<h1 align="center">Informe Gerencial</h1>
<h3 align="center">Predicción de la demanda de entradas a TransMilenio por estación y franja horaria</h3>

<div align="center">
    <p><strong>Autores:</strong> Gabriela Aldana, Santiago Jorigua, Juan Reina</p>
</div>

---

## 1. El problema y la recomendación

**El problema.** TransMilenio registra cada entrada de pasajeros (validación) en cada estación, en franjas de 15 minutos. Para planear la operación es necesario saber de antemano cuánta gente va a llegar a cada estación y a qué hora. Este proyecto construye un modelo que anticipa esa demanda.

**Alcance.** Se usaron los datos abiertos de TransMilenio de agosto de 2026:

| Dato | Valor |
|---|---:|
| Estaciones analizadas | 123 |
| Troncales | 14 |
| Validaciones en el mes | 31.016.651 |
| Registros (estación × franja × día) | 294.004 |

Los resultados detallados se muestran para tres estaciones, una por troncal (Troncal B Norte, K Calle 26 y G NQS Sur): **Mazurén, Modelia y Terreros**. Se excluyeron las estaciones de fase "Dual" (como Alcalá y los portales).

**La recomendación.**

> **Adoptar el modelo Ridge como herramienta de planeación de la demanda en días normales.** Reduce el error de pronóstico en un 63 % frente a usar el promedio histórico y explica el 87 % de la variación de las entradas.

El modelo es sencillo: aprende el perfil típico de cada estación en cada franja horaria y lo ajusta según el tipo de día (hábil o de descanso). Es rápido de calcular y fácil de explicar. **No sirve para anticipar días atípicos** (marchas, cierres, lluvia, eventos) y todavía no se ha probado en un festivo.

---

## 2. Qué tan bien predice el modelo (en pasajeros)

Cada predicción corresponde a las entradas de una estación en una franja de 15 minutos. El modelo se evaluó con los últimos seis días de agosto (26 al 31), que no se usaron para entrenarlo.

| | Error promedio por franja de 15 min | Variación de la demanda explicada |
|---|---:|---:|
| Usar el promedio histórico | 105 pasajeros | 0 % |
| **Modelo recomendado** | **39 pasajeros** | **87 %** |

El error es **63 % menor** que el de la referencia. El rango razonable del error es de 34 a 47 pasajeros por franja.

**Por estación**

| Estación | Error promedio (pasajeros por franja) | Error como % de su demanda promedio |
|---|---:|---:|
| Modelia | 16,9 | 24 % |
| Mazurén | 31,2 | 25 % |
| Terreros | 106,8 | 36 % |

Terreros es la estación con mayor error en términos absolutos: es la más grande y su demanda se concentra en la mañana. En términos relativos, el modelo se equivoca entre una cuarta parte y un tercio de la demanda promedio de cada estación.

**Cómo se ve en la práctica.** Los puntos son las entradas reales y la línea es la predicción. En el lunes de prueba (31 de agosto), que el modelo nunca vio, la curva predicha sigue de cerca la forma real del día.

<div align="center">
    <img src="./figuras/test_vs_train.png" alt="Predicción vs. datos reales en un día hábil">
</div>

**Dónde falla más.** En los sábados el ajuste es menos parejo: el modelo aprendió sobre todo de días hábiles y tiende a repetir ese comportamiento.

<div align="center">
    <img src="./figuras/test_vs_train2.png" alt="Predicción vs. datos reales en un sábado">
</div>

**Confianza en el resultado.** No hay señales de sobreajuste: el error en los datos de prueba no es mayor que el estimado durante el entrenamiento, y en cada estación el error en ambos conjuntos es casi igual. Modelos más complejos (Lasso y Kernel) tuvieron un desempeño mucho peor, y las alternativas equivalentes (OLS y Splines) no ofrecen ventaja real.

---

## 3. Dónde y a qué hora se concentra la demanda

**La demanda está muy concentrada.** La mitad de los registros tiene 46 entradas o menos por franja, pero el 10 % más alto supera las 240 y los picos llegan a casi 4.700. Pocas estaciones y pocas franjas concentran gran parte del movimiento.

**El tipo de día es el factor principal.** Los días hábiles tienen claramente más entradas que sábados, domingos y festivos.

<div align="center">
    <img src="./figuras/eda_serie_diaria.png" alt="Validaciones diarias durante agosto">
</div>

**Dos picos en días hábiles.** Durante la semana la demanda sube en dos momentos del día (mañana y tarde). En fines de semana y festivos la demanda es baja y casi constante a lo largo del día.

<div align="center">
    <img src="./figuras/eda_perfil_horario.png" alt="Perfil horario de la demanda por tipo de día">
</div>

**Cada estación tiene su propia personalidad.** Las tres estaciones de estudio muestran patrones distintos:

- **Terreros:** un solo gran pico, en la mañana.
- **Mazurén:** dos picos, con la mañana mayor que la tarde.
- **Modelia:** dos picos, con la tarde mayor que la mañana.

<div align="center">
    <img src="./figuras/eda_estaciones_estudio.png" alt="Perfil horario de Terreros, Mazurén y Modelia">
</div>

Por eso un pronóstico único para todo el sistema no funciona. Al dejar que cada estación tenga su propia curva por hora y por tipo de día, el error baja de forma drástica: el modelo sin esas diferencias solo explica un 34 % de la variación, frente al 84 % del modelo recomendado en validación.

**Estación, hora y tipo de día explican casi todo.** La combinación de estas tres variables da cuenta de la mayor parte del movimiento de las entradas.

<div align="center">
    <img src="./figuras/eda_variacion_explicada.png" alt="Variación explicada por estación, franja y tipo de día">
</div>

**Sábados.** Es el día con más registros atípicos, probablemente por actividades propias del fin de semana, y es donde el modelo es menos preciso.

---

## 4. Valor de la solución

**Qué permite hacer hoy**

- **Planear un día normal con anticipación:** saber cuántos pasajeros esperar en cada estación y franja para ajustar la oferta de buses y el personal en las horas pico.
- **Identificar dónde concentrar recursos:** el modelo ya distingue las estaciones y horarios de mayor presión, como la mañana en Terreros o la tarde en Modelia.
- **Contar con una línea base clara:** cualquier mejora futura se puede medir frente a un error de 39 pasajeros por franja.

**Por qué es una buena base**

- **Sencillo y explicable:** es el perfil promedio de cada estación por franja, corregido por tipo de día. Es fácil de auditar y de comunicar.
- **Bajo costo de operación:** no requiere infraestructura especial para calcularse.
- **Resultados estables:** no hay sobreajuste, y los modelos alternativos no logran mejorarlo.

**Límites que conviene tener presentes**

| Límite | Implicación |
|---|---|
| Se usó un solo mes de datos y solo seis días de prueba | La precisión real puede variar; los intervalos de error son amplios |
| No se ha probado en un festivo entre semana | No se debe confiar en él para esos días todavía |
| No considera eventos, marchas, cierres ni lluvia | Sirve para días normales, no para anticipar situaciones atípicas |
| No incluye estaciones de fase "Dual" (Alcalá, portales) | Cobertura parcial del sistema |
| El error crece con el tamaño de la estación | Las estaciones grandes, como Terreros, tienen mayor incertidumbre |

**Próximos pasos recomendados**

1. **Ampliar los datos a varios meses** para capturar estacionalidad y probar el modelo en festivos.
2. **Incorporar eventos y clima** para poder anticipar días atípicos.
3. **Mejorar la precisión en estaciones grandes y en sábados**, por ejemplo modelando el logaritmo de las validaciones.
4. **Extender la cobertura** a las estaciones de fase "Dual" y al resto del sistema.
