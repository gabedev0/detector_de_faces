# Detector de Faces e Olhos em Tempo Real

Um sistema de detecção facial e ocular em tempo real usando OpenCV e classificadores Haar Cascade. O programa captura vídeo da webcam e identifica faces e olhos, desenhando retângulos ao redor das detecções.

## 📋 Descrição

Este projeto implementa um detector que:
- Captura vídeo em tempo real da webcam
- Detecta faces humanas usando classificadores Haar Cascade
- Identifica olhos dentro das faces detectadas
- Desenha retângulos coloridos ao redor das detecções
- Exibe as coordenadas do centro das faces detectadas
- Permite controle via teclado para sair do programa

## 🔧 Requisitos

### Dependências
```bash
pip install opencv-python
```

### Arquivos Necessários
O programa requer os classificadores Haar Cascade da OpenCV:
- `haarcascade_frontalface_default.xml`
- `haarcascade_eye.xml`

Estes arquivos podem ser obtidos do [repositório oficial do OpenCV](https://github.com/opencv/opencv/tree/master/data/haarcascades).

## 📁 Estrutura do Projeto

```
├── detector.py                           # Código principal
├── haarcascade_frontalface_default.xml   # Classificador para faces
└── haarcascade_eye.xml                   # Classificador para olhos
```

## 🚀 Como Usar

1. Certifique-se de ter uma webcam conectada
2. Baixe os arquivos XML dos classificadores Haar
3. Coloque os arquivos no mesmo diretório do script
4. Execute o programa:
   ```bash
   python detector.py
   ```
5. Para sair, pressione a tecla **ESC**

## ⚙️ Funcionamento

### Pipeline de Detecção

1. **Captura de Vídeo**: Lê frames da webcam
2. **Espelhamento**: Inverte horizontalmente para efeito espelho
3. **Conversão**: RGB → Escala de cinza para processamento
4. **Detecção de Faces**: Usa classificador Haar para localizar faces
5. **Detecção de Olhos**: Busca olhos apenas dentro das regiões faciais
6. **Visualização**: Desenha retângulos e redimensiona o vídeo
7. **Controle**: Monitora teclas para encerrar o programa

### Parâmetros de Configuração

```python
largura = 420          # Largura da janela de exibição
altura = 360           # Altura da janela de exibição
scaleFactor = 1.3      # Fator de redução da imagem
minNeighbors = 5       # Número mínimo de vizinhos para validar detecção
```

## 🎯 Recursos

### Detecções Visuais
- **Faces**: Retângulos azuis (255, 0, 0)
- **Olhos**: Retângulos vermelhos (0, 0, 255)
- **Coordenadas**: Impressas no terminal (centro das faces)

### Controles
- **ESC**: Encerra o programa
- **Espelhamento automático**: Vídeo invertido horizontalmente
- **Redimensionamento**: Janela fixa de 420x360 pixels

## 📊 Saída do Programa

### Console
```
210 180  # Coordenadas x,y do centro da face detectada
195 165
...
```

### Interface Visual
- Janela "Reconhecimento Facial" com vídeo em tempo real
- Retângulos coloridos indicando detecções
- Resolução redimensionada para melhor visualização

## 🔧 Personalização

### Ajustar Sensibilidade
```python
# Mais sensível (mais detecções, mais falsos positivos)
faces = face_cascade.detectMultiScale(cinza, 1.1, 3)

# Menos sensível (menos detecções, mais precisão)
faces = face_cascade.detectMultiScale(cinza, 1.5, 7)
```

### Mudar Cores dos Retângulos
```python
# Face em verde
cv2.rectangle(video, (x, y), (x + w, y + h), (0, 255, 0), 2)

# Olhos em amarelo
cv2.rectangle(roi_color, (ex, ey), (ex + ew, ey + eh), (0, 255, 255), 2)
```

### Alterar Resolução
```python
largura = 640   # HD
altura = 480
```

## 🎓 Conceitos Demonstrados

- **Haar Cascades**: Classificadores para detecção de objetos
- **ROI (Region of Interest)**: Processamento em regiões específicas
- **Processamento de Vídeo**: Captura e manipulação em tempo real
- **OpenCV**: Biblioteca de visão computacional
- **Detecção Hierárquica**: Buscar olhos apenas dentro de faces

## ⚡ Performance

### Otimizações Implementadas
- Conversão para escala de cinza (processamento mais rápido)
- Redimensionamento da janela (menos pixels para renderizar)
- ROI para olhos (busca apenas dentro das faces)

### Requisitos do Sistema
- Webcam funcional
- Python 3.6+
- Processador moderno para tempo real fluido

## 🐛 Solução de Problemas

### Problemas Comuns

**Erro: Arquivo XML não encontrado**
```
Solução: Baixar os arquivos haarcascade do repositório OpenCV
```

**Webcam não detectada**
```python
# Tentar diferentes índices de câmera
cap = cv2.VideoCapture(1)  # ou 2, 3, etc.
```

**Performance lenta**
```python
# Reduzir resolução de captura
cap.set(cv2.CAP_PROP_FRAME_WIDTH, 320)
cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 240)
```

## 🚀 Possíveis Melhorias

- Reconhecimento facial (identificação de pessoas específicas)
- Detecção de emoções
- Salvar imagens das detecções
- Interface gráfica com botões
- Suporte a múltiplas câmeras
- Detecção de outras características faciais
- Integração com bases de dados

## 📝 Limitações

- Funciona melhor com boa iluminação
- Sensível ao ângulo da face
- Classificadores Haar são menos precisos que métodos modernos (deep learning)
- Não identifica pessoas específicas, apenas detecta presença
