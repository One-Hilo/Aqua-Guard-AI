````markdown
# Aqua-Guard-AI 🏊‍♂️🤖  
**Detección inteligente de presencia en piscina (dentro/fuera) con visión artificial**

Aqua-Guard-AI es una aplicación basada en **visión artificial** que detecta **personas** en imágenes o vídeo y determina si se encuentran **dentro o fuera de una piscina** usando:
- **YOLO (Ultralytics)** para detección de personas.
- **Lógica de zona (polígono)** para definir el área exacta de la piscina.
- (Opcional) Tracking para estabilidad en vídeo y alertas.

> Objetivo: monitorización y seguridad en entornos acuáticos (piscinas privadas, comunitarias, instalaciones deportivas, etc.).

---

## ✨ Características

- ✅ Detección de **personas** en tiempo real (o por lotes).
- ✅ Clasificación **Dentro / Fuera** según una **zona de piscina** definida.
- ✅ Compatible con **vídeo**, **webcam** o **carpetas de imágenes**.
- ✅ Fácil de calibrar: defines la piscina con un polígono (una sola vez si la cámara es fija).
- ✅ Exporta resultados (opcional): logs/CSV o eventos de alerta.

---

## 🧠 Cómo funciona

1) YOLO detecta objetos (nos interesa **person**).  
2) Definimos la piscina como un **polígono** (coordenadas en píxeles).  
3) Para cada persona, comprobamos si el **centro del bbox** está dentro del polígono.  
4) Resultado:
- **IN_POOL** → centro dentro de la zona
- **OUT_POOL** → centro fuera de la zona

---

## 📦 Requisitos

- Python **3.10 / 3.11** recomendado  
- Windows / Linux / macOS
- Dependencias principales:
  - `ultralytics`
  - `opencv-python`
  - `numpy`

---

## ⚙️ Instalación

```bash
git clone https://github.com/One-Hilo/Aqua-Guard-AI.git
cd Aqua-Guard-AI

python -m venv venv
# Windows:
venv\Scripts\activate
# Linux/macOS:
# source venv/bin/activate

pip install -U pip
pip install ultralytics opencv-python numpy
````

> Si quieres una instalación exacta por requirements, crea tu `requirements.txt` cuando tengas el pipeline cerrado.

---

## 🚀 Uso

### 1) Detección en vídeo (recomendado para pruebas)

Ejemplo (simple): ejecuta el script principal (cuando lo tengas en `src/`):

```bash
python src/main_video.py --source "ruta/al/video.mp4"
```

### 2) Procesar una carpeta de imágenes

```bash
python src/main_folder.py --input "ruta/a/carpeta" --output "ruta/a/output"
```

### 3) Webcam / cámara IP

```bash
python src/main_video.py --source 0
```

---

## 🗺️ Configuración de la zona de piscina

La zona se define como un conjunto de puntos (polígono). Ejemplo:

```python
POOL_POLYGON = [
    (120, 220),
    (520, 210),
    (610, 470),
    (80,  490)
]
```

**Recomendación**: si tu cámara es fija, define esta zona una sola vez y guárdala en un `config.json` o `config.yaml`.

---

## 📁 Estructura sugerida del proyecto

```text
Aqua-Guard-AI/
├─ src/
│  ├─ main_video.py          # detección en vídeo / webcam
│  ├─ main_folder.py         # detección por lotes en carpeta
│  ├─ zone.py                # lógica del polígono + punto dentro/fuera
│  ├─ utils.py               # helpers (I/O, logs, etc.)
│
├─ assets/                   # imágenes ejemplo
├─ output/                   # resultados
├─ README.md
└─ requirements.txt
```

---

## ✅ Roadmap

* [ ] Script para marcar la piscina con clicks y guardar `config.json`
* [ ] Tracking (ByteTrack / SORT) para reducir falsos positivos en vídeo
* [ ] Alertas por evento (persona entra en piscina, permanencia, etc.)
* [ ] Modo nocturno / baja luz (mejoras con ajuste de imagen o modelo)
* [ ] Exportación de eventos (CSV / JSON / webhook)

---

## 🛡️ Aviso de uso

Este proyecto es una herramienta de ayuda. No sustituye la supervisión humana en situaciones de riesgo.

---

## 🙏 Créditos

* Detección basada en **Ultralytics YOLO**: [https://github.com/ultralytics/ultralytics](https://github.com/ultralytics/ultralytics)
* Gracias a la comunidad open-source por modelos, ejemplos y herramientas.

---

## 📄 Licencia

Este repositorio hereda condiciones de las dependencias utilizadas.
Si vas a usarlo en producto comercial, revisa licencias (especialmente Ultralytics/AGPL vs Enterprise).

---

## 📬 Contacto

Autor: **One-Hilo**
