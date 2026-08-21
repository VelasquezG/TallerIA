# Diccionario de datos y glosario — Base de crédito (Proyecto Único)

**Curso:** Inteligencia Artificial · Ingeniería de Software — Tecnológico de Antioquia
**Base de datos:** archivo de crédito con **10.000 clientes** y **27 columnas**, cuyo problema de negocio es predecir si un cliente entrará en mora (`Mora30` / `Mora60`).

Este documento explica **qué significa cada variable** de la base que su equipo tiene asignada. No es un diagnóstico de calidad de datos: identificar nulos, valores atípicos, inconsistencias y columnas que no deberían usarse en el modelo (leakage) es parte del trabajo que cada equipo debe descubrir por sí mismo en el taller de la Semana 4. Aquí solo van a encontrar el significado conceptual de cada campo.

---

## 1. Identificación del cliente

| Variable | Tipo de dato | Qué significa |
|---|---|---|
| `Cliente` | Identificador numérico | Número único que identifica a cada cliente en la base. No aporta información predictiva — es solo una llave para distinguir filas, no una característica del cliente. |

---

## 2. Variables objetivo (lo que el modelo debe predecir)

| Variable | Tipo de dato | Qué significa |
|---|---|---|
| `Mora30` | Binaria (0 / 1) | Indica si el cliente incurrió en mora **igual o mayor a 30 días** en el pago de su crédito. `1` = sí cayó en mora30, `0` = no. |
| `Mora60` | Binaria (0 / 1) | Indica si el cliente incurrió en mora **igual o mayor a 60 días**. `1` = sí, `0` = no. Es un umbral de incumplimiento más severo que `Mora30`. |

> Estas son las **variables dependientes** del Proyecto Único: todo el modelado de la Entrega 2 (Semana 12) busca predecir una de estas dos columnas a partir de las demás.

---

## 3. Datos de la operación de crédito

| Variable | Tipo de dato | Qué significa |
|---|---|---|
| `Segmento` | Categórica nominal | Segmento comercial al que el banco asigna al cliente (valores: `PY`, `MPY`, `MDO`, `VIP`, `STD`). Suele reflejar el tipo de cliente o el modelo de atención (por ejemplo, empresarial, microempresa, mercado masivo, preferencial, estándar). Confirmen con su docente el significado exacto de cada sigla usado en este curso. |
| `SECTOR` | Categórica nominal | Sector económico de la actividad del cliente o de la empresa (Servicios, Agropecuario, Personas Naturales, Comercio, Manufactura, Servicios Financieros, Edificaciones, Gobierno, Recursos Naturales, Infraestructura). |
| `REGCONS` | Categórica nominal | Región o zona geográfica de gestión comercial del cliente (Especial, Occidente, Centro, Sur, Norte). |
| `FDESEM` | Fecha | Fecha de desembolso del crédito, es decir, el día en que el banco entregó el dinero al cliente. |

---

## 4. Datos sociodemográficos del cliente

| Variable | Tipo de dato | Qué significa |
|---|---|---|
| `Edad` | Numérica discreta | Edad del cliente, en años. |
| `Género` | Categórica nominal | Género del cliente (`FEMENINO`, `MASCULINO`). |
| `Estado_Civil` | Categórica nominal | Estado civil del cliente (Soltero, Casado, Divorciado, Viudo, Otros). |
| `Nivel_Academico` | Categórica ordinal | Máximo nivel educativo alcanzado (Bachiller, Tecnólogo, Universitario, Especialización, Otros). |
| `Tipo_Vivienda` | Categórica nominal | Tipo de tenencia de la vivienda donde reside el cliente (Familiar, Alquilada, Propia). |
| `PersonasCargo` | Numérica discreta | Número de personas que dependen económicamente del cliente. |

---

## 5. Datos laborales y de ingresos

| Variable | Tipo de dato | Qué significa |
|---|---|---|
| `OCUPACIÓN` | Categórica nominal | Ocupación laboral del cliente (Empleado, Jubilado/Pensionado, Profesional Independiente). |
| `TIPCONTRATO` | Categórica nominal | Tipo de contrato laboral (Término Indefinido, Término Fijo, Libre Nombramiento o Remoción, Obra Labor o Misión, Carrera Administrativa, Nombramiento Provisional, Otros). Aplica principalmente a clientes empleados. |
| `TIEMPACTIVAÑO` | Numérica discreta | Tiempo de antigüedad, en años, en la actividad laboral o empresa actual del cliente. |
| `Ingresos` | Numérica continua | Ingresos del cliente. La escala exacta (por ejemplo, millones de pesos o salarios mínimos) no viene especificada en el archivo — verifíquenla con su docente antes de usarla en el modelo. |
| `Ingresos_Totales` | Numérica continua | Ingresos totales asociados al cliente u hogar (puede incluir ingresos adicionales al principal). Al igual que `Ingresos`, confirmen la unidad de medida. |
| `Gastos` | Numérica continua | Gastos mensuales del cliente o del hogar. |

---

## 6. Historial y comportamiento crediticio

