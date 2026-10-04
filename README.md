# **Ciencia de Datos: Conectividad y Dinámica Aerocomercial en el Turismo Argentino**

# **Integrantes del equipo**

* **Facundo Acosta** – Coordinador / Comunicador / Documentador  
* **Nicole Guerrero Cabrera** – Analista de Datos (Foco Estructural)  
* **William Naufamer** – Responsable de Calidad de Datos  
* **Leonardo Elian Nuñez Marin** – Analista de Datos (Foco Visual)
* **Flavia Andrea Matus Aracena**  - (Ausente)

*Nota de gestión:* El equipo adaptó la distribución de responsabilidades y la carga operativa entre los 4 integrantes activos para garantizar la ejecución efectiva del proyecto.

# **Descripción del proyecto**

El sector turístico y aerocomercial argentino atraviesa una transformación estructural impulsada por la apertura a la competencia, la reconfiguración de frecuencias y la variabilidad en el flujo de pasajeros. Comprender la dinámica temporal y geográfica de estos flujos permite diagnosticar la resiliencia de los destinos frente a la estacionalidad turística.

Este proyecto tiene como propósito aplicar técnicas de ciencia de datos cuantitativa sobre microdatos oficiales para analizar la variabilidad, estabilidad y concentración estacional del tráfico de pasajeros aéreo en Argentina durante el período de enero de 2017 a julio de 2026\. El análisis permite diferenciar los comportamientos entre ciudades urbanas con demanda continua y destinos turísticos dependientes de temporadas específicas (verano e invierno).

# **Fuente de datos**

* **Fuente oficial:** Sistema Integrado de Aviación Civil (SIAC) de la Administración Nacional de Aviación Civil (ANAC), procesado y publicado por la plataforma SINTA \- Yvera (Subsecretaría de Turismo de la Nación).  
* **Dataset principal:** `base_microdatos.csv`  
* **Volumen de datos:** 1.078.289 registros agregados a nivel diario para el período 2017 – 2026\.  
* **Estructura:** 19 variables que incluyen dimensiones temporales (`indice_tiempo`), categóricas de servicio (`clasificacion_vuelo`, `clase_vuelo`, `aerolinea`), geográficas de origen/destino (`origen_oaci`, `origen_aeropuerto`, `origen_provincia`, `destino_oaci`, `destino_aeropuerto`, `destino_provincia`) y métricas cuantitativas operacionales (`pasajeros`, `asientos`, `vuelos`).

# **Objetivos del análisis**

## **Objetivo general**

Diagnosticar la resiliencia temporal y la concentración estacional de los flujos turísticos aerocomerciales en Argentina para proporcionar inteligencia estratégica que optimice la toma de decisiones públicas y corporativas en la asignación de capacidad.

## **Objetivos específicos**

1. **Identificar estabilidad:** Determinar qué destinos y aeropuertos de Argentina presentan un comportamiento de demanda de pasajeros más estable a lo largo del año.  
2. **Cuantificar variabilidad:** Detectar qué provincias y destinos turísticos sufren mayores oscilaciones o valles estacionales en la afluencia mensual de pasajeros.  
3. **Evaluar persistencia temporal:** Analizar si los patrones de concentración mensual de pasajeros en picos estacionales se mantienen constantes a lo largo de los distintos años evaluados (2017–2026).

# **Herramientas utilizadas**

* **Lenguaje de programación:** Python  
* **Análisis y modelado:** Coeficiente de Variación (CV) y Agrupamientos Temporales.   
* **Visualización e informes:** Power BI / Excel  
* **Gestión de proyecto:** GitHub, Trello, Diagrama de Gantt, Google Drive

# **Proceso de análisis**

1. **Ingesta y exploración estructural (EDA):** Carga de datos, verificación de volumen (filas y columnas) e inspección de consistencia general de microdatos.  
2. **Limpieza y calidad de datos:**  
   * Tratamiento de valores ausentes en variables geográficas (detectados principalmente en `origen_provincia` y `destino_provincia` para vuelos internacionales).  
   * Unificación de fuentes descartando tablas redundantes para mantener la integridad en `base_microdatos.csv`.  
   * Identificación de registros atípicos (outliers) y aislamiento de la anomalía operativa registrada en 2020 por la emergencia sanitaria. Este período será aislado como variable de control para no contaminar la "huella estacional" del modelo STL interanual.   
