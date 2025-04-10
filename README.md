# Colab-Video-Editor
This PROJECT IS PROVIDED "AS IS", it may have codign problems.

## Código para cortar un video en Google Colab usando moviepy.

```python
# Instalamos las librerías necesarias
!pip install -q pytube moviepy

import os
from pytube import YouTube
from moviepy.editor import VideoFileClip

def descargar_y_recortar_video(url, tiempo_inicio, tiempo_fin, nombre_salida=None):
    """
    Descarga un video de YouTube y lo recorta según los tiempos indicados.
    
    Parámetros:
        url (str): URL del video de YouTube
        tiempo_inicio (float): Tiempo de inicio en segundos
        tiempo_fin (float): Tiempo de fin en segundos
        nombre_salida (str, opcional): Nombre del archivo de salida
    
    Retorna:
        str: Ruta del archivo recortado
    """
    # Crear objeto YouTube
    yt = YouTube(url)
    
    # Obtener la mejor resolución disponible
    video = yt.streams.filter(progressive=True, file_extension="mp4").order_by("resolution").desc().first()
    
    # Nombre del video descargado
    if not nombre_salida:
        nombre_salida = yt.title.replace(" ", "_")[:50]
    
    archivo_descargado = video.download(filename=f"original_{nombre_salida}.mp4")
    print(f"Video descargado: {archivo_descargado}")
    
    # Recortar el video
    archivo_recortado = f"recortado_{nombre_salida}.mp4"
    clip = VideoFileClip(archivo_descargado)
    clip_recortado = clip.subclip(tiempo_inicio, tiempo_fin)
    clip_recortado.write_videofile(archivo_recortado, codec="libx264", audio_codec="aac")
    
    # Cerramos los clips para liberar memoria
    clip.close()
    clip_recortado.close()
    
    # Opcional: borrar el video original para liberar espacio
    os.remove(archivo_descargado)
    
    print(f"Video recortado guardado en: {archivo_recortado}")
    return archivo_recortado

# Ejemplo de uso
url_video = "https://www.youtube.com/watch?v=dQw4w9WgXcQ"  # Cambia esto por tu URL
tiempo_inicio = 30  # Segundos
tiempo_fin = 60     # Segundos
nombre_salida = "mi_video_recortado"

video_recortado = descargar_y_recortar_video(url_video, tiempo_inicio, tiempo_fin, nombre_salida)

```

Para usarlo:

- Copia el código a una celda en Google Colab
- Modifica la URL, los tiempos de inicio y fin, y opcionalmente el nombre del archivo de salida
- Ejecuta la celda

El código automáticamente:

- Instala las librerías necesarias
- Descarga el video en la mejor calidad disponible
- Recorta el video según los tiempos especificados
- Elimina el archivo original para ahorrar espacio
- Devuelve la ruta al archivo recortado.
