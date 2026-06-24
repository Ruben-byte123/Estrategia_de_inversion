# Estrategia_de_inversion
# Análisis de Portafolios de Inversión y Gestión de Riesgo (VaR & CVaR)

Este repositorio contiene las herramientas y metodologías necesarias para el análisis cuantitativo, la optimización y la gestión de riesgo de un portafolio de inversión compuesto por renta variable de los mercados mexicano y estadounidense (cotizando a través del SIC). 

Los módulos analíticos están desarrollados en Python mediante Jupyter Notebooks y se enfocan en la captura de datos históricos reales, la optimización bajo criterios de mínimo riesgo y la simulación del riesgo mediante múltiples metodologías de valor en riesgo.

##  Componentes del Proyecto

El proyecto está estructurado en dos fases analíticas principales correspondientes a los cuadernos de código adjuntos:

1. **Optimización de Portafolios (`Portafolio.ipynb`)**: Modelado estadístico de los activos individuales, cálculo de la matriz de varianza-covarianza y estimación empírica/teórica de las distribuciones de rendimiento.
2. **Medición y Gestión de Riesgo (`VaR.ipynb`)**: Implementación del **Valor en Riesgo (VaR)** y **Valor en Riesgo Condicional (CVaR)** a través de tres metodologías estándar de la industria, simulación histórica de pérdidas y ganancias (P&L), identificación de *outliers* y análisis comparativo contra tasas libres de riesgo (CETES) e inflación.

---

## 🛠️ Activos e Información del Portafolio

El portafolio base analiza un capital de **$1,000,000 MXN** distribuido bajo la ponderación del **Portafolio de Mínimo Riesgo (MR)** para los siguientes 10 activos (utilizando un histórico de 2 años extraído directamente de Yahoo Finance):

* **Mercado Mexicano:** `GFNORTEO.MX`, `WALMEX.MX`, `GMEXICOB.MX`, `CEMEXCPO.MX`, `GENTERA.MX`
* **Mercado Estadounidense (SIC):** `MSFT.MX`, `AAPL.MX`, `AMZN.MX`, `GOOGL.MX`, `NVDA.MX`

---

##  Características y Metodologías Implementadas

### 1. Análisis Estadístico y Distribuciones
* Conversión de precios de cierre históricos a **rendimientos logarítmicos** (`np.log(precios).diff()`).
* Construcción automática de curvas de densidad empíricas vs. teóricas (Distribución Normal).
* Generación de Funciones de Distribución Acumulada Teórica (**CDF**) y Real Acumulada (**ECDF**) individuales por activo a través de visualizaciones dinámicas con `Plotly`.

### 2. Gestión de Riesgo Cuantitativa (Módulo VaR)
El modelo evalúa la pérdida máxima potencial en un horizonte diario bajo un **nivel de confianza del 95%** utilizando tres enfoques:
* **Método Paramétrico (Varianza-Covarianza):** Basado en el supuesto de normalidad y el cálculo matricial utilizando el vector de pesos y la matriz de covarianza de la muestra.
* **Método de Simulación Histórica:** Estimación no paramétrica basada puramente en el percentil empírico de las pérdidas históricas del portafolio.
* **Simulación de Monte Carlo:** Generación de trayectorias estocásticas basadas en la media y desviación estándar para proyectar escenarios de comportamiento del portafolio.

Adicionalmente, se calcula el **CVaR (Expected Shortfall)** para determinar la pérdida promedio esperada en los escenarios de cola más adversos (el 5% peor).

### 3. Filtros y Control de Estrés (P&L Historico)
* Detección de valores atípicos (*Outliers*) de la valuación mediante el uso del **Rango Intercuartílico (IQR)** con umbrales estrictos (`Q1 - 3*IQR` / `Q3 + 3*IQR`).
* Análisis del impacto histórico real de crisis de mercado internacionales (ej. Stress testing implícito).
* Gráfico de crecimiento acumulado comparativo: **Portafolio vs. CETES vs. Inflación**.

---

##  Requisitos e Instalación

Para ejecutar los notebooks de este repositorio, asegúrate de tener instaladas las siguientes librerías de Python:

```bash
pip install yfinance numpy pandas scipy matplotlib seaborn plotly ydata-profiling
