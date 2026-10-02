# Taller: demanda de pasajeros en estaciones de TransMilenio

Predicción de las validaciones (entradas) por estación y franja de 15 minutos en las
estaciones Alcalá, Modelia y Terreros, de junio a agosto de 2026.

## Estructura

```
taller-transmilenio/
├── data/
│   ├── raw/          Excel mensuales de validaciones y, opcional, gtfs.zip (no se suben a git)
│   └── processed/    Tablas que genera el notebook (sí se suben)
├── notebooks/
│   └── taller_transmilenio.ipynb
├── reports/
│   ├── figuras/      Gráficas que genera el notebook
│   ├── informe_tecnico.md
│   └── informe_gerencial.md
├── requirements.txt
└── README.md
```

## Cómo obtener los datos

1. Validaciones: https://storage.googleapis.com/validaciones_tmsa/validaciones_mensuales.html
   En "Validación Troncal", año 2026, descargar junio, julio y agosto.
   Guardar los tres `.xlsx` en `data/raw/` sin abrirlos ni modificarlos en Excel.
2. Opcional, oferta programada: descargar un GTFS del periodo desde
   https://storage.googleapis.com/gtfs-estaticos/ y guardarlo como `data/raw/gtfs.zip`.

Anotar aquí la fecha de descarga de cada archivo: _completar_.

## Cómo correr

```
pip install -r requirements.txt
jupyter notebook notebooks/taller_transmilenio.ipynb
```

Ejecutar todas las celdas en orden. La primera vez lee los Excel (cerca de un minuto por archivo)
y guarda `data/processed/validaciones_modelo.csv`; las siguientes veces lee ese archivo.
Para volver a leer los Excel, poner `RECARGAR = True` en el bloque 0.

## Trabajo en equipo con git

- Cada integrante trabaja en su rama y en un bloque distinto del notebook.
- Antes de cada commit: Kernel > Restart & Clear Output. Los resultados guardados en las celdas
  son la causa principal de conflictos al unir ramas.
- Para la entrega final: una persona ejecuta todo de principio a fin y sube el notebook con resultados.
