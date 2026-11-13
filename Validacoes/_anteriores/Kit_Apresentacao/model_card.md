# Model card — classificação de tumor cerebral em RM (YOLO11s-cls e EfficientNet-B0)

> Trabalho acadêmico. **Não é um dispositivo médico** e não deve apoiar diagnóstico real.

## Uso pretendido
Classificar imagens de ressonância magnética cerebral em 4 classes (glioma, meningioma, notumor, pituitary), como estudo comparativo de duas arquiteturas.

## Dados
- Conjunto *Tumor Cerebral* v1 (Roboflow, CC BY 4.0), 6879 imagens 512×512: treino 4819, validação 1379, teste 681 (divisão estratificada; χ² p = 0.42).
- 101 imagens de teste (14.8%) têm quase-duplicata no treino; sem identificador de paciente.
- Manifesto do dataset (SHA-256 dos arquivos): `24859d45c130ff831b85f33283d958c068deb77555e1f9657af7b7905a6e8b73`

## Treino
- YOLO11s-cls: yolo11s-cls pré-treinado, 100 épocas máx., AdamW, lr 0.0003, batch 32, imgsz 512, semente 42.
- EfficientNet-B0: EfficientNet-B0 (torchvision, ImageNet), AdamW, lr 3e-4, batch 32, 512×512, semente 42, 100 épocas.

## Desempenho (conjunto de teste)
## YOLO11s-cls
- **Teste (681 imagens):** acurácia 0.9794 · F1 macro 0.9794 · AUC macro 0.9987 · log-loss 0.0780 · ECE 0.0050
- **Teste limpo (sem quase-duplicatas, 570 imagens):** acurácia 0.9772
- **Média ± desvio em 50 dobras do teste:** 0.9794 ± 0.0099
- **Visão clínica (tumor × sem tumor):** sensibilidade 0.9924, especificidade 0.9872, F2 0.9931
- **Pior classe (recall):** meningioma = 0.9602
- **Peso (SHA-256):** `1adb24e68c3bfb93e9b9fe49d5be8fd1c796da570db94eea238bf1c3c804b064`

## EfficientNet-B0
- **Teste (681 imagens):** acurácia 0.9912 · F1 macro 0.9914 · AUC macro 0.9999 · log-loss 0.0339 · ECE 0.0087
- **Teste limpo (sem quase-duplicatas, 570 imagens):** acurácia 0.9895
- **Média ± desvio em 50 dobras do teste:** 0.9912 ± 0.0065
- **Visão clínica (tumor × sem tumor):** sensibilidade 1.0000, especificidade 0.9936, F2 0.9996
- **Pior classe (recall):** meningioma = 0.9830
- **Peso (SHA-256):** `5bd491856e8d1fbde961772b393b7c43e1e92ca30e6446d135d565671431cc94`

## Decisão
- Limiar de tumor escolhido pelo custo (FN = 5 × FP) na validação: YOLO 0.02, CNN 0.02.
- Calibração (temperatura, ajustada na validação): T = 1.41 (YOLO) e 2.11 (CNN).

## Limitações
- Validação interna (mesmo conjunto de origem); sem validação externa em outro hospital/scanner.
- Quase-duplicatas entre treino e teste; auditoria de atalhos: atributos triviais preveem 0.93 (acaso 0.25).
- Uma execução de treino por modelo (sem variância entre treinos); curva de aprendizado não avaliada.
- Robustez a ruído, desfoque forte e compressão severa é limitada (ver notebook de validação completa).

## Reprodutibilidade
Ambiente: 3.14.0, torch 2.11.0+cpu, ultralytics 8.4.194, scikit-learn 1.8.0; dispositivo cpu. Diferença máxima entre execuções repetidas: 0e+00.
