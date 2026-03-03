# 📡 Telecom X — Parte 2: Modelo Predictivo de Evasión de Clientes (Churn)

> **Challenge Data Science LATAM** · Segunda Fase  
> Herramientas: Python · Pandas · Scikit-learn · XGBoost · Matplotlib · Seaborn

---

## 📋 Descripción del Proyecto

Este repositorio contiene la **segunda fase** del análisis de churn de clientes para **Telecom X**, una empresa de telecomunicaciones con alta tasa de cancelaciones. Partiendo del dataset limpio generado en la Parte 1 (proceso ETL + EDA), esta fase construye, evalúa y compara modelos de Machine Learning para **predecir qué clientes tienen mayor riesgo de cancelar** el servicio.

### Pregunta central
> ¿Quiénes son los clientes con mayor riesgo de evasión, qué variables influyen más en ese comportamiento y qué perfil de cliente debemos cuidar con mayor atención?

---

## 🗂️ Estructura del Repositorio

```
telecomx-churn-parte2/
│
├── 📓 TelecomX_LATAM_Parte2_ModeloPredictivo.ipynb   ← Notebook principal
├── 📓 TelecomX_LATAM_Completo.ipynb                  ← Notebook Parte 1 (referencia)
├── 📄 TelecomX_churn_scores.csv                      ← Scores de riesgo por cliente (output)
├── 🤖 telecomx_model_*.pkl                           ← Modelo serializado (output)
└── 📖 README.md                                      ← Este archivo
```

---

## 🔄 Pipeline del Notebook

```
1. Carga y Preparación
   └── Reconstrucción desde API  →  One-Hot Encoding  →  Eliminación de columnas irrelevantes

2. Análisis de Balance de Clases
   └── Verificación desbalance  →  SMOTE / Oversampling manual

3. Correlación y Selección de Variables
   └── Correlación de Pearson  →  Información Mutua  →  StandardScaler

4. Modelado Predictivo
   └── Logistic Regression  →  Random Forest  →  Gradient Boosting / XGBoost

5. Evaluación de Modelos
   └── Accuracy · Precision · Recall · F1 · AUC-ROC  →  Matrices de Confusión  →  Curvas ROC

6. Análisis de Importancia de Variables
   └── Feature Importance (RF + GB)  →  Coeficientes (LR)  →  Comparativa

7. Perfil de Riesgo
   └── Segmentación: Bajo / Medio / Alto Riesgo  →  Perfil del cliente de mayor riesgo

8. Conclusión Estratégica
   └── Informe final  →  Recomendaciones  →  Exportación de resultados
```

---

## 🚀 Cómo ejecutar

### Opción A — Google Colab (recomendado)

1. Abre [Google Colab](https://colab.research.google.com)
2. Sube el archivo `TelecomX_LATAM_Parte2_ModeloPredictivo.ipynb`
3. Ejecuta la primera celda para instalar dependencias:
   ```python
   !pip install imbalanced-learn xgboost --quiet
   ```
4. Ejecuta todas las celdas en orden (`Runtime → Run all`)

### Opción B — Entorno local

```bash
# 1. Clonar repositorio
git clone https://github.com/tu-usuario/telecomx-churn-parte2.git
cd telecomx-churn-parte2

# 2. Crear entorno virtual
python -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Lanzar Jupyter
jupyter notebook TelecomX_LATAM_Parte2_ModeloPredictivo.ipynb
```

### Dependencias principales

```txt
pandas>=1.5
numpy>=1.23
scikit-learn>=1.2
imbalanced-learn>=0.11
xgboost>=1.7
matplotlib>=3.6
seaborn>=0.12
joblib>=1.2
requests>=2.28
```

---

## 📊 Resultados Principales

### Métricas de Modelos (valores aproximados)

| Modelo | Accuracy | F1-Score | AUC-ROC |
|--------|:--------:|:--------:|:-------:|
| Logistic Regression | ~79% | ~0.62 | ~0.85 |
| Random Forest | ~81% | ~0.65 | ~0.87 |
| **Gradient Boosting / XGBoost** | **~82%** | **~0.67** | **~0.88** |

> El modelo final recomendado es **Gradient Boosting / XGBoost** por su mejor balance entre precisión y recall sobre la clase de churn.

### Top Variables Predictoras

| # | Variable | Descripción |
|---|----------|-------------|
| 1 | `tenure` | Antigüedad del cliente (meses) |
| 2 | `contract_Month-to-month` | Contrato mensual sin compromiso |
| 3 | `monthly_charges` | Monto mensual del servicio |
| 4 | `internet_service_Fiber optic` | Tipo de internet contratado |
| 5 | `payment_method_Electronic check` | Método de pago manual |
| 6 | `total_charges` | Acumulado histórico de pagos |
| 7 | `online_security` | Tiene seguridad online contratada |
| 8 | `total_services` | Número total de servicios activos |

### Perfil del Cliente de Mayor Riesgo

```
✗ Contrato mensual (sin compromiso)
✗ Antigüedad < 12 meses
✗ Servicio de Fibra Óptica
✗ Pago por cheque electrónico
✗ Cargo mensual > $70
✗ Sin seguridad online ni soporte técnico
```

---

## 💡 Recomendaciones Estratégicas

| Prioridad | Acción | Impacto |
|-----------|--------|---------|
| 🔴 Alta | Programa de onboarding en primeros 3 meses | Retención temprana |
| 🔴 Alta | Incentivos para migrar a contrato anual | Reduce churn 3-4x |
| 🔴 Alta | Auditoría calidad/precio Fiber Optic | Corrige causa raíz |
| 🔴 Alta | Sistema de alertas tempranas con el modelo | Acción preventiva |
| 🟡 Media | Bundles con descuento (seguridad + soporte) | Aumenta stickiness |
| 🟡 Media | Campaña de pagos automáticos | Reduce fricción |

---

## 📁 Archivos de Salida

| Archivo | Descripción |
|---------|-------------|
| `TelecomX_churn_scores.csv` | Dataset completo con `churn_proba` y `risk_segment` por cliente |
| `telecomx_model_*.pkl` | Mejor modelo serializado con `joblib` listo para producción |

---

## 🔗 Fuente de Datos

Los datos se cargan directamente desde la API oficial del challenge:

```
https://raw.githubusercontent.com/ingridcristh/challenge2-data-science-LATAM/refs/heads/main/TelecomX_Data.json
```

---

## 👤 Autor

Desarrollado como parte del **Challenge 2 — Data Science LATAM**  
Telecom X · Análisis de Evasión de Clientes  

---

## 📝 Licencia

Este proyecto es de uso educativo en el marco del challenge de formación en Data Science.
