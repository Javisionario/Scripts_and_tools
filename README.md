# Engineering Scripts

Colección de **notebooks y utilidades técnicas** para análisis de datos aplicado a transporte, movilidad e ingeniería.

Cada herramienta mantiene su propia documentación y dependencias.

| Herramienta | Descripción |
|---|---|
| [V85](V85/) | Procesamiento de velocidades INRIX, cálculo de V₈₅ ponderada y análisis horario por tramos. |
| [Profile & Slope Plotter](Profile-Slope-Plotter/) | Generación de perfiles longitudinales y gráficas de pendiente a partir de datos tabulares. |

## Uso

Cada carpeta contiene:

- el notebook ejecutable;
- un `README.md` específico;
- un `requirements.txt` con las dependencias necesarias.

Se recomienda utilizar un entorno virtual de Python antes de instalar las dependencias.

```bash
python -m venv .venv
pip install -r <herramienta>/requirements.txt
```

## Historial

Estas herramientas se desarrollaron inicialmente en repositorios independientes. Los repositorios originales pueden conservarse como archivo histórico mientras el desarrollo activo continúa aquí.

## Licencia

El contenido se distribuye bajo **GNU General Public License v3.0 (GPL-3.0)**. Consulta [LICENSE](LICENSE).
