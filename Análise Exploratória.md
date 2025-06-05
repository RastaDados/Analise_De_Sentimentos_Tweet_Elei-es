### Análise Exploratória

#### Distribuição de Sentimentos

```python
sns.countplot(data=df, x='sentiment', palette='coolwarm')
plt.title("Distribuição dos Sentimentos")
plt.show()
```

![image](https://github.com/user-attachments/assets/afda3e8b-86bd-4d90-b848-2fec61bb0a41)

#### Sentimento por Candidato

```python
plt.figure(figsize=(12, 6))
sns.countplot(data=df, x='candidate', hue='sentiment', palette='Set2', order=df['candidate'].value_counts().index)
plt.xticks(rotation=90)
plt.title("Sentimento por Candidato")
plt.show()
```

![image](https://github.com/user-attachments/assets/a56745e6-d36d-4ce7-9df8-81790a1f7816)

#### Retweets por Sentimento

```python
sns.boxplot(data=df, x='sentiment', y='retweet_count', palette='pastel')
plt.title("Distribuição de Retweets por Sentimento")
plt.show()
```

![image](https://github.com/user-attachments/assets/31e256fc-594a-4fad-8d8a-a65f50fc1733)

## Análise de Texto

#### Pré-Processamento

```python
stop_words = set(stopwords.words('english'))

def clean_text(text):
    text = re.sub(r"http\S+|@\S+|#\S+", "", text)  # remove links, mentions e hashtags
    text = text.lower()
    text = re.sub(f"[{re.escape(string.punctuation)}]", "", text)
    tokens = text.split()
    tokens = [t for t in tokens if t not in stop_words and len(t) > 2]
    return " ".join(tokens)

df['clean_text'] = df['text'].astype(str).apply(clean_text)
```

#### Nuvens de Palavra por Sentimento

```python
for sentiment in ['Positive', 'Neutral', 'Negative']:
    text = " ".join(df[df['sentiment'] == sentiment]['clean_text'])
    wordcloud = WordCloud(width=800, height=400, background_color='white').generate(text)
    plt.figure(figsize=(10, 5))
    plt.imshow(wordcloud, interpolation='bilinear')
    plt.axis("off")
    plt.title(f"Nuvem de Palavras - {sentiment}")
    plt.show()
```

![image](https://github.com/user-attachments/assets/a3e74732-3185-4bd0-9977-156c1a0145fb)

![image](https://github.com/user-attachments/assets/a2b8ff27-3972-4199-9499-8de059febbd1)

![image](https://github.com/user-attachments/assets/9678fbda-e52f-4e67-a652-84c73ac0d061)

## Outras Visualizações

```python
#Configurações visuais
sns.set(style="whitegrid")

#Sentimento ao longo do tempo
df_time_sentiment = df.copy()
df_time_sentiment['date'] = df_time_sentiment['tweet_created'].dt.date
time_sentiment = df_time_sentiment.groupby(['date', 'sentiment']).size().unstack(fill_value=0)

#Top 10 candidatos mais mencionados
top_candidates = df['candidate'].value_counts().nlargest(10)

#Sentimento por localização geográfica
location_sentiment = df[df['tweet_location'].notna()].groupby(['tweet_location', 'sentiment']).size().unstack(fill_value=0)
top_locations = location_sentiment.sum(axis=1).sort_values(ascending=False).head(10)
location_sentiment_top = location_sentiment.loc[top_locations.index]
```

#### Evolução Temporal dos Sentimentos

```python
#Evolução temporal dos sentimentos
plt.figure(figsize=(12, 6))
time_sentiment.plot(marker='o')
plt.title("Volume de Tweets por Sentimento ao Longo do Tempo")
plt.xlabel("Data")
plt.ylabel("Quantidade de Tweets")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

![image](https://github.com/user-attachments/assets/d2173d18-8c04-4be3-a21e-a431482c27b4)

#### Top 10 candidatos mais mencionados

```python
plt.figure(figsize=(10, 6))
sns.barplot(x=top_candidates.values, y=top_candidates.index, palette="viridis")
plt.title("Top 10 Candidatos Mais Mencionados")
plt.xlabel("Número de Menções")
plt.tight_layout()
plt.show()
```

![image](https://github.com/user-attachments/assets/ca2b6ff0-c152-47bb-a3b1-a86d1e8afce6)

#### Sentimentos por localizações mais ativas

```python
#Sentimentos por localizações mais ativas
plt.figure(figsize=(12, 6))
location_sentiment_top.plot(kind="barh", stacked=True, colormap="Accent", figsize=(12, 6))
plt.title("Sentimentos por Localização (Top 10)")
plt.xlabel("Número de Tweets")
plt.tight_layout()
plt.show()
```

![image](https://github.com/user-attachments/assets/5910c644-769b-497b-bd87-07896c5c4ac0)