3. **Transformación y procesamiento estadístico:**  
   * Cómputo del Coeficiente de Variación (CV) por provincia y terminal de destino.  
   * Construcción de matrices de concentración mensual e interanual.  
4. **Visualización y síntesis:** Elaboración de gráficos de múltiples pequeños, rankings comparativos y mapas de calor para la extracción de hallazgos y visibilizar los ciclos estacionales.

# **Resultados principales**

1. **Patrón estacional bimodal:** Se identificó un patrón estacional marcado en el flujo de pasajeros, con picos de actividad durante los meses de verano (enero-febrero) y un segundo período de mayor movimiento alrededor de julio (invierno).  
2. **Mayor volatilidad por provincia:** Las provincias con marcado perfil turístico receptivo (Río Negro, Santa Cruz, Tierra del Fuego) presentaron los mayores Coeficientes de Variación (CV), indicando una mayor fluctuación mensual de pasajeros a lo largo del año.  
3. **Estabilidad en la demanda:** Provincias como Jujuy, Corrientes, San Juan, San Luis, Mendoza y La Pampa presentaron una menor variabilidad mensual, evidenciando un comportamiento más estable durante el período analizado.  
4. **Persistencia interanual y anomalía 2020:** La distribución mensual presenta cierta persistencia entre los distintos años, con la excepción de 2020, donde la emergencia sanitaria por COVID-19 generó una fuerte alteración de la distribución de pasajeros a partir de abril.

# **Visualizaciones**

* `docs/images/grafico1_evolucion_mensual_provincia.png`: **Evolución Mensual por Provincia** (Múltiplos pequeños que ilustran la trayectoria del flujo de pasajeros por jurisdicción y evidencian los picos de verano/invierno).  
* `docs/images/grafico2_ranking_variabilidad_cv.png`: **Ranking de Variabilidad Estacional** (Gráfico comparativo del Coeficiente de Variación que clasifica las provincias según la volatilidad de su demanda).  
* `docs/images/grafico3_matriz_concentracion_temporal.png`: **Matriz de Concentración Temporal** (Mapa de calor interanual y mensual de la distribución porcentual de pasajeros).

# **Conclusiones**

* **Dualidad de la red aerocomercial:** La infraestructura del país opera bajo dos realidades disímiles: polos turísticos expuestos a valles de demanda pronunciados y nodos urbanos que otorgan sostén y previsibilidad a la red.  
* **Implicancias estratégicas:** Identificar los periodos de valle estacional resulta indispensable para orientar la política pública de promoción turística y para que las aerolíneas reconfiguren sus frecuencias hacia destinos alternativos sin perder eficiencia de mercado.  
* **Líneas futuras de investigación:**  
  * Analizar la relación entre el factor de ocupación (*load factor*) y la rentabilidad en meses de temporada baja.  
  * Evaluar el impacto de la conectividad federal directa (rutas interprovinciales sin pasar por Buenos Aires) en la reducción del Coeficiente de Variación.  
  * Comparar la concentración estacional según el modelo de negocio operado (aerolíneas tradicionales vs. low-cost).

# **Archivos del proyecto**

`README.md`: Documento principal de presentación y documentación del proyecto.

* **`data/`:** Archivos de datos utilizados en el proyecto (`raw/` para datos originales o sin modificaciones; `processed/` para datos preparados o transformados).  
* **`analysis/`:** Archivos relacionados con el análisis realizado por el equipo (notebooks, consultas y recursos técnicos).  
* **`docs/`:** Documentación del proyecto, fichas, definiciones y otros documentos relevantes (`images/` para gráficos del proyecto).  
* **`reports/`:** Informes, presentaciones u otros productos finales del proyecto.

# **Contacto**

Para consultas o información adicional referente a este proyecto, puede contactarse con el equipo a través de:

**Leonardo Elian Nuñez Marin**  
Nunezelianpromo@gmail.com

**William Naufamer**  
williamnaufamer@gmail.com

**Flavia Andrea Matus Aracena**  
flaviamatus@gmail.com

**Facundo Acosta**  
facuacosta120@gmail.com

**Nicole Guerrero Cabrera**  
nicoleguerrero9494@gmail.com  
