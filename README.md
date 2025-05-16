# Detecção de Vazamento de Gás com BMia+MRMR 

![License](https://img.shields.io/badge/license-MIT-blue)

##  Sumário
- [Contexto](#contexto)
- [Abordagem](#abordagem)
- [Resultados](#resultados)
- [Como executar](#como-executar)
- [Visualizações](#visualiza%C3%A7%C3%B5es)
- [Próximos passos](#pr%C3%B3ximos-passos)
- [Licença](#licen%C3%A7a)

##  Contexto
Monitoramento de sensores em tubulações industriais para detecção antecipada de vazamentos de gás.  
Desafio: poucas variáveis, alto ruído e necessidade de explicabilidade para operadores.

## 🛠️ Abordagem
1. **Pré‑processamento**  
   - Limpeza, normalização (StandardScaler) e split estratificado  
2. **Seleção de Features**  
   - Comparação entre MI tradicional (30 features) e BMia+MRMR (10 features)  
3. **Modelagem**  
   - Teste de RandomForest, KNeighbors, VotingClassifier e GradientBoosting  
   - Tuning com RandomizedSearch (40 iterações)  
4. **Interpretabilidade**  
   - **SHAP**: summary, dependence e force plots  
   - **LIME**: explicações locais em TP, FP, FN e TN  
5. **Avaliação de Custo**  
   - Cálculo de custo hipotético (FP=1, FN=5) e otimização de threshold

## Alguns Resultados
| Modelo                           | Accuracy | F1_weighted | # Features |
|----------------------------------|----------|-------------|------------|
| BMia+MRMR + GradientBoosting     | 0.7667   | 0.7091      | 10         |
| BMia+MRMR + RandomForest         | 0.7472   | 0.7472      | 9 (run prévio) |
| MI Traditional + RandomForest    | 0.6667   | 0.5600      | 30         |
| Baseline (100 features) + Voting | 0.7000   | 0.6260      | 100        |

- **Insights**:  
  - Sensores em extremos de operação (muito baixos ou altos) são preditores fortes.  
  - Padrões “U‑shaped” e interações críticas visíveis nos dependence plots.  

##  Como executar
1. Clone o repositório  
   ```bash
   git clone https://github.com/seu-usuario/detect-gas-leak-ml.git
   cd detect-gas-leak-ml

