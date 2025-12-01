# Sat-Conjunction-ML
# LEO-Collision-Risk-SVM-Classifier

## Resumo do Projeto

Este projeto implementa um classificador de Machine Learning (ML) para o Gerenciamento de Tráfego Espacial (STM), focado na avaliação de risco de conjunções na **Órbita Baixa da Terra (LEO)**.

O sistema processa TLEs (Two-Line Elements) em lote, utilizando a propagação orbital (Skyfield/SGP4) para gerar *features* físicas (Dmin, Vrel, Tmin). O objetivo central é validar uma arquitetura de segurança que lida com o desbalanceamento de classes e elimina o erro mais crítico: o **Falso Negativo (FN)**.

##  Contribuição Principal e Lógica de Segurança

A principal contribuição reside na solução operacional para o problema do FN, conforme detalhado na Seção de Resultados do artigo:

1.  **Modelo Robusto:** Treinamento do **Support Vector Machine (SVM)** com **SMOTE** para lidar com o desbalanceamento de classes (90% Baixo Risco vs. 10% Alto Risco).
2.  **Mitigação do FN:** Implementação de um **limiar probabilístico conservador (0.02)**. Esta regra de segurança **elimina o Falso Negativo**, pois força o sistema a classificar como ALERTA (Risco 1) qualquer evento cuja probabilidade cruze o limiar, aceitando o custo de introduzir **Falsos Positivos (FPs)** em troca da segurança absoluta (trade-off de engenharia).

##  Arquitetura e Execução

### 1. Pré-requisitos

Para replicar o ambiente, você precisa das bibliotecas listadas no `requirements.txt`.

Instale as dependências no seu ambiente (ex: Google Colab):
```bash
pip install -r requirements.txt

### 2. Execução em Modo Offline (Validação)
Garanta que o arquivo de validação (Teste.csv) esteja no diretório raiz.

Execute o script principal (projeto_conjuncao.py):

python projeto_conjuncao.py
No menu, escolha a Opção 1 (MODO OFFLINE).

Insira o caminho do arquivo de teste (Teste.csv).

Resultado Comprovado: A saída demonstrará que a lógica de segurança (o limiar de 0.01) classificou corretamente o evento de FN como Risco Alto (1.00), validando a tese de segurança.
