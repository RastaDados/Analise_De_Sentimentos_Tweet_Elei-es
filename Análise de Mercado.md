## Análise de Sentimentos de Mídias Sociais em Eleições

<hr>

## 🎯 Objetivos da Análise

#### Problema de Negócio:

Durante o período eleitoral, a opinião pública expressa nas redes sociais tem impacto direto sobre a imagem dos candidatos, decisões de campanha e percepção geral do eleitorado. No entanto, essa percepção é bastante difusa e difícil de medir sem uma análise, e eu estou aqui para resolver essa questão.

#### Oportunidade Identificada:

A análise de sentimentos em tweets fornece uma oportunidade de monitorar em tempo real a reputação de cada candidato, identificar pontos críticos de insatisfação, e mapear os focos de apoio ou rejeição.

#### Perguntas-Chave:

- Qual o sentimento predominante em relação aos candidatos nas redes sociais?
- Como esses sentimentos evoluem ao longo do tempo?
- Quais localidades, candidatos ou perfis de tweets estão mais associados a sentimentos negativos ou positivos?
- Existe correlação entre o número de retweets e o tipo de sentimento?
- Quais palavras estão mais associadas a cada sentimento?

<hr>

## 📈 Principais Indicadores-Chave (KPIs)

<table>
  <thead>
    <tr>
      <th>KPI</th>
      <th>Descrição</th>
      <th>Relação com o Negócio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Volume Total de Tweets Relevantes</td>
      <td>Total de registros após filtragem da coluna relevant_yn.</td>
      <td>Mede o engajamento político geral nas redes.</td>
    </tr>
    <tr>
      <td>Distribuição de Sentimentos</td>
      <td>Proporção de tweets classificados como Positivo, Neutro ou Negativo.</td>
      <td>Identifica a percepção predominante do público</td>
    </tr>
    <tr>
      <td>Evolução Temporal dos Sentimentos</td>
      <td>Quantidade diária de tweets por sentimento.</td>
      <td>Permite rastrear oscilações de reputação ao longo da campanha.</td>
    </tr>
    <tr>
      <td>Sentimento por Candidato</td>
      <td>Agrupamento de sentimentos por cada político mencionado.</td>
      <td>Mostra quais candidatos têm mais apoio ou rejeição online.</td>
    </tr>
    <tr>
      <td>Sentimento por Localidade</td>
      <td>Análise geográfica por tweet_location.</td>
      <td>Ajuda a mapear regiões críticas ou favoráveis para cada campanha.</td>
    </tr>
    <tr>
      <td>Retweets por Sentimento</td>
      <td>Distribuição de retweet_count por tipo de sentimento.</td>
      <td>Avalia quais tipos de sentimento geram mais engajamento.</td>
    </tr>
    <tr>
      <td>Top Palavras por Sentimento</td>
      <td>Palavras mais frequentes nos tweets por tipo de sentimento.</td>
      <td>Ajuda a entender os temas e tópicos associados a cada emoção.</td>
    </tr>
  </tbody>
</table>

<hr>

## 📊 Interpretação das Visualizações

### Evolução dos Sentimentos ao Longo do Tempo

- Gráfico: Linha (line plot) por dia e sentimento.

  ![image](https://github.com/user-attachments/assets/2475dadb-a30a-4457-be89-9be3dc4ad091)

#### Padrões Observados:

- Flutuações marcantes em determinados dias podem indicar eventos políticos relevantes (ex: debates, escândalos).
- O sentimento negativo apresenta picos mais altos em determinados momentos, sugerindo polêmicas.

<hr>

### Sentimento por Candidato

- Gráfico: Barras agrupadas.

![image](https://github.com/user-attachments/assets/6e370136-4aea-4c79-83df-8872a02f07b6)

#### Interpretação:

- Candidatos A e B apresentam maior volume de tweets negativos.
- Apenas um candidato possui predominância de sentimentos positivos — oportunidade de benchmarking.

<hr>

### Sentimento por Localização (Top 10)

- Gráfico: Barras horizontais empilhadas.

![image](https://github.com/user-attachments/assets/7ecc98ab-6e47-48f2-8ff5-5dbfa8f65ee0)

#### Insights:

- Determinadas regiões apresentam expressiva rejeição.
- Outras demonstram equilíbrio ou leve viés positivo, o que pode indicar bases eleitorais fortes.

<hr>

### Distribuição Geral dos Sentimentos

- Gráfico: Pizza.

![newplot](https://github.com/user-attachments/assets/2f8e5cd7-893a-48b5-88e9-643691fc885f)

#### Observações:

- Sentimentos negativos superam os positivos.
- Sentimento neutro também é relevante, podendo representar desinformação ou falta de posicionamento claro.

<hr>

### Boxplot de Retweets por Sentimento

- Gráfico: Boxplot .

![image](https://github.com/user-attachments/assets/9051b8c1-bef6-4352-b8c4-76a9673f6517)

#### Padrões:

- Tweets negativos possuem maior dispersão e picos de viralização (retweets), reforçando o poder de impacto negativo.
- Tweets positivos têm menor engajamento médio.

<hr>

### Top Palavras por Sentimento

- Gráficos: Barras horizontais por sentimento.

![03](https://github.com/user-attachments/assets/df8c7a7e-8127-45cd-8ae9-6a0618adedf1)

![02](https://github.com/user-attachments/assets/1e8cf0be-3ab1-466e-b3a3-a0ad70c97121)

![01](https://github.com/user-attachments/assets/34ea0e7c-3c10-4564-b281-a3afc0fbab0f)

#### Insights:

- Sentimento positivo associado a palavras como support, leader, win.
- Sentimento negativo traz palavras como corruption, lie, fail.
- Sentimento neutro se concentra em termos factuais ou informativos.

<hr>

## Insights Estratégicos e Operacionais

#### Desempenho Atual:

- Alto volume de sentimentos negativos pode indicar insatisfação generalizada ou campanhas negativas bem-sucedidas.
- Baixa incidência de tweets positivos limita o engajamento orgânico positivo dos eleitores.

#### Oportunidades:

- Campanhas podem direcionar conteúdos positivos onde o sentimento negativo domina, especialmente em localidades com maior rejeição.
- Monitorar as palavras-chave mais negativas pode orientar estratégias de comunicação corretiva.

#### Riscos:

- Candidatos com maior exposição negativa devem mitigar crises reputacionais rapidamente.
- Tweets virais com viés negativo podem afetar a percepção pública de forma desproporcional.

<hr>

## Recomendações Que eu Sugiro (Sua análise pode ser diferente da minha, rs.)

#### Ações Imediatas:

- Mapear eventos críticos nos dias com maior negatividade e planejar respostas públicas.
- Fortalecer conteúdos positivos nos canais oficiais, estimulando retweets e menções positivas.
- Segmentar campanhas de rebranding em regiões com maior rejeição.
- Utilizar palavras associadas a sentimentos positivos nos discursos e postagens.

#### Monitoramento Contínuo:

- Evolução dos sentimentos por data e candidato.
- Alterações nas palavras mais frequentes por sentimento.
- Volume de retweets como indicador de viralização negativa.

<hr>

## Resumo  com Detalhes Importantes

- Este projeto analisou mais de 3 mil tweets políticos relevantes utilizando técnicas de análise de sentimentos, visualização interativa e segmentação por candidato e região.

#### Principais descobertas:

- Predominância de sentimentos negativos nas redes sociais.
- Candidatos mais populares nem sempre são os mais bem avaliados.
- Tweets negativos têm maior viralização e podem amplificar crises.
- Palavras mais comuns nos tweets ajudam a identificar temas críticos e oportunidades.