| Variable | Tipo de dato | Qué significa |
|---|---|---|
| `Calificación Superfinanciera` | Categórica ordinal | Calificación de riesgo crediticio bajo la metodología de la Superintendencia Financiera de Colombia. Va de `A` (riesgo normal, mejor calificación) a `E` (riesgo de incobrabilidad, la peor). Orden de mejor a peor: **A > B > C > D > E**. |
| `CalificaciónSistema Financiero` | Numérica (tipo score) | Puntaje o score crediticio del cliente dentro del sistema financiero, similar a un score de central de riesgo (a mayor puntaje, generalmente menor riesgo percibido). |
| `MoraMaxima 12 meses` | Numérica discreta | Máximo número de días en mora que registró el cliente, considerando todas sus obligaciones, durante los últimos 12 meses. |
| `%Deuda Actual Sistema Financiero` | Numérica continua (proporción) | Proporción de la deuda actual del cliente frente al sistema financiero (por ejemplo, nivel de utilización de sus cupos de crédito). Se expresa entre 0 y 1 (0% a 100%). |
| `Experiencia Financiera` | Binaria (0 / 1) | Indica si el cliente ya tenía experiencia previa en el sistema financiero (`1`) o si es un cliente nuevo sin historial (`0`). |
| `Antigüedad en el Sistema Financiero` | Numérica discreta | Años que el cliente lleva vinculado/registrado dentro del sistema financiero. |
| `Numero de creditos vigentes` | Numérica discreta | Cantidad de créditos que el cliente tiene activos actualmente en el sistema financiero. |

> **Nota técnica:** en el archivo original hay **dos columnas con el nombre `MoraMaxima 12 meses`**. Al abrir la base con `pandas`, Python renombra automáticamente la segunda como `MoraMaxima 12 meses.1` para que ambas columnas tengan un nombre distinto internamente. Tengan esto presente al explorar la base con `df.columns` — es un comportamiento normal de pandas ante nombres de columna repetidos, no un error de su código.

---

## Glosario de términos técnicos

**Mora:** situación en la que un cliente no realiza el pago de su crédito en la fecha pactada. Se suele medir en días de atraso (por ejemplo, mora30 = 30 días o más de atraso).

**Variable objetivo (o variable dependiente):** la variable que el modelo de Machine Learning intenta predecir. En este proyecto es `Mora30` o `Mora60`.

**Variable predictora (o variable independiente / *feature*):** cada una de las columnas que el modelo usa como insumo para predecir la variable objetivo (edad, ingresos, score, etc.).

**Variable categórica nominal:** variable cualitativa cuyos valores son categorías sin un orden natural entre sí (por ejemplo, `Género` o `Estado_Civil`).

**Variable categórica ordinal:** variable cualitativa cuyas categorías sí tienen un orden lógico (por ejemplo, la `Calificación Superfinanciera`, donde A es mejor que E).

**Variable numérica discreta:** variable cuantitativa que solo toma valores enteros y contables (por ejemplo, número de personas a cargo).

**Variable numérica continua:** variable cuantitativa que puede tomar cualquier valor dentro de un rango (por ejemplo, ingresos o porcentaje de deuda).

**Score crediticio:** puntaje numérico calculado por una entidad o central de riesgo que resume qué tan "riesgoso" es un cliente desde el punto de vista financiero.

**Central de riesgo / buró de crédito:** entidad que centraliza el historial crediticio de las personas (en Colombia, por ejemplo, DataCrédito o TransUnion), y que las entidades financieras consultan antes de otorgar un crédito.

**Superintendencia Financiera de Colombia (SFC):** entidad estatal que supervisa el sistema financiero colombiano y define, entre otras cosas, la metodología de calificación de riesgo (A a E) que usan los bancos para clasificar sus créditos.

**Leakage (fuga de información):** cuando una variable predictora contiene información que en la práctica no estaría disponible en el momento de hacer la predicción (o que ya "revela" el resultado), lo que hace que el modelo parezca funcionar muy bien en el entrenamiento pero falle en la realidad. Identificar posibles columnas con leakage es parte del taller de la Semana 4.

**Valores nulos / faltantes (missing values):** celdas de una columna que no tienen dato registrado. Es uno de los problemas de calidad de datos que cada equipo debe detectar en su base.

**Valor atípico (outlier):** un valor que se aleja mucho del comportamiento normal de una variable y que puede deberse a un error de captura o a un caso genuinamente extremo. También es parte del taller de detección de calidad de datos.

**EDA (Exploratory Data Analysis / Análisis Exploratorio de Datos):** proceso de explorar una base de datos con estadísticas descriptivas y visualizaciones antes de modelar, para entender su estructura, calidad y relaciones entre variables.

**`.info()` (pandas):** función que muestra el tipo de dato y la cantidad de valores no nulos de cada columna de un DataFrame.

**`.describe()` (pandas):** función que muestra estadísticas descriptivas (promedio, mínimo, máximo, cuartiles) de las columnas numéricas de un DataFrame.

---

*Documento de apoyo para el Proyecto Único — Inteligencia Artificial, Tecnológico de Antioquia.*
