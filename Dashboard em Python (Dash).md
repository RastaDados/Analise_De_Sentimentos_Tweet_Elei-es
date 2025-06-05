## Dashboard em Python Utilizando o Dash

```python
import dash
from dash import dcc, html
import pandas as pd
import plotly.express as px
from sklearn.feature_extraction.text import CountVectorizer
import re
import string
import nltk
from nltk.corpus import stopwords

#Preparando o nltk
nltk.download('stopwords')
stop_words = set(stopwords.words('english'))

def clean_text(text):
    text = re.sub(r"http\S+|@\S+|#\S+", "", str(text))
    text = text.lower()
    text = re.sub(f"[{re.escape(string.punctuation)}]", "", text)
    tokens = text.split()
    tokens = [t for t in tokens if t not in stop_words and len(t) > 2]
    return " ".join(tokens)

#Carregando os dados
df = pd.read_csv("dados/Sentiment.csv")
df = df[df['relevant_yn'] == 'yes'].dropna(subset=['sentiment', 'text', 'candidate'])
df['tweet_created'] = pd.to_datetime(df['tweet_created'], errors='coerce')
df['sentiment'] = df['sentiment'].str.capitalize()
df['date'] = df['tweet_created'].dt.date

#Limpando o texto para a análise de palavras (como em wordmap por exemplo)
df['clean_text'] = df['text'].astype(str).apply(clean_text)

# Preparando os dados para criar os gráficos 

#Sentimentos ao longo do tempo
time_data = df.groupby(['date', 'sentiment']).size().reset_index(name='count')

#Sentimento por candidato
candidate_data = df.groupby(['candidate', 'sentiment']).size().reset_index(name='count')

#Sentimento por localidade (top 10)
location_df = df[df['tweet_location'].notna()]
top_locations = location_df['tweet_location'].value_counts().head(10).index
location_data = location_df[location_df['tweet_location'].isin(top_locations)]
location_data = location_data.groupby(['tweet_location', 'sentiment']).size().reset_index(name='count')

#Distribuição de sentimentos
dist_data = df['sentiment'].value_counts().reset_index()
dist_data.columns = ['sentiment', 'count']

#Retweets por sentimento
retweet_data = df[['sentiment', 'retweet_count']].dropna()

#Top palavras por sentimento
top_words_by_sentiment = {}
for sentiment in df['sentiment'].unique():
    texts = df[df['sentiment'] == sentiment]['clean_text']
    vectorizer = CountVectorizer(max_features=20)
    X = vectorizer.fit_transform(texts)
    word_freq = pd.DataFrame(X.toarray(), columns=vectorizer.get_feature_names_out()).sum().sort_values(ascending=False)
    top_words_by_sentiment[sentiment] = word_freq

#Criação do App 
app = dash.Dash(__name__)
app.title = "Dashboard de Sentimento Político"

app.layout = html.Div([
    html.H1("Análise de Sentimentos Políticos em Tweets", style={'textAlign': 'center', 'color': '#2c3e50'}),

    dcc.Graph(figure=px.line(
        time_data, x='date', y='count', color='sentiment',
        title='Evolução dos Sentimentos ao Longo do Tempo',
        template='plotly_white'
    )),

    dcc.Graph(figure=px.bar(
        candidate_data, x='candidate', y='count', color='sentiment',
        title='Sentimento por Candidato', barmode='group',
        template='plotly_white'
    )),

    dcc.Graph(figure=px.bar(
        location_data, x='count', y='tweet_location', color='sentiment',
        title='Sentimento por Localização (Top 10)', orientation='h',
        barmode='stack', template='plotly_white'
    )),

    dcc.Graph(figure=px.pie(
        dist_data, names='sentiment', values='count',
        title='Distribuição Geral dos Sentimentos',
        template='plotly_white'
    )),

    dcc.Graph(figure=px.box(
        retweet_data, x='sentiment', y='retweet_count', color='sentiment',
        title='Distribuição de Retweets por Sentimento',
        points='all', template='plotly_white'
    )),

    *[html.Div([
        html.H2(f"Top Palavras - {sentiment}", style={'textAlign': 'center'}),
        dcc.Graph(figure=px.bar(
            x=top_words_by_sentiment[sentiment].values,
            y=top_words_by_sentiment[sentiment].index,
            orientation='h', title=f"Top 20 Palavras em Tweets {sentiment}",
            template='plotly_white'
        ))
    ]) for sentiment in top_words_by_sentiment]
])

if __name__ == '__main__':
    app.run_server(debug=True)
```
