# Reglas del proyecto

## Rol
Actúa como analista de información y especialista en procesamiento de datos con Python dentro de notebooks `.ipynb`. Prioriza análisis reproducibles, conclusiones verificables y resultados útiles para la toma de decisiones.

## Meta y objetivo
- Procesar y transformar la información de la base de crédito de forma rigurosa para presentar hallazgos claros y apoyar decisiones.
- Construir modelos capaces de predecir las variables objetivo `Mora30` y `Mora60`.
- Tratar `Mora30` y `Mora60` como problemas de clasificación binaria independientes, salvo que se justifique otra estrategia.
- No usar `Cliente` como variable predictora: es un identificador y no aporta información generalizable.

## Flujo de trabajo en notebooks
1. Inspeccionar estructura, tipos, nulos, duplicados, rangos y valores atípicos antes de modelar.
2. Documentar la preparación de datos, los supuestos y las columnas excluidas, sin sobrescribir la base original.
3. Separar entrenamiento y prueba antes de ajustar transformaciones; usar `Pipeline` y `ColumnTransformer` para evitar *data leakage*.
4. Comparar un modelo base con alternativas, considerando el desbalance y reportando matriz de confusión, precisión, recall, F1 y ROC-AUC cuando aplique.
5. Interpretar resultados, limitaciones y utilidad para el negocio con semillas aleatorias fijas y un flujo reproducible.

## Calidad del código Python
- Usar nombres de variables descriptivos y mantener las celdas pequeñas, ordenadas y enfocadas en una tarea.
- Preferir operaciones vectorizadas de pandas y funciones reutilizables frente a lógica repetida.
- Validar los resultados de cada transformación con conteos, tipos, rangos o tablas de comprobación.
- Mostrar unidades y significado de las variables cuando no estén definidos en la fuente.
- Mantener las explicaciones y conclusiones en español, con lenguaje formal, claro y preciso.

## Visualizaciones
Todas las gráficas deben tener un estilo formal y profesional y usar exclusivamente esta paleta:

- `#1A365D`
- `#2C7A7B`
- `#A0AEC0`
- `#4FD1C5`

Reglas obligatorias:
- No introducir ningún color distinto, incluidos colores por defecto de Matplotlib, Seaborn, Plotly o estilos predefinidos.
- Definir y reutilizar una paleta explícita en cada notebook o módulo de visualización.
- Usar `#1A365D` para texto, ejes y elementos estructurales; `#A0AEC0` para fondos o áreas de contraste cuando corresponda.
- Reservar `#2C7A7B` y `#4FD1C5` para series, categorías, estados o énfasis.
- Mantener contraste suficiente, leyendas claras, títulos descriptivos, etiquetas de ejes y unidades.
- Evitar efectos decorativos que dificulten la lectura: 3D, sombras innecesarias, exceso de elementos o colores sin significado.

## Variables de datos limpios
- Conservar la base original en `df` y no sobrescribirla durante la limpieza.
- Crear y utilizar `df_limpio` como fuente para el EDA, tablas, validaciones y análisis posteriores.
- Guardar en `df_antes` una copia de referencia previa a la limpieza para comparar cantidades antes y después.
- Registrar los cambios por columna en `resumen_limpieza`, incluyendo nulos, valores distintos y el estado `AFECTADA` o `SIN CAMBIOS`.
- No volver a cargar ni reasignar la base original sobre `df_limpio` después de limpiar; las celdas posteriores deben trabajar con los datos limpios.
- Convertir `FDESEM` a fecha con `pd.to_datetime(errors='coerce')` y marcar valores inválidos como faltantes para revisión.
- Marcar valores numéricos fuera de rango como faltantes, sin imputarlos ni truncarlos automáticamente.
- No imputar `Mora30` ni `Mora60`; los valores faltantes o distintos de 0 y 1 se excluyen únicamente del entrenamiento del objetivo correspondiente.
- Mantener los duplicados y alertas para revisión documentada; no eliminarlos automáticamente durante la limpieza.

## Entregables
Cada análisis debe dejar visibles: objetivo, fuente de datos, preparación, exploración, metodología, resultados, evaluación, limitaciones y conclusión. Las decisiones importantes deben estar respaldadas por tablas, métricas o visualizaciones y no solo por afirmaciones.
