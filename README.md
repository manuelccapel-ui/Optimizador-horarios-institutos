# Optimizador de horarios escolares (CP-SAT / OR-Tools) 🗓️⚙️

Proyecto de **optimización de horarios** para un instituto, formulado como un problema de satisfacción/optimización con restricciones usando **OR-Tools (CP-SAT)**.  
A partir de la asignación *profesor–grupo–asignatura*, las **horas semanales** de cada materia y las **restricciones** del profesorado, el modelo genera un horario factible y, además, minimiza una función objetivo con **restricciones blandas** (calidad del horario).

---

## Qué hace el proyecto

- Construye un modelo con variables binarias `x[p,g,d,h]` = 1 si el profesor `p` da clase al grupo `g` el día `d` a la hora `h`.
- Impone **restricciones duras** (obligatorias) para asegurar factibilidad.
- Penaliza **restricciones blandas** (preferencias) para mejorar la calidad del horario.
- Exporta el horario final a CSV, **un archivo por grupo**.

---


---

## Requisitos

Python 3.x y las siguientes librerías:

- `ortools`
- `pandas`, `numpy`
- (opcionales) `matplotlib`, `seaborn`

Instalación rápida:

```bash
pip install ortools pandas numpy matplotlib seaborn

---

## Datos de entrada

El optimizador se alimenta de 3 CSV (generados desde TXT con los notebooks de parsing):

# 1) data/prueba_horario_instituto.csv (compatibilidad + restricciones)

Matriz binaria profesor × grupo, con:

id_profesor

Una columna por cada grupo (ej. 1E_A, 2BACH_C, …) con valores 0/1

restricciones con formato "dia_hora" (ej. "3_5")

Nota: tal como está el parser, por defecto guarda una restricción por profesor (si hay varias líneas, se queda con la última). Se puede ampliar fácilmente para soportar varias.

# 2) data/prueba_profesor_grupo_asignatura.csv (quién da qué a quién)

Columnas:

profesor, curso, letra, grupo, asignatura

Ejemplo (conceptual):

MAT1, 1E, A, 1E_A, MAT

# 3) data/prueba_horas_semanales.csv (horas por curso y asignatura)

Columnas:

curso, asignatura, horas_semanales

Ejemplo (conceptual):

1E, MAT, 4

# Cómo generar los CSV desde TXT
A) Asignación profesor–grupo–asignatura + compatibilidad

Notebook: notebooks/parse_txt_to_csv.ipynb

Lee:

data/informacion_asignacion_profesorado.txt

data/restricciones_profesores.txt (opcional)

Genera:

data/prueba_profesor_grupo_asignatura.csv

data/prueba_horario_instituto.csv
