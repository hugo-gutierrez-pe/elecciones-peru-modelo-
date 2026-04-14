# 📊 Simulación Electoral Perú – Extrapolación por Provincias

Este proyecto construye una estimación del resultado electoral nacional a partir de resultados parciales publicados por la ONPE.

## 🎯 Objetivo

Explorar si, bajo ciertos supuestos razonables, el candidato Roberto Sánchez podría superar a Rafael López Aliaga en el resultado final.

## ⚙️ Metodología

1. Se extraen resultados oficiales desde la web de ONPE a nivel provincial
2. Se obtiene:
   - votos por candidato
   - porcentaje de actas contabilizadas
3. Se aplica una extrapolación simple:

   votos_estimados = votos_actuales / (avance_pct / 100)

4. Se agregan resultados a nivel nacional
5. Se calculan porcentajes de votos válidos

## 📁 Archivos

- `codigo_provincias.ipynb` → extracción + procesamiento
- `resultado_provincial_completo.csv` → base consolidada
- `top20_nacional_provincial.csv` → ranking nacional proyectado

## ⚠️ Limitaciones

- Modelo asume que votos faltantes siguen patrón actual (sesgo potencial)
- No incorpora heterogeneidad temporal (actas rurales vs urbanas)
- Resultados deben interpretarse como simulación, no predicción oficial

## 🔬 Extensiones

- Simulación dinámica usando diferencias entre cortes temporales
- Ajuste por sesgo rural
- Modelos probabilísticos (Monte Carlo)

## 👤 Autor

Hugo Gutierrez  
Economista PUCP | Finanzas públicas y privadas
