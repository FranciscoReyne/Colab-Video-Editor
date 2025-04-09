# Colab-Video-Editor
Código para cortar un video en Google Colab usando moviepy.


----

```python

# Instalar moviepy
!pip install moviepy

# Importar librerías necesarias
from moviepy.editor import VideoFileClip
from google.colab import files

# Subir el archivo de video
uploaded = files.upload()

# Obtener el nombre del archivo subido
video_filename = list(uploaded.keys())[0]

# Cargar el video
video = VideoFileClip(video_filename)

# Definir los segundos de inicio y fin del recorte
inicio = 10  # Segundo de inicio
fin = 20  # Segundo de fin

# Recortar el video
video_recortado = video.subclip(inicio, fin)

# Guardar el video recortado
output_filename = "video_recortado.mp4"
video_recortado.write_videofile(output_filename)

# Descargar el video recortado
files.download(output_filename)
```

---

Si solo quieres visualizar un video de YouTube dentro de Google Colab sin descargarlo, puedes usar IPython.display junto con un iframe de YouTube. Aquí tienes el código:


```python

from IPython.display import HTML

# Reemplaza con el enlace de tu video de YouTube
youtube_url = "https://www.youtube.com/embed/TU_VIDEO_ID"

# Mostrar el video en Colab
HTML(f'<iframe width="800" height="450" src="{youtube_url}" frameborder="0" allowfullscreen></iframe>')

```

---



