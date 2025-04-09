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
---

# OPCION 2:


```python
!pip install moviepy

from moviepy.editor import VideoFileClip
from google.colab import files
from IPython.display import HTML

# Reemplaza con el enlace de tu video de YouTube

youtube_url = "https://www.youtube.com/embed/TU_VIDEO_ID" # Reemplaza TU_VIDEO_ID con el ID de tu video

# Extrae el ID del video si se proporciona la URL completa
if "youtube.com/watch?v=" in youtube_url:
  youtube_url = youtube_url.split("youtube.com/watch?v=")[1]
  if "&" in youtube_url:
    youtube_url = youtube_url.split("&")[0]
  youtube_url = "https://www.youtube.com/embed/" + youtube_url

HTML(f'<iframe width="800" height="450" src="{youtube_url}" frameborder="0" allowfullscreen></iframe>')

# Mostrar el video en Colab
HTML(f'<iframe width="800" height="450" src="{youtube_url}" frameborder="0" allowfullscreen></iframe>')


```
---



---
```python
# prompt:  #aqui agrega la opcion para guardar el video de youtube en directorio de colab

!pip install pytube

from pytube import YouTube

def download_youtube_video(url, resolution='highest', output_path='/content'):
  """Downloads a YouTube video to the specified directory.

  Args:
    url: The URL of the YouTube video.
    resolution: The desired resolution of the video. Defaults to 'highest'.
                Can be 'highest', 'lowest', or a specific resolution string
                (e.g., '720p').
    output_path: The directory to save the downloaded video. Defaults to /content.
  """
  try:
      yt = YouTube(url)
      print(f"Downloading: {yt.title}")

      if resolution == 'highest':
          stream = yt.streams.get_highest_resolution()
      elif resolution == 'lowest':
          stream = yt.streams.get_lowest_resolution()
      else:
          stream = yt.streams.filter(res=resolution).first()
          if stream is None:
              print(f"Resolution '{resolution}' not found. Downloading highest resolution instead.")
              stream = yt.streams.get_highest_resolution()

      if stream:
          stream.download(output_path=output_path)
          print(f"Download complete. Video saved to: {output_path}")
      else:
          print("No suitable stream found for download.")

  except Exception as e:
      print(f"An error occurred: {e}")

# Example usage:
video_url = "YOUR_YOUTUBE_VIDEO_URL"  # Replace with the actual YouTube video URL.
download_youtube_video(video_url)


# Example usage specifying a resolution:
# download_youtube_video(video_url, resolution='720p')

# Example usage specifying a different output path:
# download_youtube_video(video_url, output_path='/content/my_videos')
```
