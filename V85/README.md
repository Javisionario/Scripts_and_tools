# Interpretación de velocidades V₈₅ con datos INRIX  
Procesamiento, cálculo de V₈₅ ponderada y análisis horario por tramos

Este script permite procesar datos de velocidad de **INRIX**, limpiar y homogeneizar el campo temporal, filtrar por **periodos definidos por el usuario**, calcular la **V₈₅ ponderada por tramo** y generar **gráficos horarios** con percentiles (P5–P95) y curvas V₈₅.  

También admite la inclusión de **velocidades límite** y permite definir la granularidad temporal para el análisis (15 min, 30 min, 60 min, etc.).

La **V₈₅** mostrada por este script **no es el percentil 85 global** del tramo.  
En su lugar, se calcula una **V₈₅ ponderada por la longitud de cada segmento**.

Esto resulta más representativo en tramos donde los segmentos tienen longitudes muy dispares y se aproxima mejor al comportamiento real del corredor.

### 📐 Fórmula empleada

Para cada tramo:

$$
V_{85} = \frac{\sum L}{\sum \left( \frac{L}{V_{85,\text{segmento}}} \right)}
$$

Donde:

- $$\ L \$$ es la longitud del segmento.  
- $$\ V_{85,\text{segmento}} \$$ es el percentil 85 de velocidad calculado para cada segmento.

Se trata de una **media armónica ponderada por longitud**, adecuada para estimar velocidades representativas del tiempo de recorrido en tramos largos.

---

## ⚙️ Parámetros  

El script solicita al usuario:

- **Ruta del archivo** `data.csv`  
- **Periodos de análisis** (formato `MM/DD/YYYY - MM/DD/YYYY`)  (opcional)
- **Granularidad horaria** (`15min` por defecto)  
- **Velocidades límite** (opcional):  
  - Comunes para todos los tramos, o  
  - Específicas por tramo  

Columnas necesarias en los datos:
- `Speed(km/hour)`
- `Segment ID`
- `Corridor/Region Name`
- `Date Time`

Columnas requeridas en metadata:
- `Segment ID`
- `Segment Length(Kilometers)`

---

## 🔧 Metodología  
1. **Carga y validación** de `data.csv` y `metadata.csv`.  
2. **Normalización del campo Date Time**, eliminando zonas horarias y resolviendo formatos inconsistentes.  
3. **Entrada de periodos de estudio** definidos manualmente o uso automático del rango completo del dataset.  
4. **Cálculo de V₈₅ ponderada por tramo**:
   - Obtención de la V₈₅ de cada segmento.
   - Incorporación de la longitud segmentaria desde `metadata.csv`.
   - Promedio ponderado (media armónica) según longitud del segmento.
5. **Agrupación horaria** según la granularidad seleccionada.  
6. **Cálculo de percentiles horarios** (P5, V85, P95) por tramo y periodo.  
7. **Generación de gráficos** comparativos e individuales:
   - Percentiles horarios (P5–P95)
   - Curva V₈₅
   - Opcional: velocidad límite

---

## 📌 Casos de uso  
- Análisis comparativo antes/después de una actuación vial.  
- Evaluación de la consistencia entre la velocidad límite y velocidades reales.  
- Identificación de tramos con velocidades excesivas o muy variables.  
- Apoyo a estudios de seguridad vial y movilidad.  
- Generación de gráficos e informes técnicos.

---

## ⚠️ Limitaciones  

- Los datos están limitados por la **segmentación espacial propia de INRIX**, y el usuario debe adaptarse a ella.
- Se desconoce el **tamaño de la muestra real** utilizada por INRIX para generar cada observación; no es posible determinar cuántos vehículos contribuyen a cada estimación de velocidad.
- No se dispone de información sobre el **porcentaje de vehículos pesados**, su distribución temporal ni su posible impacto en las velocidades registradas.
- INRIX no facilita detalles sobre la **fuente exacta de los datos** (mezcla de GPS, dispositivos móviles, flotas, sensores…), lo que puede introducir sesgos temporales o espaciales.
- Los periodos sin datos se omiten automáticamente, lo que puede generar **desequilibrios entre tramos o periodos**.
- Tras la limpieza del campo `Date Time`, la hora se interpreta siempre como **hora local**, lo cual puede resultar problemático si los datos originales mezclan distintas zonas horarias.
- La estabilidad de los percentiles y de la **V₈₅ ponderada** puede verse afectada en tramos con pocos datos, segmentos muy cortos o periodos con baja disponibilidad.

---

## 📄 Licencia  
Este proyecto se distribuye bajo licencia **GNU General Public License v3.0**.  
Puedes usarlo, modificarlo y redistribuirlo libremente manteniendo el aviso de copyright.

---
