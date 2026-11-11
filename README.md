# Aprendizaje Automático III — Series de tiempo y pronósticos

Repositorio de los ejercicios del curso **Aprendizaje Automático III** de la Maestría en Inteligencia Artificial Aplicada de la Universidad Icesi. Contiene, sesión por sesión, el notebook con la solución del grupo a cada ejercicio de clase.

Este repositorio es la **única fuente de verdad** de los ejercicios: la versión vigente de cada uno es la que está en la rama `main`.

- **Profesor:** Diego Fernando Agudelo
- **Integrantes:** Juan Esteban Cardona, Daniel Velasco

## Contenido por sesión

| Sesión | Tema | Ejercicio | Estado |
|---|---|---|---|
| 01 | Pronóstico, componentes de una serie, promedios móviles y suavización exponencial | Pronóstico de ocupados a 6 meses con promedios móviles y suavización exponencial | En progreso |
| 02 | Estacionariedad, ruido blanco y regresión para tendencia y estacionalidad | Pronóstico de ocupados a 6 meses con regresión lineal (tendencia y estacionalidad) | En progreso |

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
└── sesion-02-regresion-tendencia-estacionalidad/
    └── ejercicio2_pronostico_ocupados.ipynb
```

Cada sesión nueva agrega una carpeta `sesion-NN-tema-corto/` con el notebook de su ejercicio.

## Reglas del repositorio

1. **Un solo archivo por ejercicio.** No se crean copias como `ejercicio_v2_final.ipynb`: el historial de versiones lo lleva Git.
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
