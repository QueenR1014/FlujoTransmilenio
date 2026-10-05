<h1 align="center">Informe Técnico</h1>

<div align="center">
    <p>
    <p><strong>Autores:</strong> Gabriela Aldana, Santiago Jorigua, Juan Reina
    </p>
</div>

## 1. Descripción del dataset y del problema

En la página web `[Datos abierto](https://datosabiertos-transmilenio.hub.arcgis.com/)`  encontramos los Datos Abiertos de TRANSMILENIO S. A. . En este portal de acceso podemos encontrar distintos datos sobre el sistema masivo de tránsito de la ciudad, desde sus servicios troncales (BRT "Transmilenio") y  zonales (comúnmente llamado buses SITP). En este proyecto queremos predecir las **validaciones** (entradas) al sistema troncal de Transmilenio para tres estaciones:
- Álcala (Troncal B Norte)
- Modelia (Troncal K Calle 26)
- Terreros (Troncal G NQS Sur)

La fuente de Datos Abiertos TRANSMILENIO S.A. nos provee de las validaciones
mensuales para el año 2026 de todo el sistema troncal. Para efectos de este ejercicio solo usaremos los datos para los meses de junio, julio y agosto del año mencionado. En cada archivo encontramos el DataSet para el respectivo mes con las siguientes variables:

| Variable | Descripción | Tipo|
| --- | --- | --- |
|codigo | Identificador único para cada estación. | Numérica Discreta|
|linea | Troncal a la que pertenece la estación. | Texto |
| franja_min |  Ventana de tiempo de 15 minutos en las que se presentaron las validaciones. | Numérica Discreta|
| validaciones |Cantidad de validaciones (entradas) realizadas a la estación | Numérica Discreta |
|acceso  | Acceso de la estación. (Acceso o talanquera por la que se contaron las validaciones) |  Categórica |
| nombre | Nombre de la estación | Texto |

## 2. Exploración y decisiones de limpieza
## 3. Matriz de aplicabilidad
## 4. Métodos aplicados: planteamiento, hiperparámetros (rango probado, valor elegido, por qué) y evaluación
## 5. Comparación de los finalistas
## 6. Decisión final
## 7. Limitaciones y posibles mejoras
