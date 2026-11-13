# Conclusão da comparação — YOLO11s-cls × EfficientNet-B0

**Desempenho.** No teste (681 imagens), EfficientNet-B0 acerta 99,1% (6 erros) e YOLO11s-cls 97,9% (14 erros); no teste limpo (sem quase-duplicatas), 99,0% e 97,7%. AUC macro 0.9999 contra 0.9987; log-loss 0.034 contra 0.078.

**A diferença é real?** Diferença de acurácia (CNN − YOLO) de +1.17 p.p. (IC 95% [+0.15; +2.35]); McNemar p = 0.057 → limítrofe: o IC do bootstrap exclui zero por pouco, mas o McNemar não é significativo a 5%. Na validação (1379 imagens), p = 3e-06. Em 50 dobras do teste, a CNN vence em 74% e perde em 6%.

**Generalização.** Gap treino−validação de 1.12 p.p. (CNN) e 2.84 p.p. (YOLO): variância baixa nos dois; validação ≈ teste.

**Clínico.** Com o corte 0,50: sensibilidade 1.000 (0 falsos negativos) na CNN e 0.992 (4 falsos negativos) no YOLO.

**Robustez.** Queda média de 22.3 p.p. (CNN) e 20.5 p.p. (YOLO); os dois falham com ruído e desfoque forte; só o YOLO falha também com JPEG severo.

**Eficiência.** A CNN é menor (4.0 M × 5.5 M de parâmetros), mas mais lenta na CPU (136 ms × 77 ms).

**Complementaridade.** 3 imagens erradas pelos dois, 3 só pela CNN e 11 só pelo YOLO; o ensemble chega a 99,3%.

**Placar.** CNN 11 × YOLO 3 (0 empates). Checklist: CNN 11/14 OK; YOLO 11/14 OK.
