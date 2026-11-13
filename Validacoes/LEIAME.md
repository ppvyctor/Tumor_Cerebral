# Validações — classificação de tumor cerebral em RM

Tudo o que é validação dos dois modelos está nesta pasta, separado em três partes.

```
Validacoes/
├── 01_YOLO11s-cls/                  só o YOLO11s-cls
├── 02_EfficientNet-B0/              só a CNN (EfficientNet-B0)
├── 03_Comparacao_YOLO_vs_CNN/       só a comparação dos dois
├── _compartilhado/cache/            probabilidades em cache (lidas pelos três notebooks)
└── _anteriores/                     versões antigas, guardadas e não apagadas
```

## O que tem em cada pasta

| Pasta | Notebook | Relatório Word | Também contém |
|---|---|---|---|
| `01_YOLO11s-cls` | `Validacao_YOLO11s-cls.ipynb` | `Relatorio_Validacao_YOLO11s-cls.docx` | `figuras/` (18), `tabelas/`, `legendas.json`, `numeros_chave.csv/.json`, `checklist.json`, `model_card.md`, `reprodutibilidade.json` |
| `02_EfficientNet-B0` | `Validacao_EfficientNet-B0.ipynb` | `Relatorio_Validacao_EfficientNet-B0.docx` | idem |
| `03_Comparacao_YOLO_vs_CNN` | `Comparacao_YOLO_vs_CNN.ipynb` | `Relatorio_Comparacao_YOLO_vs_CNN.docx` | `figuras/` (17), `tabelas/`, `legendas.json`, `numeros_chave.csv/.json`, `conclusao_comparacao.md` |

Cada validação de modelo cobre: dados e integridade (vazamento, atalhos), treinamento, **acurácia de treino e validação por época**, desempenho e variância, matrizes de confusão, ROC/PR, log-loss, calibração, visão clínica, incerteza estatística, robustez, Grad-CAM, análise de erros, eficiência, reprodutibilidade e checklist.

A comparação só traz o que exige olhar os dois juntos (métricas lado a lado, curvas sobrepostas, estatística pareada, erros em comum, placar). Os mapas de calor das figuras 12 e 13 são cópias fiéis das aprovadas.

## Ordem para rodar de novo

1. `01_YOLO11s-cls/Validacao_YOLO11s-cls.ipynb` e `02_EfficientNet-B0/Validacao_EfficientNet-B0.ipynb` (geram as probabilidades em `_compartilhado/cache` e os resultados de cada modelo; ≈ 8 a 12 min cada em CPU).
2. `03_Comparacao_YOLO_vs_CNN/Comparacao_YOLO_vs_CNN.ipynb` (lê o cache e os resultados dos dois; ≈ 3 a 5 min).

Os notebooks encontram a pasta do trabalho sozinhos (procuram `Treinamento_CNN` e `Treinamento_YOLO` acima da pasta onde estão).

## Dentro de `_anteriores/`

- `Validacao_Completa_3_etapas/`: o notebook antigo de 3 etapas (YOLO, CNN e comparação no mesmo arquivo), seus resultados e o `resultados_validacao.zip`.
- `Kit_Apresentacao/`: o kit de apresentação anterior (figuras, guia em Word e notebook). Dele vêm os dois mapas de calor usados na comparação.

## Observações

- A acurácia de treino **por época** só existe para a CNN; o treino do YOLO não a gravou (o `results.csv` só tem a loss de treino). No relatório do YOLO aparece a acurácia de treino do melhor checkpoint, medida depois, sem augmentation.
- As metas do checklist são do grupo, não padrões clínicos. Trabalho acadêmico: os modelos não são dispositivos médicos.
