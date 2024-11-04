# Configuración de GPU NVIDIA para Deep Learning

## Paso 1: Controlador de video NVIDIA

Deberías instalar la última versión del controlador para tu GPU. Puedes descargar los controladores aquí:
 - [Descargar controlador de GPU NVIDIA](https://www.nvidia.com/Download/index.aspx)

## Paso 2: Visual Studio C++

Necesitarás Visual Studio con C++ instalado. De forma predeterminada, C++ no se instala con Visual Studio, así que asegúrate de seleccionar todas las opciones relacionadas con C++.
 - [Visual Studio Edición Comunitaria](https://visualstudio.microsoft.com/vs/community/)

## Paso 3: Anaconda/Miniconda

Necesitarás Anaconda para instalar todos los paquetes de deep learning.
 - [Descargar Anaconda](https://www.anaconda.com/download/success)

## Paso 4: CUDA Toolkit

 - [Descargar CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit-archive)

## Paso 5: cuDNN

 - [Descargar cuDNN](https://developer.nvidia.com/rdp/cudnn-archive)

## Paso 6: Instalar PyTorch

 - [Instalar PyTorch](https://pytorch.org/get-started/locally/)

## Finalmente, ejecuta el siguiente script para probar tu GPU

```python
import torch

print("Número de GPU: ", torch.cuda.device_count())
print("Nombre de GPU: ", torch.cuda.get_device_name())

device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
print('Usando el dispositivo:', device)