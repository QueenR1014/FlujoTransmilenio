<h1 align="center">Informe Técnico</h1>

<div align="center">
    <p>
    <p><strong>Autores:</strong> Gabriela Aldana, Santiago Jorigua, Juan Reina
    </p>
</div>

## 1. Descripción del dataset y del problema

En la página web `[Datos abierto](https://datosabiertos-transmilenio.hub.arcgis.com/)`  encontramos los Datos Abiertos de TRANSMILENIO S. A. . En este portal de acceso podemos encontrar distintos datos sobre el sistema masivo de transporte de la ciudad, desde sus servicios troncales (BRT "Transmilenio") y  zonales (comúnmente llamado buses SITP). En este proyecto queremos predecir las **validaciones** (entradas) al sistema  Transmilenio para tres troncales:
- Troncal B Norte
- Troncal K Calle 26
- Troncal G NQS Sur
*Estas troncales fueron elegidas de manera arbitraria.*

La fuente de Datos Abiertos TRANSMILENIO S.A. nos provee de las validaciones
mensuales para el año 2026 de todo el sistema troncal. Para efectos de este ejercicio solo usaremos los datos para el mes de agosto del año mencionado. En el archivo encontramos el DataSet para el respectivo mes con las siguientes variables:

| Variable | Descripción | Tipo|
| --- | --- | --- |
|Fase | Fase a la que pertenece el servicio. (Antigüedad de la troncal) | Categórica|
|Línea | Troncal a la que pertenece la estación. | Texto |
| Estación |  Código y Nombre de la estación | Texto |
| Acceso de Estación |Acceso o talanqueras por la que se contaron las validaciones de la estación. | Numérica Discreta |
|Intervalo  | Intervalo de 15 minutos en los que se cuentan las cantidades de validaciones realizadas por cada acceso. |  Numérica Discreta |
| Fechas | Las últimas 31 columnas representan cada uno de los días del mes. El valor que alojan en esta variable son las cantidades de validaciones que se realizaron en el día respectivo. | Numérica Discreta |

<div align="center">
    <p>Datos en bruto</p>
    <img src="./images/raw_data.png" alt="Datos en Bruto">
</div>

## 2. Exploración y decisiones de limpieza
## 3. Matriz de aplicabilidad
## 4. Métodos aplicados: planteamiento, hiperparámetros (rango probado, valor elegido, por qué) y evaluación
## 5. Comparación de los finalistas
## 6. Decisión final
## 7. Limitaciones y posibles mejoras
