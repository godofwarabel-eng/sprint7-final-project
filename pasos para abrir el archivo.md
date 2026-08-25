# ConnectaTel — Análisis de Clientes y Patrones de Uso

## Objetivo

Analizar el comportamiento de los clientes de ConnectaTel para identificar segmentos por edad y nivel de uso, detectar problemas de calidad en los datos, y generar recomendaciones accionables sobre la oferta de planes (Básico y Premium).

---

## Datasets utilizados

| Archivo | Descripción |
|---|---|
| `users.csv` | Información de clientes: edad, ciudad, fecha de registro y plan contratado |
| `usage.csv` | Registro de eventos de uso: mensajes, llamadas, duración y longitud |

Ambos datasets se integran mediante `user_id` usando un `LEFT JOIN`.

---

## Etapas del análisis

1. **Carga y exploración inicial**
   - Lectura de `users` y `usage`
   - Revisión de columnas, tipos de datos y valores ausentes

2. **Limpieza de datos**
   - Reemplazo de sentinel `-999` en `age` por la mediana
   - Reemplazo de `"?"` en `city` por `pd.NA`
   - Marcado de fechas futuras en `reg_date` como `NaT`
   - Diagnóstico MAR en `duration` y `length` — mantenidos como nulos

3. **Agregación y construcción del perfil de usuario**
   - Cálculo de `cant_mensajes`, `cant_llamadas` y `cant_minutos_llamada` por usuario
   - Integración con `users` mediante `pd.merge`

4. **Análisis estadístico**
   - Resumen numérico con `.describe()` para columnas clave
   - Distribución porcentual de la columna `plan`

5. **Visualización**
   - Histogramas por variable y plan (`hue='plan'`)
   - Boxplots para detección visual de outliers
   - Countplots de segmentos por uso y edad

6. **Segmentación**
   - `grupo_uso`: Bajo uso / Uso medio / Alto uso (basado en llamadas y mensajes)
   - `grupo_edad`: Joven / Adulto / Adulto Mayor (basado en edad)

7. **Conclusiones y recomendaciones**
   - Segmentos más valiosos para el negocio
   - Outliers y su implicación comercial
   - Propuestas de nuevos planes y campañas

---

## Cómo ejecutar el notebook

### Opción 1 — GitHub (solo lectura)
1. Abre el repositorio en [github.com](https://github.com)
2. Navega al archivo `.ipynb`
3. GitHub renderiza el notebook automáticamente — no requiere instalación

### Opción 2 — Google Colab
Abre directamente con este enlace:

[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/godofwarabel-eng/sprint7-final-project/blob/main/S7%20Version-Estudiante-Project-ConnectaTel.ipynb)

### Opción 3 — Local con Jupyter
```bash
git clone https://github.com/godofwarabel-eng/sprint7-final-project.git
cd sprint7-final-project
pip install -r requirements.txt
jupyter notebook
```

---

## Guía de reproducción

1. Clona el repositorio o descarga los archivos.
2. Coloca los datasets en la carpeta `/datasets/`:
   - `users.csv`
   - `usage.csv`
3. Abre el notebook principal (`S7 Version-Estudiante-Project-ConnectaTel.ipynb`).
4. Ejecuta las celdas **en orden de arriba a abajo** — cada celda depende de las anteriores.
5. Si reinicias el kernel, vuelve a ejecutar todas las celdas desde la primera.

### Dependencias

```
pandas
numpy
matplotlib
seaborn
```

Instálalas con:

```bash
pip install pandas numpy matplotlib seaborn
```

---

## Estructura del proyecto

```
sprint7-final-project/
├── datasets/
│   ├── users.csv
│   └── usage.csv
├── S7 Version-Estudiante-Project-ConnectaTel.ipynb
└── README.md
```

---

## Repositorio

GitHub: https://github.com/godofwarabel-eng/sprint7-final-project

---

## Autor

Análisis realizado como parte del bootcamp de análisis de datos.
