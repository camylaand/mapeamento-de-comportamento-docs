#  Documentação do Projeto – Mapeamento de Comportamento de Transações por Conta

 **Documentação Pública** |  **Código Privado**  
 **Atenção:** este repositório contém somente a documentação do projeto.  
O código-fonte é privado e não está disponível para acesso público.  

---

##  Visão Geral
Este projeto implementa um pipeline de **pré-processamento de dados, redução de dimensionalidade, clusterização e análise estatística** para **detectar anomalias em transações financeiras**.  

A abordagem combina:
- **Autoencoder (Deep Learning)** → Redução de dimensionalidade e cálculo de erro de reconstrução.  
- **KMeans** → Clusterização de perfis de comportamento.  
- **ANOVA e GLM** → Validação estatística das diferenças entre clusters.  
- **Perfis comportamentais por conta** → Identificação de padrões individuais.  

O código foi desenvolvido para auxiliar em **fraude detection** e **mapeamento de comportamento transacional**.

---

##  Estrutura Geral
- **Pré-processamento**
  - Conversão de datas e criação de variáveis derivadas (dia da semana, fim de semana, faixa horária).
  - Exclusão de colunas irrelevantes (`transacao_id`, `conta_destino_id`).
  - Codificação de variáveis categóricas com **OneHotEncoder**.
  - Normalização com **RobustScaler**.

- **Autoencoder**
  - Rede neural para compressão dos dados em espaço latente.
  - Erro de reconstrução usado como métrica de anomalia.
  - Modelo salvo em `modelo_autoencoder.keras`.

- **Clusterização**
  - **KMeans** aplicado nos dados latentes.
  - Clusterização para identificar grupos de comportamento.
  - Resultados salvos em `kmeans_auto.pkl`.

- **Análises Estatísticas**
  - **ANOVA** → Comparação de variáveis entre clusters.  
  - **GLM (Generalized Linear Model)** → Reforço das análises de significância.

- **Perfis de Clientes**
  - Construção de **perfil comportamental por conta**.
  - Variáveis como média de valor, frequência de tipos de transação, horários e dias mais comuns.
  - Perfis salvos em `perfil_comportamentais.csv`.

- **Detecção de Suspeitas**
  - Transações classificadas por nível de suspeita:
    - `nenhuma`, `baixa`, `media`, `alta`.  
  - Resultado exportado em `transacoes_com_suspeita.csv`.

---

##  Tecnologias Utilizadas
- **Linguagem**: Python 3  
- **Bibliotecas principais**:
  - `pandas`, `numpy` → Manipulação de dados
  - `tensorflow/keras` → Autoencoder
  - `scikit-learn` → OneHotEncoder, RobustScaler, KMeans
  - `scipy`, `statsmodels` → Testes estatísticos
  - `joblib` → Serialização de modelos

---

## 📊 Fluxo do Projeto

1. **Leitura e tratamento dos dados**
   - Conversão da coluna `transacao_data`.
   - Criação de colunas adicionais: dia da semana, fim de semana, faixa horária.
   - Exclusão de identificadores irrelevantes.

2. **Codificação e normalização**
   - OneHotEncoder para variáveis categóricas.
   - RobustScaler para variáveis numéricas.

3. **Treinamento do Autoencoder**
   - Compressão dos dados.
   - Cálculo do erro de reconstrução (indicador de anomalia).

4. **Clusterização (KMeans)**
   - Identificação de padrões no espaço latente.
   - Análise de diferenças entre clusters.

5. **Análise Estatística**
   - ANOVA e GLM para confirmar significância das variáveis entre clusters.

6. **Perfis Comportamentais**
   - Perfil agregado por conta.
   - Identificação de padrões de dia da semana, horário e tipo de transação.

7. **Exportação de resultados**
   - Modelos e encoders salvos (`.pkl`, `.keras`).
   - Perfis de clientes (`perfil_comportamentais.csv`).
   - Transações suspeitas (`transacoes_com_suspeita.csv`).

---

**Comparação de Clusters**
  - A tabela abaixo mostra a diferença entre os clusters encontrados pelo **Autoencoder + KMeans**, evidenciando variáveis com maior impacto:

![Comparação de clusters](https://github.com/user-attachments/assets/5f7f0779-ca73-45f0-9ad0-5682a080bf09)


---
##  Saídas Geradas
- **Modelos**
  - `modelo_autoencoder.keras`
  - `modelo_encoder.keras`
  - `kmeans_auto.pkl`
  - `scaler.pkl`
  - `encoder_tipo_transacao.pkl`
  - `encoder_semana.pkl`
  - `encoder_horario.pkl`

- **Resultados**
  - `perfil_comportamentais.csv` → Perfil agregado por cliente.
  - `transacoes_com_suspeita.csv` → Transações com grau de suspeita.

---

## 📌 Aplicações
- **Detecção de Fraudes em Tempo Real**  
- **Segmentação de Clientes por Comportamento**  
- **Suporte a Sistemas de Risco e Compliance**  

