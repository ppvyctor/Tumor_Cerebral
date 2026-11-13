# Model card — YOLO11s-cls

> Trabalho acadêmico. Não é um dispositivo médico e não deve apoiar diagnóstico real.

## Uso pretendido
Classificar imagens de ressonância magnética cerebral em 4 classes (glioma, meningioma, notumor, pituitary).

## Dados
- Conjunto Tumor Cerebral v1 (Roboflow, CC BY 4.0), 6879 imagens 512×512: treino 4819, validação 1379, teste 681.
- 101 imagens de teste (14.8%) têm quase-duplicata no treino; sem identificador de paciente.
- Manifesto do dataset (SHA-256): 24859d45c130ff831b85f33283d958c068deb77555e1f9657af7b7905a6e8b73

## Treino
- yolo11s-cls pré-treinado, 100 épocas (máx.), AdamW, lr 0.0003, batch 32, imgsz 512, semente 42; 93 épocas executadas, melhor na 63ª.

## Desempenho (teste, 681 imagens)
- Acurácia 0.9794 (IC 95% [0.9692; 0.9897]) · F1 macro 0.9794 · AUC macro 0.9984 · log-loss 0.0780 · ECE 0.0050
- Teste limpo: acurácia 0.9772 (570 imagens)
- Visão clínica: sensibilidade 0.9924, especificidade 0.9872
- Média ± desvio em 50 dobras do teste: 0.9794 ± 0.0099
- Pior classe (recall): meningioma = 0.9602
- Robustez: queda média de 20.5 p.p. sob perturbações sintéticas

## Limitações
- Validação interna (mesmo conjunto de origem); sem validação externa.
- Quase-duplicatas entre treino e teste; auditoria de atalhos: atributos triviais da imagem preveem 0.93 (acaso 0.25).
- Uma execução de treino (sem variância entre treinos).

## Reprodutibilidade
- Pesos (SHA-256): 1adb24e68c3bfb93e9b9fe49d5be8fd1c796da570db94eea238bf1c3c804b064
- Ambiente: Python 3.14.0, torch 2.11.0+cpu, ultralytics 8.4.194, scikit-learn 1.8.0; dispositivo cpu. Diferença máxima entre execuções repetidas: 0e+00.
