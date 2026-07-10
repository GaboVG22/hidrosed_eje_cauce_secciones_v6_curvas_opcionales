# HidroSed · Módulo Eje Cauce y Secciones v6 · Curvas opcionales

Versión corregida del módulo de eje del cauce y secciones. Mantiene el modelo probado de la aplicación `app_secciones_kmz_v13_fix_km_final_utm19s_3d`, pero deja las curvas de nivel de apoyo como entrada opcional.

## Objetivo

Generar y revisar secciones transversales del cauce sobre el tramo útil entre el PC hidrológico y el PC cuenca soporte, usando el eje del cauce como referencia obligatoria.

## Mejora principal v6

Se incorpora un modo automático recomendado. Si existen curvas de nivel de apoyo, usa el método v13 por intersección entre:

```text
línea transversal de sección ∩ curvas de nivel de apoyo
```

Luego construye el perfil station-cota de izquierda a derecha mirando aguas abajo y genera un perfil 3D con coordenadas hidráulicas:

```text
X = progresiva sobre eje
Y = offset transversal desde eje
Z = cota
```

Esto evita que las secciones se vean deformadas o aplastadas por la escala UTM.

## Inputs obligatorios

1. Eje del cauce KMZ/KML con línea.
2. PC hidrológico KMZ/KML con punto.
3. PC cuenca soporte KMZ/KML con punto.

## DEM

La app permite:

- Descargar DEM desde OpenTopography con API Key.
- Cargar DEM GeoTIFF manual.

El DEM se usa para orientar el eje, perfil longitudinal y secciones naturales. Si no se cargan curvas de apoyo, el módulo genera secciones naturales desde DEM. Si tampoco hay DEM disponible, genera secciones prismáticas por parámetros.

## Curvas de nivel de apoyo

Las curvas de nivel de apoyo son opcionales. Si se cargan, el modo v13 las usa para mejorar las secciones. Formatos aceptados:

- KMZ/KML con elevación Z o nombre con cota.
- DXF con polilíneas 3D o elevación.

## Modo de generación recomendado

Para una corrida robusta:

```text
Modo de generación de secciones: Automático recomendado
```

La lógica es:

```text
Si hay curvas de apoyo → método v13.
Si no hay curvas → DEM natural.
Si no hay DEM → sección prismática por parámetros.
```

Parámetros iniciales:

```text
Separación secciones: 50 a 100 m
Semi-ancho sección: 100 a 200 m
```

## Visualización

La aplicación incluye:

1. Vista del eje y secciones en planta.
2. Perfil longitudinal interactivo.
3. Ventana independiente de cada sección por km.
4. Editor Station-Cota.
5. Vista 3D hidráulica interactiva.

## Descargas

- KMZ eje + secciones.
- CSV perfil longitudinal.
- Excel tipo HEC-RAS.
- JSON técnico.

## Streamlit Cloud

```text
Main file path: app.py
Python version: 3.11
```

## Dependencias

La app mantiene un entorno liviano y estable:

- Sin pysheds.
- Sin geopandas.
- Sin scipy.
- Sin scikit-image.
- Sin Earth Engine.

