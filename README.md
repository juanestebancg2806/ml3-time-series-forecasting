# Aprendizaje Automático III — Series de tiempo y pronósticos

Repositorio de los ejercicios del curso **Aprendizaje Automático III** de la Maestría en Inteligencia Artificial Aplicada de la Universidad Icesi. Contiene, sesión por sesión, el notebook con la solución del grupo a cada ejercicio de clase, y los talleres que se entregan, que combinan los ejercicios de dos sesiones en un solo notebook.

Este repositorio es la **única fuente de verdad** de los ejercicios: la versión vigente de cada uno es la que está en la rama `main`.

- **Profesor:** Diego Fernando Agudelo
- **Integrantes:** Juan Esteban Cardona, Daniel Velasco

## Talleres (entregables)

Cada taller reúne en un solo notebook los ejercicios de dos sesiones, con un mismo protocolo de evaluación para todos los modelos, porque así lo pidió el profesor. Es la versión que se entrega y la que sustenta el video de presentación.

| Taller | Sesiones | Notebook | Estado |
|---|---|---|---|
| 1 | 01 y 02 | [`taller1/taller1_pronostico_ocupados.ipynb`](taller1/taller1_pronostico_ocupados.ipynb) · [Abrir en Colab](https://colab.research.google.com/github/juanestebancg2806/ml3-time-series-forecasting/blob/main/taller1/taller1_pronostico_ocupados.ipynb) | Terminado |

### Taller 1: pronóstico de ocupados en las 13 principales ciudades

Pronóstico del número mensual de ocupados (miles de personas) de las 13 principales ciudades de Colombia para julio a diciembre de 2019, con datos de enero de 2001 a junio de 2019. El notebook mezcla los dos ejercicios en tres partes:

- **Preparación común:** exploración de la serie, descomposición, partición de entrenamiento y prueba, y esquema de evaluación compartido: validación con origen móvil de 6 cortes de 6 meses (2016-2018), RMSE como métrica principal, MAPE como complemento, el naive estacional como referencia y una prueba reservada de enero a junio de 2019.
- **Parte I (ejercicio de la sesión 01):** promedios móviles con distintas ventanas y suavización exponencial (SES, Holt y Holt-Winters, aditivo y multiplicativo).
- **Parte II (ejercicio de la sesión 02):** regresión lineal con tendencia polinómica y estacionalidad (dummies, términos de Fourier y escala logarítmica), estimada con toda la historia o con ventanas móviles, y la evaluación de los supuestos de los residuales sobre los candidatos, en orden de desempeño.
- **Parte III:** comparación final, evaluación en la prueba y pronóstico de los 6 meses siguientes.

**Resultado:** el modelo final es el promedio simple del Holt-Winters aditivo sin tendencia y la regresión con tendencia lineal y dummies de mes estimada con los últimos 24 meses. En la validación tiene un RMSE de 116.47 mil personas (MAPE 0.92 %) y en la prueba, de 62.72 mil (MAPE 0.52 %). Pronostica entre 10,855 y 10,964 mil ocupados al mes, con el máximo en octubre, e intervalos de predicción empíricos, porque los errores de la regresión no cumplen los supuestos de independencia y varianza constante.

## Ejercicios por sesión

Los notebooks de cada sesión son la solución individual de cada ejercicio, desarrollada antes de unirlos en el taller. Se conservan como referencia; la versión que se entrega es la del taller.

| Sesión | Tema | Ejercicio | Notebook |
|---|---|---|---|
| 01 | Pronóstico, componentes de una serie, promedios móviles y suavización exponencial | Pronóstico de ocupados a 6 meses con promedios móviles y suavización exponencial | [`ejercicio1_pronostico_ocupados.ipynb`](sesion-01-promedios-moviles-suavizacion/ejercicio1_pronostico_ocupados.ipynb) |
| 02 | Estacionariedad, ruido blanco y regresión para tendencia y estacionalidad | Pronóstico de ocupados a 6 meses con regresión lineal (tendencia y estacionalidad) | [`ejercicio2_pronostico_ocupados_regresion.ipynb`](sesion-02-regresion-tendencia-estacionalidad/ejercicio2_pronostico_ocupados_regresion.ipynb) |

## Estructura

```
ml3-time-series-forecasting/
├── README.md
├── pyproject.toml          # dependencias del proyecto
├── uv.lock                 # versiones exactas, generadas por uv
├── .python-version         # versión de Python (3.13)
├── .gitignore
├── sesion-01-promedios-moviles-suavizacion/
│   └── ejercicio1_pronostico_ocupados.ipynb
├── sesion-02-regresion-tendencia-estacionalidad/
│   └── ejercicio2_pronostico_ocupados_regresion.ipynb
└── taller1/
    └── taller1_pronostico_ocupados.ipynb      # sesiones 01 y 02, versión entregada
```

Cada sesión nueva agrega una carpeta `sesion-NN-tema-corto/` con el notebook de su ejercicio, y cada taller, una carpeta `tallerN/` con el notebook que combina los ejercicios de sus sesiones.

## Reglas del repositorio

1. **Un solo archivo por ejercicio y por taller.** No se crean copias como `ejercicio_v2_final.ipynb`: el historial de versiones lo lleva Git. El notebook del taller no es una copia de los ejercicios: los integra en un solo análisis con un protocolo de evaluación común.
2. **Los notebooks se suben ejecutados**, con sus salidas, porque los resultados y gráficas hacen parte de la entrega. Antes de cada commit se reinicia el kernel y se ejecuta todo en orden, para que las salidas sean reproducibles.

## Flujo de trabajo

- `main` contiene siempre la versión vigente y funcional.
- Cada ejercicio se desarrolla en una rama propia (por ejemplo, `sesion-02-ejercicio`) y se integra a `main` con un *pull request* revisado por el otro integrante.
- Mensajes de commit cortos y en presente, indicando la sesión: `sesion-02: agrega diagnóstico de residuos del mejor modelo`.

## Datos

Los notebooks descargan los datos directamente del repositorio público del curso, por lo que se necesita conexión a internet para ejecutarlos.

## Entorno

El entorno se maneja con [uv](https://docs.astral.sh/uv/). Un solo entorno virtual, `.venv/` en la raíz del repositorio, ejecuta todos los ejercicios.

- `pyproject.toml` declara las dependencias.
- `uv.lock` fija las versiones exactas, para que ambos integrantes obtengan los mismos resultados.
- `.python-version` fija Python 3.13; uv lo descarga si no está instalado.
- `.venv/` no se sube al repositorio: cada integrante lo crea localmente.

### Primera vez

```bash
# 1. Instalar uv (una sola vez por equipo)
curl -LsSf https://astral.sh/uv/install.sh | sh     # macOS y Linux
# en Windows: powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# 2. Crear .venv/ con las versiones exactas de uv.lock
uv sync
```

Luego, en VS Code o Jupyter, se selecciona como kernel el intérprete de `.venv/`.

### Agregar o actualizar una librería

```bash
uv add nombre-libreria        # agrega la dependencia y actualiza uv.lock
uv sync                       # en el otro computador, después de hacer pull
```

Siempre se suben juntos `pyproject.toml` y `uv.lock`. No se instalan librerías con `pip install` dentro de `.venv/`, porque esos cambios no quedan registrados.

Librerías principales: `pandas`, `numpy`, `matplotlib`, `statsmodels`, `scikit-learn`, `scipy` y `openpyxl` (para leer los archivos de Excel). `ipykernel` va como dependencia de desarrollo para ejecutar los notebooks.

## Referencias

- Alonso, J. C. — libro guía del curso (los ejemplos del libro están en R).
- Hyndman, R. J. y Athanasopoulos, G. *Forecasting: Principles and Practice* (3.ª ed.). https://otexts.com/fpp3/
- Documentación de [statsmodels](https://www.statsmodels.org/) y [scikit-learn](https://scikit-learn.org/).
