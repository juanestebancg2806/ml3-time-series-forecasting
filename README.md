# Aprendizaje Automático III — Series de tiempo y pronósticos

Repositorio del curso **Aprendizaje Automático III** de la Maestría en Inteligencia Artificial Aplicada de la Universidad Icesi. Reúne, sesión por sesión, los notebooks del profesor, los ejercicios desarrollados por el grupo y los apuntes de estudio.

Este repositorio es la **única fuente de verdad** del curso: la versión vigente de cada ejercicio es la que está en la rama `main`.

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
├── requirements.txt
├── .gitignore
├── sesion-01-promedios-moviles-suavizacion/
│   ├── profesor/      # notebooks originales del profesor, sin modificar
│   ├── ejercicio/     # solución del grupo
│   └── apuntes/       # resúmenes de estudio (PDF)
├── sesion-02-regresion-tendencia-estacionalidad/
│   ├── profesor/
│   ├── ejercicio/
│   └── apuntes/
└── datos/             # copia local de los datos usados en los ejercicios
```

Cada sesión nueva sigue la misma estructura: `sesion-NN-tema-corto/` con sus carpetas `profesor/`, `ejercicio/` y `apuntes/`.

## Reglas del repositorio

1. **Los notebooks del profesor no se editan.** Se suben tal como se recibieron en `profesor/`, como referencia. Las notas, correcciones o pruebas sobre ellos se hacen en una copia dentro de `ejercicio/`.
2. **Un solo archivo por entregable.** No se crean copias como `ejercicio_v2_final.ipynb`: el historial de versiones lo lleva Git.
3. **Los notebooks de `ejercicio/` se suben ejecutados**, con sus salidas, porque los resultados y gráficas hacen parte de la entrega. Antes de cada commit se reinicia el kernel y se ejecuta todo en orden, para que las salidas sean reproducibles.
4. **Los datos se descargan de la fuente del curso** (el repositorio público del profesor) y se guarda una copia en `datos/`, para que los ejercicios sigan funcionando si la fuente cambia.
5. **Cada entrega se marca con una etiqueta** (`git tag sesion-01-entrega`), para poder recuperar exactamente la versión que se envió.

## Flujo de trabajo

- `main` contiene siempre la versión vigente y funcional.
- Cada ejercicio se desarrolla en una rama propia (por ejemplo, `sesion-02-ejercicio`) y se integra a `main` con un *pull request* revisado por el otro integrante.
- Mensajes de commit cortos y en presente, indicando la sesión: `sesion-02: agrega diagnóstico de residuos del mejor modelo`.

## Entorno

Python 3.11 o superior.

```bash
python -m venv .venv
source .venv/bin/activate        # en Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

Librerías principales: `pandas`, `numpy`, `matplotlib`, `statsmodels`, `scikit-learn`, `scipy` y `openpyxl` (para leer los archivos de Excel).

## Referencias

- Alonso, J. C. — libro guía del curso (los ejemplos del libro están en R).
- Hyndman, R. J. y Athanasopoulos, G. *Forecasting: Principles and Practice* (3.ª ed.). https://otexts.com/fpp3/
- Documentación de [statsmodels](https://www.statsmodels.org/) y [scikit-learn](https://scikit-learn.org/).
