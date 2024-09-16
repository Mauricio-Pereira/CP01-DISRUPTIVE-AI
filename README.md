### README

# Detecção e Segmentação de Objetos em Vídeos

## Integrantes
- Maurício Vieira Pereira - RM553748
- Yago Lucas Golçalves da Silva - RM553013

## Descrição do Projeto
Este projeto utiliza o modelo YOLOv8 para realizar a detecção e segmentação de objetos em vídeos. O modelo foi treinado com o dataset COCO e possui 80 classes de objetos. A comparação é feita entre os modelos YOLOv8n e YOLOv8m, utilizando pesos pré-treinados.

## Estrutura do Projeto
- `VIDEO-DETECTION.ipynb`: Notebook principal contendo o código para detecção e segmentação de objetos.
- `IMAGE-DETECTION.ipynb`: Notebook contendo o código para detecção e segmentação de objetos em imagens.
- `Image Detection/images/`: Diretório contendo as imagens de entrada.
- `Image Detection/runs/`: Diretório onde os resultados das predições são salvos.
- `Video Detection/videos/`: Diretório contendo os vídeos de entrada.
- `Video Detection/runs/`: Diretório onde os resultados das predições são salvos.

## Instalação
Para instalar as bibliotecas necessárias, execute os seguintes comandos:

```bash
!pip install ultralytics
!pip install imageio
!pip install imageio[ffmpeg]
!pip install imageio-ffmpeg
```

**Observação:** Os comandos de instalação `!pip` podem variar dependendo de onde você está rodando a aplicação (e.g., Jupyter Notebook, VSCode, terminal).


##Importação de Bibliotecas
Para importar as bibliotecas necessárias, execute os seguintes comandos:

```python
import ultralytics
import cv2
import matplotlib.pyplot as plt
import os
from PIL import Image
```

## Uso
### Detecção de Objetos
Para realizar a detecção de objetos (tanto em imagens quanto em vídeos), execute os seguintes comandos:

```bash
!yolo task=detect mode=predict model=yolov8n.pt conf=0.75 source='images/image1.jpg' save=False
!yolo task=detect mode=predict model=yolov8m.pt conf=0.75 source='images/image1.jpg' save=False
!yolo task=detect mode=predict model=yolov8n.pt conf=0.75 source='videos/video1.mp4' save=False
!yolo task=detect mode=predict model=yolov8m.pt conf=0.75 source='videos/video1.mp4' save=False
```

### Segmentação de Objetos
Para realizar a segmentação de objetos (tanto em imagens quanto em vídeos), execute os seguintes comandos:

```bash
!yolo task=segment mode=predict model=yolov8n-seg.pt conf=0.75 source='images/image2.jpg' save=False
!yolo task=segment mode=predict model=yolov8m-seg.pt conf=0.75 source='images/image2.jpg' save=False
!yolo task=segment mode=predict model=yolov8n-seg.pt conf=0.75 source='videos/video2.mp4' save=False
!yolo task=segment mode=predict model=yolov8m-seg.pt conf=0.75 source='videos/video2.mp4' save=False
```
### Exibição das Imagens
#### VSCode
Para exibir as imagens no VSCode, execute o seguinte nódulo (lembrando que esse é apenas um exemplo, você pode alterar o caminho da imagem conforme necessário):

```python
resultado = cv2.imread('runs\detect\predict2\image.jpg')
plt.imshow(cv2.cvtColor(resultado, cv2.COLOR_BGR2RGB))
```


### Exibição dos Vídeos
#### VSCode
Para exibir os vídeos no VSCode, execute os seguintes nódulos (lembrando que esse é apenas um exemplo, você pode alterar o caminho do vídeo conforme necessário):

```python
# Nódulo 1
import imageio
from tkinter import Tk, Label
from PIL import Image, ImageTk
import threading

def exibir_video_vscode(video_caminho):
    video = imageio.get_reader(video_caminho, 'ffmpeg')
    root = Tk()
    lbl = Label(root)
    lbl.pack()

    def stream():
        try:
            for frame in video.iter_data():
                img = ImageTk.PhotoImage(Image.fromarray(frame))
                lbl.config(image=img)
                lbl.image = img
                root.update()
        except RuntimeError:
            pass

    threading.Thread(target=stream).start()
    root.mainloop()

# Nódulo 2
exibir_video_vscode('runs/detect/predict/video1.mp4')

# Nódulo 3
exibir_video_vscode('runs/detect/predict2/video1.mp4')
```

#### Jupyter Notebook
Para exibir os vídeos no Jupyter Notebook, execute os seguintes nódulos (lembrando que esse é apenas um exemplo, você pode alterar o caminho do vídeo conforme necessário):

```python
# Nódulo 1
def exibir_video_jupyter(video_caminho):
    from IPython.display import HTML
    from base64 import b64encode
    mp4 = open(video_caminho, 'rb').read()
    data_url = "data:video/mp4;base64," + b64encode(mp4).decode()
    return HTML("""
    <video width=500 controls>
      <source src="%s" type="video/mp4">
    </video>
    """ % data_url)

# Nódulo 2
exibir_video_jupyter('runs/detect/predict/video1.mp4')

# Nódulo 3
exibir_video_jupyter('runs/detect/predict2/video1.mp4')
```

**Observação:** Os caminhos para a localização dos arquivos podem ser interpretados de forma diferente dependendo do ambiente em que você está rodando a aplicação.

## Resultados Obtidos
### Detecção
#### Imagens
O modelo YOLOv8m obteve um resultado superior ao modelo YOLOv8n, com uma melhor detecção dos objetos presentes na imagem. O modelo YOLOv8n detectou apenas 2 objetos (pessoas e laptops), enquanto o modelo YOLOv8m detectou 4 objetos (pessoas, laptops, canecas e livros).
#### Vídeos
O modelo YOLOv8m também obteve um resultado superior ao modelo YOLOv8n na detecção de objetos em vídeos. O modelo YOLOv8n detectou 6 objetos (pessoas, ônibus, carro, mala, semáforo e bolsa de mão), enquanto o modelo YOLOv8m detectou 7 objetos (pessoas, ônibus, carro, mala, semáforo, bolsa de mão e mochila).

### Segmentação
#### Imagens
O modelo YOLOv8m obteve um resultado superior ao modelo YOLOv8n, com uma melhor segmentação dos objetos presentes na imagem. O modelo YOLOv8n detectou apenas 2 objetos (pessoas e laptops), enquanto o modelo YOLOv8m detectou 4 objetos (pessoas, laptops, canecas e livros).
#### Vídeos
O modelo YOLOv8m também obteve um resultado superior ao modelo YOLOv8n na segmentação de objetos em vídeos. O modelo YOLOv8n detectou 6 objetos (pessoas, ônibus, carro, mala, semáforo e bolsa de mão), enquanto o modelo YOLOv8m detectou 7 objetos (pessoas, ônibus, carro, mala, semáforo, bolsa de mão e mochila).  

**Obs.:** A opção `save=True` foi alterada para `save=False` para que a imagem não seja salva no diretório, já que o código já foi executado e as imagens estão salvas no diretório.