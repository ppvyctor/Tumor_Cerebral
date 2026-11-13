
### Conclusão da comparação (gerada automaticamente a partir desta execução)

**Desempenho.** No teste (681 imagens): **EfficientNet-B0** = 99.12% (6 erros) × **YOLO11s-cls** = 97.94% (14 erros).
No teste **limpo** (sem quase-duplicatas do treino): YOLO 97.72% | CNN 98.95%. AUC macro: YOLO 0.9984 | CNN 0.9999. Log-loss: YOLO 0.0780 | CNN 0.0339.

**A diferença é real?** Teste: McNemar p = 0.0574 e IC95% da diferença de acurácia (CNN − YOLO) [+0.15%; +2.20%] → evidência LIMÍTROFE: o IC do bootstrap exclui 0 por pouco, mas o McNemar não é significativo a 5%. Validação (1 379 imagens): p = 3.032e-06 (SIM); o valid também guiou a escolha do melhor epoch.
O ensemble (média das probabilidades) chegou a 99.27% no teste.

**Variância.** gap treino−valid: YOLO 2.84 p.p. | CNN 1.12 p.p.; valid−teste: YOLO -0.84 | CNN -0.28 p.p.

**Clínico.** Sensibilidade p/ tumor no teste: YOLO 99.24% | CNN 100.00%.

**Robustez.** Queda média de acurácia sob perturbações: YOLO 20.5 p.p. | CNN 22.3 p.p.

**Eficiência.** Parâmetros: YOLO 5.45 M | CNN 4.01 M. GFLOPs: 7.7 | 4.0. Latência do modelo (cpu): 75 ms | 144 ms.

**Checklist:** EfficientNet-B0: 10/11 critérios atendidos, YOLO11s-cls: 10/11 critérios atendidos. **Placar:** EfficientNet-B0: 12, YOLO11s-cls: 3.
**Vazamento:** 101 imagens de teste (14.8%) têm quase-duplicata no treino.
