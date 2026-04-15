# 📊 Proyección Electoral Perú – Pipeline de Scraping y Extrapolación

Este proyecto construye un pipeline completo para:

* Extraer resultados electorales desde la ONPE
* Procesar información a nivel provincial (y exterior)
* Estimar votos finales mediante extrapolación
* Generar datasets listos para análisis y simulaciones (Monte Carlo, dashboards, etc.)
* Registrar logs de ejecución para debugging y monitoreo

---

## 🚀 Objetivo

A partir de resultados parciales (actas contabilizadas), se estima el resultado final de la elección utilizando un enfoque de expansión:

[
votos_estimados = \frac{votos}{avance_pct / 100}
]

Donde:

* `avance_pct` = % de **actas contabilizadas** (no procesadas)
* Se asume distribución homogénea de actas faltantes

---

## 🧠 Enfoque metodológico

### ✔ Nivel de análisis

* Perú: **provincial**
* Exterior: agregado por continente

### ✔ Corrección clave

El modelo usa:

* `actasContabilizadas` (correcto)
* ❌ NO usa actas procesadas

Esto evita subestimar el factor de expansión.

---

## ⚙️ Estructura del Pipeline

### 1. Scraping ONPE

Se extrae:

* Provincias
* Votos por candidato
* Actas (avance electoral)

### 2. Integración

* Merge votos + actas
* Inclusión de resultados del extranjero

### 3. Extrapolación

Se calcula:

* `votos_estimados`
* `votos_restantes`

### 4. Métricas territoriales

* Participación por región
* Peso actual vs proyectado

### 5. Agregación nacional

---

## 📁 Outputs generados

### 🔹 1. `resultado_provincial_completo.csv`

Base cruda combinada:

* votos reales
* avance_pct

---

### 🔹 2. `base_intermedia_proyeccion.csv`

Incluye:

* votos estimados
* votos restantes

---

### 🔹 3. `proyeccion_provincial_completa.csv` ⭐ (principal)

Dataset final listo para análisis:

| columna               | descripción      |
| --------------------- | ---------------- |
| candidato             | nombre           |
| departamento          | región           |
| provincia             | provincia        |
| votos                 | votos actuales   |
| votos_estimados       | proyección       |
| votos_restantes       | votos faltantes  |
| avance_pct            | % contabilizado  |
| total_region          | total proyectado |
| pct_region_actual     | share actual     |
| pct_region_proyectado | share final      |

---

### 🔹 4. `nacional_resumen.csv`

Resultado agregado nacional proyectado.

---

### 🔹 5. `log_proceso.csv` 🛠️

Tracking completo de ejecución:

| paso | tiempo_seg | error |
| ---- | ---------- | ----- |

Permite:

* detectar cuellos de botella
* debuggear scraping
* monitorear performance

---

## ▶️ Cómo ejecutar

```bash
python script.py
```

Requisitos:

* Python 3.10+
* Google Chrome
* ChromeDriver compatible

---

## ⚠️ Consideraciones

### 🔁 Re-ejecución

El script es **idempotente**:

* No duplica datos
* No modifica inputs originales
* Puede correrse múltiples veces

---

### 📉 Limitaciones del modelo

* Supone distribución uniforme de votos faltantes
* No corrige sesgos territoriales
* No modela timing de actas

---

## 🔥 Roadmap (próximos pasos)

### 1. Modelo híbrido territorial

* Lima y Callao → nivel distrital
* Resto del país → provincial

👉 Reduce sesgo urbano/marginal

---

### 2. Identificación de provincias críticas

* Top por:

  * votos restantes
  * tamaño electoral

---

### 3. Simulación Monte Carlo

* Variación en shares territoriales
* Estimación probabilística de resultados

---

### 4. Dashboard interactivo

* Tableau / Data Studio
* Seguimiento en tiempo real

---

## 🧪 Uso sugerido

Este dataset es ideal para:

* análisis político-electoral
* investigación académica
* visualización de resultados
* simulaciones probabilísticas

---

## 👨‍💻 Autor

Proyecto desarrollado por Hugo Gutierrez
Economista | Finanzas públicas y privadas | Data analytics

---

## 📌 Nota final

Este proyecto busca transformar datos electorales en herramientas analíticas robustas, manteniendo transparencia metodológica y capacidad de extensión hacia modelos más complejos.

---


Hugo Gutierrez  
Economista PUCP | Finanzas públicas y privadas
