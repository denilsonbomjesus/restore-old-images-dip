# 🖼️ Restauração de Imagens Antigas com Processamento Digital de Imagens

Projeto desenvolvido para o desafio final da disciplina de **Processamento Digital de Imagens (PDI)**, com foco na restauração de fotografias antigas degradadas utilizando técnicas clássicas de visão computacional e processamento de imagens.

## 📋 Sobre o Projeto

Fotografias antigas frequentemente apresentam diversos tipos de degradação, como:

* Ruído impulsivo (salt and pepper)
* Desfoque (blur)
* Baixo contraste
* Desbotamento de cores
* Rasgos e danos físicos
* Distorções de perspectiva
* Artefatos provenientes da digitalização

Este projeto implementa uma pipeline modular capaz de restaurar imagens antigas através da combinação de diferentes técnicas de processamento digital.

---

## 🎯 Objetivos

* Melhorar a qualidade visual de fotografias antigas.
* Reduzir ruídos e artefatos.
* Recuperar detalhes perdidos.
* Corrigir cores e contraste.
* Restaurar regiões danificadas.
* Corrigir deformações geométricas.

---

## 🏗️ Pipeline de Restauração

A pipeline principal é composta pelas seguintes etapas:

```text
Imagem Original
       │
       ▼
Pré-processamento
       │
       ▼
Remoção de Ruído e Artefatos
       │
       ▼
Redução de Blur (Deconvolução Wiener)
       │
       ▼
Realce de Detalhes
       │
       ▼
Correção de Cor
       │
       ▼
Pós-processamento
       │
       ▼
Imagem Restaurada
```

---

## 🔧 Técnicas Utilizadas

### 1. Pré-processamento

* Normalização de intensidade
* Redimensionamento
* Alinhamento automático (opcional)
* Conversão para formato adequado

### 2. Remoção de Ruídos e Artefatos

* Filtro Bilateral
* Filtro Mediano
* Inpainting (Telea)
* Filtragem no domínio da frequência (FFT)

### 3. Redução de Desfoque

Utilização da técnica de:

* Deconvolução de Wiener

Com suporte para PSFs:

* Circular (Gaussian Blur)
* Linear (Motion Blur)

### 4. Realce de Detalhes

* CLAHE (Contrast Limited Adaptive Histogram Equalization)
* Unsharp Masking
* Realce de bordas utilizando Sobel

### 5. Correção de Cor

* Balanceamento de branco
* Ajuste de saturação
* Ajuste de contraste

### 6. Pós-processamento

* Upscaling
* Denoising utilizando Non-Local Means

---

## 🛠️ Tecnologias Utilizadas

* Python 3
* OpenCV
* NumPy
* Scikit-Image
* SciPy
* Matplotlib

---

## 📦 Instalação

Clone o repositório:

```bash
git clone https://github.com/denilsonbomjesus/restore-old-images-dip.git
cd restore-old-images-dip
```

Instale as dependências:

```bash
pip install -r requirements.txt
```

Ou manualmente:

```bash
pip install opencv-python numpy matplotlib scipy scikit-image
```

---

## 📂 Dataset

O projeto utiliza o dataset:

**Old Photos Dataset**

Disponível em:

https://www.kaggle.com/datasets/marcinrutecki/old-photos

Download via KaggleHub:

```python
import kagglehub

path = kagglehub.dataset_download(
    "marcinrutecki/old-photos"
)

print(path)
```

---

## 🚀 Como Executar

Defina o caminho da imagem:

```python
img_path = "old_photo_06.jpg"
```

Configure a pipeline desejada:

```python
pipeline = [
    lambda x: preprocess_image(
        x,
        target_size=(1024, None),
        align=False
    ),

    lambda x: remove_noise_artifacts(
        x,
        bilateral_d=9,
        median_k=0,
        inpaint_radius=0,
        fft_threshold=0
    ),

    lambda x: deblur_image(
        x,
        psf_type='circular',
        psf_size=5,
        wiener_balance=0.01
    ),

    lambda x: postprocess_image(
        x,
        upscale_factor=1,
        denoise_sigma=5
    )
]
```

Execute:

```python
restored_img = restore_image(
    img_path,
    pipeline
)
```

O resultado será salvo automaticamente como:

```text
nome_da_imagem_restored.jpg
```

---

## 🔍 Casos de Estudo

Foram realizados experimentos em diversas imagens do dataset:

* k.jpg
* old_photo_06.jpg
* old_photo_07.jpg
* old_photo_08.jpeg
* old_photo_09.jpeg
* old_photo_10.jpg
* old_photo_14.jpg
* old_photo_18.jpg
* old_photo_19.jpg
* old_photo_22.jpg

Algumas imagens exigiram etapas adicionais:

### Correção de Rasgos

Aplicação de:

* Thresholding
* Operações morfológicas
* Inpainting

### Remoção de Ruído Salt & Pepper

Aplicação de:

* Filtro mediano local
* Mistura ponderada entre imagem original e filtrada

### Correção de Perspectiva

Aplicação de:

* Perspective Warping
* Transformação projetiva usando OpenCV

---

## 📊 Resultados

Os resultados demonstraram melhorias significativas em:

* Nitidez
* Contraste
* Redução de ruído
* Recuperação de regiões danificadas
* Correção de distorções geométricas

Cada etapa da pipeline gera visualizações comparativas entre a imagem original e a processada, permitindo análise detalhada dos efeitos de cada técnica.

---

## 📚 Conceitos de PDI Aplicados

* Filtragem espacial
* Filtragem no domínio da frequência
* Transformadas geométricas
* Equalização de histograma
* Operações morfológicas
* Detecção de bordas
* Deconvolução
* Inpainting
* Realce de imagens

---

## 👨‍💻 Autor

Projeto desenvolvido como parte do desafio final da disciplina de **Processamento Digital de Imagens (PDI)**.

---

## 📄 Licença

Este projeto possui finalidade acadêmica e educacional.
