# Decodificación de EEG del sistema visual: percepción e imaginería

Código de preprocesamiento y extracción de características para la base de datos de EEG
descrita en el artículo de *MethodsX* «Diseño e implementación de un algoritmo para la
decodificación de señales electroencefalográficas del sistema visual» (manuscrito en
español; traducción al inglés en curso).

**Autores:** Emilia Ramírez-Saverio, José-Antonio Cervantes, Salvador Cervantes,
Rubén Torres Agustín y Francisco Robles (autor por correspondencia).

## Contenido

| Notebook | Descripción |
|---|---|
| `01_PreProcesamiento_EEG_optimizado.ipynb` | Preprocesamiento de los registros `.cnt` (Neuroscan): montaje 10-20 extendido, interpolación de canales malos, referencia mastoidea (A1, A2), filtros 0.5–100 Hz + notch 60 Hz, remuestreo a 250 Hz, reasignación de eventos, ICA (FastICA, 20 componentes), épocas maestras de 9 s (−0.1 a 9.0 s) y exportación a FIF/EDF. |
| `02_Feature_Engine_optimizado.ipynb` | Motor de características: 324 características por ensayo (36 canales × 9), ventanas ERP (P100, P300, tardía), PSD por bandas (theta, alfa, beta, gamma), selección mRMR (top-25), baseline de clasificación (Random Forest, LOSO) y auditoría fisiológica por participante (SNR). |
| `Analisis_Canales_EEG_optimizado.ipynb` | Auditoría de canales: verifica que los 62 archivos `.cnt` tengan los mismos 39 canales (34 EEG + A1 + A2 + EOGL + EOGR + Trigger) y que los 36 canales del pipeline tengan señal real. |

## Datos

**Los datos de EEG no están en este repositorio.** Por el consentimiento informado de
los participantes, los datos se comparten únicamente bajo solicitud razonable al autor
por correspondencia (Dr. Francisco Robles). Para solicitar acceso, escriba al autor
por correspondencia indicando el uso previsto.

Los notebooks esperan la siguiente estructura de carpetas (Google Drive o local):

```
Neuroscan_Data/
├── Datos_Crudo/                  # Archivos .cnt originales
└── Procesado/
    ├── 03_Epocas_Completas_9s/   # Épocas maestras .fif
    └── 05_Resultados_FeatureEngine/
```

## Requisitos

- Python 3.13 (Google Colab) o superior.
- Cada notebook instala sus dependencias en la primera celda (`!pip install -q`
  con versiones fijadas: MNE 1.13.2, NumPy 2.4.6, SciPy 1.16.3, scikit-learn 1.6.1,
  feature-engine 1.9.4, pandas 2.2.3, seaborn 0.13.2, Matplotlib 3.10.0, edfio 0.4.18,
  statsmodels 0.15.0) y verifica las versiones instaladas.

## Notas

- Ventana de percepción: −0.1 a 5.0 s; ventana de imaginería: 5.0 a 9.0 s.
- Filtro analógico de adquisición: pasa-banda 0.5–100 Hz (la banda Gamma, 30–100 Hz,
  se conserva desde el registro).
- La calidad de la señal se reporta por participante mediante el SNR (Parks et al.,
  2016) como métrica descriptiva; ningún participante se excluye del repositorio
  por su SNR. La selección más estricta queda a criterio de cada análisis derivado.
- Financiamiento: beca nacional SECIHTI (CVU 1331508).

## Cita

> Ramírez-Saverio, E., Cervantes, J.-A., Cervantes, S., Torres Agustín, R., &
> Robles, F. *Diseño e implementación de un algoritmo para la decodificación de
> señales electroencefalográficas del sistema visual*. MethodsX (en preparación).
