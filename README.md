# 🧠 Tumor Cerebral — Classificação de RM com Deep Learning

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.x-ee4c2c)](https://pytorch.org/)
[![Ultralytics](https://img.shields.io/badge/Ultralytics-YOLO11-00FFFF)](https://github.com/ultralytics/ultralytics)
[![Status](https://img.shields.io/badge/Status-Acadêmico-orange)]()

> Classificação automática de tumores cerebrais em imagens de ressonância magnética (RM) utilizando **YOLO11s-cls** e **EfficientNet-B0**, com validação rigorosa e comparação estatística entre os modelos.

---

## 📌 Sobre o Projeto

Este repositório contém o treinamento, validação e comparação de dois modelos de deep learning para classificação de tumores cerebrais a partir de imagens de ressonância magnética.

**Classes preditas:**
| Classe | Descrição |
|--------|-----------|
| `glioma` | Glioma |
| `meningioma` | Meningioma |
| `notumor` | Sem tumor |
| `pituitary` | Tumor de hipófise |

> ⚠️ **Importante:** Este é um **trabalho acadêmico**. Os modelos **não são dispositivos médicos** e **não devem ser usados para diagnóstico real**.

---

## 🏆 Principais Resultados

| Métrica | EfficientNet-B0 | YOLO11s-cls |
|---------|-----------------|-------------|
| **Acurácia (teste)** | **99,12%** | 97,94% |
| **F1-macro** | **0,991** | 0,979 |
| **AUC-macro** | **0,9999** | 0,9987 |
| **Log-loss** | **0,034** | 0,078 |
| **Erros no teste** | **6** | 14 |
| **Sensibilidade** | **1,000** | 0,992 |
| Parâmetros | 4,0 M | 5,5 M |
| Inferência (CPU) | 136 ms | **77 ms** |

- **EfficientNet-B0** venceu na maioria das métricas de desempenho e generalização.
- **YOLO11s-cls** é mais rápido na CPU.
- Ensemble dos dois modelos alcança **99,3%** de acurácia.

---

## 🗂️ Estrutura do Repositório

```
Tumor_Cerebral/
│
├── Treinamento_CNN/               # Treinamento da EfficientNet-B0
│   ├── Treinamento_CNN.ipynb
│   ├── Tumor-Cerebral-1/          # Dataset (formato pasta)
│   └── runs/                      # Checkpoints e logs
│
├── Treinamento_YOLO/              # Treinamento do YOLO11s-cls
│   ├── Treinamento_YOLO.ipynb
│   ├── Validacao_do_Modelo.ipynb
│   ├── yolo11s-cls.pt             # Pesos finais
│   └── runs/classify/
│
└── Validacoes/                    # Validação completa e comparação
    ├── 01_YOLO11s-cls/            # Validação isolada do YOLO
    ├── 02_EfficientNet-B0/        # Validação isolada da CNN
    ├── 03_Comparacao_YOLO_vs_CNN/ # Comparação lado a lado
    ├── _compartilhado/cache/      # Probabilidades em cache
    └── LEIAME.md                  # Guia detalhado das validações
```

---

## 📊 Dataset

| Item | Valor |
|------|-------|
| **Fonte** | [Roboflow – Tumor Cerebral](https://universe.roboflow.com/pedros-workspace-1w4rz/tumor-cerebral-wuayk) |
| **Licença** | CC BY 4.0 |
| **Total de imagens** | 6.879 (512×512) |
| **Treino** | 4.819 |
| **Validação** | 1.379 |
| **Teste** | 681 |
| **Pré-processamento** | Auto-orientação (sem augmentação no export) |

> 101 imagens do teste (14,8%) possuem quase-duplicatas no treino. As validações incluem análise de **teste limpo** (sem quase-duplicatas).

---

## 🚀 Como Executar

### 1. Pré-requisitos

```bash
# Ambiente recomendado
Python 3.10+
PyTorch 2.x
ultralytics
timm / torchvision
scikit-learn, pandas, matplotlib, seaborn
```

### 2. Treinamento

```bash
# EfficientNet-B0
cd Treinamento_CNN
jupyter notebook Treinamento_CNN.ipynb

# YOLO11s-cls
cd Treinamento_YOLO
jupyter notebook Treinamento_YOLO.ipynb
```

### 3. Validação (ordem recomendada)

1. Execute `Validacoes/01_YOLO11s-cls/Validacao_YOLO11s-cls.ipynb`
2. Execute `Validacoes/02_EfficientNet-B0/Validacao_EfficientNet-B0.ipynb`
3. Execute `Validacoes/03_Comparacao_YOLO_vs_CNN/Comparacao_YOLO_vs_CNN.ipynb`

Os notebooks localizam automaticamente as pastas de treinamento e geram:
- Matrizes de confusão, curvas ROC/PR
- Análise de calibração e incerteza
- Grad-CAM
- Relatórios em Word
- Tabelas e figuras prontas para apresentação

---

## 📈 O que foi avaliado

Cada validação cobre:

- ✅ Integridade dos dados e detecção de vazamento
- ✅ Acurácia por época (treino e validação)
- ✅ Desempenho e variância estatística
- ✅ Matrizes de confusão e curvas ROC/PR
- ✅ Log-loss e calibração
- ✅ Visão clínica (sensibilidade / especificidade)
- ✅ Robustez a perturbações (ruído, desfoque, JPEG)
- ✅ Grad-CAM e análise de erros
- ✅ Eficiência (parâmetros e tempo de inferência)
- ✅ Reprodutibilidade e checklist de qualidade

---

## 🛠️ Tecnologias

| Componente | Tecnologia |
|------------|------------|
| CNN | EfficientNet-B0 (timm / torchvision) |
| YOLO | YOLO11s-cls (Ultralytics) |
| Framework | PyTorch |
| Dataset | Roboflow |
| Análise | scikit-learn, pandas, matplotlib |
| Relatórios | python-docx |

---

## 📄 Licença

Este projeto está sob a licença **MIT**. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

O dataset original está sob licença **CC BY 4.0**.

---

## 👤 Autor

**Pedro Vyctor Carvalho de Almeida**  
Estudante de Ciência de Dados e Inteligência Artificial — PUC-SP

[![GitHub](https://img.shields.io/badge/GitHub-ppvyctor-181717?logo=github)](https://github.com/ppvyctor)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Pedro%20Vyctor-0A66C2?logo=linkedin)](https://www.linkedin.com/in/pedro-vyctor-almeida-285b89273)

---

## 📚 Referências e Agradecimentos

- Dataset disponibilizado via [Roboflow Universe](https://universe.roboflow.com)
- Ultralytics YOLO
- EfficientNet (Tan & Le, 2019)

---

<div align="center">

**Feito com ❤️ e muita RM cerebral**

</div>
