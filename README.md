# 🚚 Sistema de Predicción de Fallos en Última Milla
## KPI Nacional de Distribución Logística — Argentina 2022-2024

![Python](https://img.shields.io/badge/Python-3.13-blue?logo=python&logoColor=white)
![XGBoost](https://img.shields.io/badge/ML-XGBoost-orange)
![Dash](https://img.shields.io/badge/Dashboard-Plotly%20Dash-informational)
![SAP](https://img.shields.io/badge/ERP-SAP%20TM-blue)
![UNIGIS](https://img.shields.io/badge/TMS-UNIGIS-green)
![Status](https://img.shields.io/badge/Status-Producción-brightgreen)

---

## 🎯 Problema de Negocio

En Argentina, el **22.1% de los envíos de última milla fallan** antes de llegar
al destinatario. Cada envío fallido genera:

- 💸 Costo de reenvío y gestión de devolución
- ⏱️ Demoras que afectan la satisfacción del cliente
- 📉 Impacto directo en el margen operativo del transportista
- 🔄 Sobrecarga operativa en los centros de distribución

Con **500.000 envíos analizados** entre 2022 y 2024, el costo total
acumulado de fallos superó los **$1.034 millones de pesos**.

---

## 💡 Solución Propuesta

Sistema de Machine Learning que predice con **99.14% de accuracy**
si un envío será exitoso **antes de despacharlo**, permitiendo:

✅ Reasignar envíos de alto riesgo a transportistas más confiables
✅ Alertar al planificador sobre zonas y condiciones de riesgo
✅ Reducir la tasa de fallo del 22.1% al objetivo del 10%
✅ Ahorro estimado de **$310 millones de pesos anuales**

---

## 🔍 Insights Logísticos Descubiertos

### 📍 Por Zona
| Zona | Tasa de Éxito | Riesgo |
|---|---|---|
| Urbana | ~90% | 🟢 Bajo |
| Suburbana | ~83% | 🟡 Medio |
| Rural | ~72% | 🟠 Alto |
| Zona Peligrosa | ~52% | 🔴 Crítico |

### 🚚 Por Transportista
- **DHL y FedEx** lideran en tasa de éxito pero tienen el mayor costo
- **Correo Argentino** tiene el mayor volumen con performance media
- La diferencia entre el mejor y peor transportista supera los **15 puntos porcentuales**

### 📅 Estacionalidad Argentina
- **Navidad y Cyber Monday** generan un aumento del **320%** en volumen
- **Junio y Diciembre** (Aguinaldo) disparan las demoras por sobrecarga
- **Marzo** (Vuelta al Cole) muestra la menor tasa de distribución del año
- El clima **Tormentoso y Nieve** aumenta las demoras hasta **4 horas extra**

### 💰 Impacto de la Inflación
| Año | Costo Promedio de Envío |
|---|---|
| 2022 | Baseline |
| 2023 | +95% vs 2022 |
| 2024 | +280% vs 2022 |

---

## 🤖 Resultados Técnicos

### Modelos de Machine Learning

| Modelo | Objetivo | Algoritmo | Resultado |
|---|---|---|---|
| **Modelo 1** | ¿Entrega exitosa? | XGBoost | **Accuracy 99.14%** ✅ |
| **Modelo 2** | Nivel de riesgo del envío | XGBoost | **Accuracy 90.12%** ✅ |
| **Modelo 3** | Costo estimado del envío | XGBoost | **En optimización** 🔄 |

### Métricas Detalladas Modelo 1
```
Accuracy  : 99.14%
F1-Score  : 0.9915
AUC-ROC   : 0.9998
```

### Métricas Detalladas Modelo 2
```
Accuracy     : 90.12%
F1 Weighted  : 0.9043
F1 Macro     : 0.7112

Niveles de riesgo:
  🟢 Sin Riesgo   (Entregado)     → 77.9% del total
  🟡 Riesgo Medio (Demorado)      → 14.3% del total
  🔴 Riesgo Alto  (Perdido/Dev.)  →  7.8% del total
```

---

## 🏗️ Arquitectura del Sistema
```
CAPA 1 — FUENTES DE DATOS
    SAP TM       → Órdenes, costos, clientes en tiempo real
    UNIGIS TMS   → Rutas, tracking GPS, choferes
    Dataset CSV  → 500K registros históricos 2022-2024
    APIs         → Clima, feriados, eventos especiales AR
         ↓
CAPA 2 — PROCESAMIENTO
    ETL + Limpieza + Feature Engineering
    pandas · numpy · scikit-learn
    Score de riesgo compuesto por zona + clima + evento
         ↓
CAPA 3 — MODELOS ML
    Modelo 1 → Clasificación Binaria    (ACC 99.14%)
    Modelo 2 → Niveles de Riesgo        (ACC 90.12%)
    Modelo 3 → Regresión de Costo       (En optimización)
    Motor: XGBoost · joblib
         ↓
CAPA 4 — OUTPUTS
    Alertas de riesgo por envío
    Score de probabilidad 0 a 1
    Reportes automáticos Excel/PDF
         ↓
CAPA 5 — VISUALIZACIÓN
    Dashboard Plotly Dash interactivo
    Filtros por zona, transportista, fecha
    Mapa de Argentina con envíos en tiempo real
         ↓
CAPA 6 — INTEGRACIÓN EMPRESARIAL
    SAP TM  → Score de riesgo al panel del planificador
    UNIGIS  → Alertas de ruta al despachante en tiempo real
```

### Integración SAP / UNIGIS
Este sistema está diseñado para integrarse con:
- **SAP Transport Management (TM)** via RFC para leer órdenes
  y escribir scores de riesgo de vuelta al sistema
- **UNIGIS TMS** via API REST para obtener tracking en tiempo
  real y enviar alertas de riesgo al panel del despachante

---

## 📁 Estructura del Proyecto
```
sistema_de_Predicción_de_Fallos_en_Última_Milla/
│
├── 📂 data/
│   ├── raw/
│   │   └── dataset_distribucion_nacional2.csv
│   ├── processed/
│   │   └── dataset_limpio.csv
│   └── external/
│       └── feriados_argentina.csv
│
├── 📂 notebooks/
│   ├── 01_exploracion_inicial.ipynb
│   ├── 01b_eda_avanzado.ipynb
│   ├── 02_limpieza_y_transformacion.ipynb
│   ├── 03_feature_engineering_y_modelado.ipynb
│   └── 04_evaluacion_resultados.ipynb
│
├── 📂 src/
│   ├── data_loader.py
│   ├── data_cleaner.py
│   ├── forecast_model.py
│   └── visualizations.py
│
├── 📂 dashboard/
│   └── dashboard.py
│
├── 📂 integracion/
│   ├── sap/
│   │   └── sap_connector.py
│   └── unigis/
│       └── unigis_connector.py
│
├── 📂 outputnts/
│   ├── figures/
│   ├── models/
│   └── reports/
│
├── .gitignore
├── requirements.txt
└── README.md
```

---

## 🚀 Cómo Ejecutar el Proyecto

### 1. Clonar el repositorio
```bash
git clone https://github.com/jvillagra66-oss/sistema-prediccion-fallos-ultima-milla.git
cd sistema-prediccion-fallos-ultima-milla
```

### 2. Instalar dependencias
```bash
pip install -r requirements.txt
```

### 3. Ejecutar notebooks en orden
```
01_exploracion_inicial.ipynb
01b_eda_avanzado.ipynb
02_limpieza_y_transformacion.ipynb
03_feature_engineering_y_modelado.ipynb
04_evaluacion_resultados.ipynb
```

### 4. Lanzar el dashboard
```bash
python dashboard/dashboard.py
```
Abrí tu navegador en: **http://localhost:8050**

---

## 🛠️ Stack Tecnológico

| Categoría | Tecnología |
|---|---|
| Lenguaje | Python 3.13 |
| Machine Learning | XGBoost, Scikit-learn |
| Visualización | Matplotlib, Seaborn, Plotly |
| Dashboard | Dash, Dash Bootstrap Components |
| Procesamiento | Pandas, NumPy, SciPy |
| ERP Integration | SAP TM (RFC), UNIGIS (API REST) |
| Serialización | Joblib |
| Entorno | Jupyter Notebook, VS Code |

---

## 👤 Autor

**Matías**
- 🏭 Analista de Logística y Distribución
- 📊 Data Scientist — Supply Chain
- 🔗 Experiencia en SAP TM y UNIGIS TMS
- 📍 Argentina

---

## 📄 Licencia

Proyecto desarrollado con fines profesionales y de portfolio.
Los datos utilizados son sintéticos generados con Python.
