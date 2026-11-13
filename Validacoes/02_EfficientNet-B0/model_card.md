# Model card — EfficientNet-B0

> Trabalho acadêmico. Não é um dispositivo médico e não deve apoiar diagnóstico real.

## Uso pretendido
Classificar imagens de ressonância magnética cerebral em 4 classes (glioma, meningioma, notumor, pituitary).

## Dados
- Conjunto Tumor Cerebral v1 (Roboflow, CC BY 4.0), 6879 imagens 512×512: treino 4819, validação 1379, teste 681.
- 101 imagens de teste (14.8%) têm quase-duplicata no treino; sem identificador de paciente.
- Manifesto do dataset (SHA-256): 24859d45c130ff831b85f33283d958c068deb77555e1f9657af7b7905a6e8b73

## Treino
- EfficientNet-B0 (torchvision, ImageNet), AdamW, lr 3e-4, batch 32, 512×512, semente 42; 100 épocas, melhor na 40ª.

## Desempenho (teste, 681 imagens)
- Acurácia 0.9912 (IC 95% [0.9838; 0.9971]) · F1 macro 0.9914 · AUC macro 0.9999 · log-loss 0.0339 · ECE 0.0087
- Teste limpo: acurácia 0.9895 (570 imagens)
- Visão clínica: sensibilidade 1.0000, especificidade 0.9936
- Média ± desvio em 50 dobras do teste: 0.9912 ± 0.0065
- Pior classe (recall): meningioma = 0.9830
- Robustez: queda média de 22.3 p.p. sob perturbações sintéticas

## Limitações
- Validação interna (mesmo conjunto de origem); sem validação externa.
- Quase-duplicatas entre treino e teste; auditoria de atalhos: atributos triviais da imagem preveem 0.93 (acaso 0.25).
- Uma execução de treino (sem variância entre treinos).

## Reprodutibilidade
- Pesos (SHA-256): 5bd491856e8d1fbde961772b393b7c43e1e92ca30e6446d135d565671431cc94
- Ambiente: Python 3.14.0, torch 2.11.0+cpu, ultralytics 8.4.194, scikit-learn 1.8.0; dispositivo cpu. Diferença máxima entre execuções repetidas: 0e+00.
