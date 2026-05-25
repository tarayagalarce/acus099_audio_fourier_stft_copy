# Pistas de audio, Transformada de Fourier y Espectrogramas

Material docente para el curso **ACUS099 - Procesamiento Digital de Señales** con Python.

Este repositorio contiene cuadernillos Jupyter diseñados para introducir a las y los estudiantes al procesamiento de señales de audio usando pistas musicales como ejemplo. Las actividades avanzan de manera progresiva: primero se trabaja con la visualización temporal y mezcla de señales, luego con la Transformada Discreta de Fourier, la FFT, la Transformada de Fourier de Tiempo Corto y los espectrogramas.

## Objetivos de la clase

Los objetivos principales de este material son:

1. Cargar pistas de audio en Python.
2. Visualizar formas de onda en el dominio del tiempo.
3. Comprender una señal de audio como un vector de muestras discretas.
4. Mezclar varias pistas mediante suma muestra a muestra.
5. Resolver el problema de pistas con distinta duración mediante recorte y relleno con ceros.
6. Aplicar la Transformada Discreta de Fourier usando `np.fft.fft`.
7. Conectar la expresión matemática

   ```text
   X = W x
   ```

   con el algoritmo práctico de la FFT.
8. Introducir la Transformada de Fourier de Tiempo Corto, STFT.
9. Visualizar espectrogramas como representaciones tiempo-frecuencia.
10. Explorar el compromiso entre resolución temporal y resolución frecuencial.

## Estructura del repositorio

```text
audio-tracks-fourier-stft/
│
├── data/
│   └── audio_tracks/
│       └── .gitkeep
│
├── notebooks/
│   ├── 01_audio_tracks_fourier.ipynb
│   └── 02_stft_spectrogram_intro.ipynb
│
├── outputs/
│   ├── audio/
│   └── figures/
│
├── scripts/
│   └── check_audio_files.py
│
├── README.md
├── requirements.txt
└── .gitignore
```

## Cuadernillos

### 01_audio_tracks_fourier.ipynb

Este cuadernillo introduce el flujo básico de trabajo con audio:

- carga de archivos de audio;
- reproducción de audio dentro de Jupyter usando `IPython.display.Audio`;
- visualización de formas de onda;
- cálculo de la duración de cada pista;
- análisis del problema de pistas con distinta longitud;
- creación de mezclas de audio;
- normalización y guardado de mezclas;
- cálculo de la FFT de pistas individuales y mezclas;
- comparación de espectros de magnitud;
- introducción a la PSD y observación de envolventes espectrales más suaves.

### 02_stft_spectrogram_intro.ipynb

Este cuadernillo introduce el análisis tiempo-frecuencia:

- revisión de la limitación de una FFT global;
- explicación de la idea de ventana temporal móvil;
- cálculo de la Short-Time Fourier Transform, STFT;
- visualización de espectrogramas;
- comparación de espectrogramas entre distintas pistas;
- exploración del efecto de `n_fft` y `hop_length`;
- mejora de la resolución en bajas frecuencias para la pista de bajo.

## Nota importante sobre los archivos de audio

Los archivos de audio **no están incluidos** en este repositorio.

En la clase se pueden usar pistas locales como:

```text
bass.wav
drums.wav
piano.wav
voice1.wav
voice2.wav
```

Estos archivos deben ubicarse localmente en:

```text
data/audio_tracks/
```

Los archivos de audio están excluidos intencionalmente del control de versiones mediante `.gitignore`.

Por favor, no subir material de audio con derechos de autor a GitHub.

## Archivos de audio esperados localmente

Los cuadernillos esperan encontrar los siguientes archivos:

```text
data/audio_tracks/bass.wav
data/audio_tracks/drums.wav
data/audio_tracks/piano.wav
data/audio_tracks/voice1.wav
data/audio_tracks/voice2.wav
```

Si se desean usar otros nombres de archivo, se debe modificar el diccionario `track_files` dentro de los cuadernillos.

## Ambiente de trabajo

El ambiente del curso es:

```bash
conda activate acus099_2026
```

Si faltan paquetes, se pueden instalar con:

```bash
pip install -r requirements.txt
```

Un archivo `requirements.txt` mínimo puede contener:

```text
numpy
matplotlib
scipy
soundfile
librosa
jupyter
ipython
```

## Cómo ejecutar los cuadernillos

Desde la raíz del proyecto, abrir VS Code:

```bash
code .
```

Luego abrir los cuadernillos dentro de la carpeta `notebooks/`.

También se puede ejecutar:

```bash
jupyter notebook
```

y abrir los cuadernillos desde el navegador.

## Revisión segura antes de subir a GitHub

Antes de hacer `push` a GitHub, verificar que los archivos de audio estén siendo ignorados:

```bash
git check-ignore -v data/audio_tracks/bass.wav
git check-ignore -v data/audio_tracks/drums.wav
git check-ignore -v data/audio_tracks/piano.wav
git check-ignore -v data/audio_tracks/voice1.wav
git check-ignore -v data/audio_tracks/voice2.wav
```

Luego revisar el estado del repositorio:

```bash
git status
```

Asegurarse de que no aparezcan archivos `.wav`, `.mp3`, `.flac` u otros archivos de audio en la lista de archivos que serán incluidos en el commit.

## Flujo sugerido para estudiantes

1. Clonar el repositorio.
2. Activar el ambiente del curso.
3. Colocar los archivos de audio localmente en `data/audio_tracks/`.
4. Abrir el primer cuadernillo y ejecutarlo celda por celda.
5. Continuar con el segundo cuadernillo para explorar espectrogramas.
6. Modificar parámetros como `n_fft`, `hop_length` y los límites de frecuencia.
7. Comparar el comportamiento del bajo, batería, piano y voces.

## Conceptos principales

### Señal en el dominio del tiempo

Una señal de audio puede representarse como una secuencia discreta:

```text
x[n]
```

donde `n` es el índice de muestra.

### Mezcla de audio

Mezclar pistas significa sumar señales muestra a muestra:

```text
y[n] = x1[n] + x2[n] + x3[n] + ...
```

Si las pistas tienen distinta longitud, primero deben recortarse o rellenarse con ceros.

### DFT y FFT

La DFT puede escribirse matemáticamente como:

```text
X = W x
```

donde:

- `x` es la señal en el dominio del tiempo;
- `W` es la matriz de Fourier;
- `X` es la representación de la señal en el dominio de la frecuencia.

En la práctica usamos:

```python
X = np.fft.fft(x)
```

porque la FFT calcula el mismo resultado de forma mucho más eficiente.

### STFT y espectrograma

La STFT aplica la FFT sobre ventanas cortas y superpuestas de la señal.

Un espectrograma muestra cómo cambia el contenido frecuencial en el tiempo:

- eje horizontal: tiempo;
- eje vertical: frecuencia;
- color: magnitud o energía.

## Nota docente

Estos materiales están pensados para estudiantes que todavía están desarrollando habilidades de programación. Por eso los cuadernillos usan código explícito y legible, con explicaciones intermedias y visualizaciones.

El objetivo no es solamente obtener resultados, sino comprender cada paso computacional.
