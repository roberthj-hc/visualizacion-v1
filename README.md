# Ruta 14 · Residuos sólidos — Proyecto integrador de Visualización de datos

Entrega 1 (semana 1): acta de alcance, fuente de datos y ficha inicial de calidad.

## Estructura

```
01_datos/
  bruto/        archivos tal como se descargaron (no se editan)
  procesado/    dsny_tonelaje_procesado_v0.csv / .parquet (generados por el notebook)
02_etl/
  01_extraccion_perfilamiento.ipynb   extracción, perfilamiento y preparación v0
  salidas/      tablas de control (perfil, nulos, sumas de control, hashes)
03_visualizaciones/
  entrega1/     figuras borrador usadas en la entrega 1
05_informe/
  Entrega1_Ruta14_ResiduosSolidos.docx
requirements.txt        dependencias mínimas
requirements-lock.txt   versiones exactas del entorno local
```

## Fuentes (NYC Open Data, descargadas el 30/10/2026)

| Archivo | Conjunto | Enlace |
|---|---|---|
| `dsny_monthly_tonnage_raw.csv` | DSNY Monthly Tonnage Data (ebb7-mvp5) | https://data.cityofnewyork.us/d/ebb7-mvp5 |
| `DSNY_Monthly_Tonnage_Data_Dictionary.xlsx` | Diccionario oficial (versión 2026-04-16) | adjunto del mismo conjunto |
| `nyc_community_districts.geojson` | Community Districts, DCP (5crt-au7u) | https://data.cityofnewyork.us/d/5crt-au7u |
| `nyc_population_by_cd.csv` | New York City Population By Community Districts, DCP (xi7c-iiu2) | https://data.cityofnewyork.us/d/xi7c-iiu2 |

Las huellas SHA-256 de cada archivo quedan en `02_etl/salidas/registro_extraccion.csv`.

## Cómo reproducir

### Local (Windows)

```bash
py -m venv .venv
.venv\Scripts\python -m pip install -r requirements.txt
.venv\Scripts\python -m ipykernel install --user --name python3
# abrir el notebook en VS Code/Jupyter y ejecutar "Run all", o bien:
cd 02_etl
..\.venv\Scripts\python -c "import nbformat; from nbclient import NotebookClient; nb=nbformat.read('01_extraccion_perfilamiento.ipynb',4); NotebookClient(nb,timeout=600).execute(); nbformat.write(nb,'01_extraccion_perfilamiento.ipynb')"
```

### Google Colab

Subir el notebook, descomentar la línea `!pip install ...` de la primera celda y ejecutar "Run all".
Si los archivos brutos no están, el notebook los descarga desde las URL oficiales.
