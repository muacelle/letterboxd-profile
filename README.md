## > WIP <

# Your Letterboxd Profile
O programa recebe como input um arquivo CSV com todos os filmes assistidos e avaliados pelo usuário no Letterboxd, e retorna:
 1) Ranking dos seus Diretores preferidos (com as notas mais altas);
 2) Ranking dos Diretores mais assistidos;
 3) (WIP) Ranking dos Diretores com as piores notas.

---

# Libs & Frameworks
```
csv-parse
node-fetch
dotenv
underscore
react
```
---

# Estrutura
## 1. CSV Reader
O input é um arquivo CSV, exportado pelo Letterboxd, que lista as notas dadas pelo usuário aos filmes assistidos. Por isso, o primeiro passo do programa é ler o arquivo. 

O CSV tem o seguinte conteúdo:

```
Date,Name,Year,Letterboxd URI,Rating
2021-09-17,Old,2021,https://boxd.it/npKI,3
2021-09-20,Candyman,2021,https://boxd.it/kHFg,3.5
2021-09-26,The Matrix Revolutions,2003,https://boxd.it/2a12,2
2021-10-16,Scream,1996,https://boxd.it/24EC,4
...
```

## 2. JSON Writer
Usei o csv-parse para ler o arquivo ratings.csv e, em seguida, me utilizei das funções de fs para criar um novo arquivo JSON e salvar nele apenas os dados necessários: título do filme, diretor e nota do usuário.

```
[
  {
    "title": "A Faithful Man",
    "director": "Louis Garrel",
    "rating": 3.5
  },
  {
    "title": "Suspiria",
    "director": "Luca Guadagnino",
    "rating": 4
  },
  ...
]
```
**Espera aí!** Você percebeu que o arquivo CSV **não** informava o diretor dos filmes? Então **como** trazemos esse dado em todos os filmes do nosso JSON?

---

## IMDB API
Eu utilizei a API do IMDB para coletar os nomes dos diretores. Construí duas funções assíncronas para buscar os filmes pelo título (getMovieID) e pegar o nome do diretor de cada um (getDirectorName), e lidei com os erros que surgiram no caminho após identificar a causa deles (tryThisInstead). 

- **Error Handling**: 

Algumas vezes, a busca no formato "filme, ano" na API do IMDB, em vez de retornar o filme, retornava um episódio de podcast sobre o filme em questão - o que, por sua vez, gerava um erro (ainda bem!).

Eu lidei com esse erro refazendo a busca com apenas o título do filme, sem o ano, porque percebi, após alguns testes, que o resultado era mais preciso nesse formato.

_Mas, @muacelle, por que então fazer a busca no formato "filme, ano" pra início de conversa? Por que não buscar apenas pelo título, se o resultado é mais preciso assim???_ 

Eu te digo o porquê: REMAKES! THEY'RE EVERYWHERE! 

**Considerando ambos os cenários, uma pesquisa com padrão de formato "filme, ano" ainda é mais assertiva. ;)**

--- 

## 3. [WIP] Gerando os Rankings

<h1> O que eu aprendi </h1>

<h1> Próximos passos </h1>

<h1> Links e Referências </h1>
