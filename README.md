# graphQL-course


In visual studio code installare :


![Screenshot 2024-09-10 alle 11 37 25](https://github.com/user-attachments/assets/d4dd69dc-63fa-4c45-b091-4e3be267c1a4)



# What is GraphQL ?

-graphQl is a Query Language.
-Alternative to using a Rest API


Rest API :

Endpoints :

pokemonsite.com/api/pokemon
pokemonsite.com/api/pokemon/123

_________________________

Over fetching :

Getting back more data than we need
![Screenshot 2024-09-10 alle 10 31 00](https://github.com/user-attachments/assets/f188f5f2-d1bb-43b2-9ede-6485935097a5)


_________________________

Under fetching :

Getting back less data then we need

In GraphQL, il **under-fetching** (o *under-fetching*) si verifica quando una query non recupera abbastanza dati in una singola richiesta, costringendo a effettuare ulteriori query per ottenere le informazioni mancanti. Questo accade quando la struttura dello schema GraphQL non è ben allineata con le esigenze specifiche del client o dell'interfaccia utente, portando a più richieste al server per ottenere tutti i dati necessari.

### Esempio di Sotto-fetching:
Immagina di fare una query per ottenere un elenco di utenti, ma nella risposta ricevi solo dettagli di base come `nome` ed `email`. Se hai bisogno di ulteriori informazioni, come l'indirizzo o il numero di telefono, dovresti fare un'altra query per recuperare quei dati mancanti.

### Come evitare il sotto-fetching:
- **Progettare lo schema con attenzione**: Assicurarsi che lo schema includa tutti i campi rilevanti, riducendo il rischio di perdere dati necessari.
- **Usare query nidificate**: GraphQL consente di effettuare query profondamente nidificate, permettendo di specificare esattamente quali dati sono richiesti in un'unica richiesta.
- **Caricamento in batch**: Implementare tecniche come **DataLoader** per raggruppare e memorizzare in cache le chiamate al database o API, migliorando le prestazioni e riducendo la necessità di fare più richieste.

In questo modo si può evitare di dover fare più round-trip al server per ottenere i dati necessari, migliorando l'efficienza della comunicazione tra client e server.


_____________________

In GRAPHQL abbiamo un singolo endpoint ( es : mysite.com/graphql

Esempio di Query :

```
Query {
  courses {
    id ,
    title,
    thumbnail_url
  }

}
```

```

Query {
  course(id : "1" ) {
    id,
    title,
    thumbnail_url,
    author {
      name,
      id,
      courses {
        id,
        title,
        thumbnail_url
      }
    }
  }
}
```


# Query Basics 



In GraphQL, una **query** è il modo principale con cui i client richiedono dati da un server. Le query GraphQL sono strutturate in modo che il client possa chiedere esattamente le informazioni di cui ha bisogno, niente di più e niente di meno. Ciò permette un controllo preciso sui dati ricevuti, migliorando l'efficienza.

### Struttura di una Query di Base

Una query di base in GraphQL ha questa struttura:
1. **Nome del campo**: Indica quale dato si vuole ottenere.
2. **Argomenti (facoltativi)**: Parametri che possono essere passati per filtrare o modificare i risultati.
3. **Selezione dei campi**: Definisce quali campi specifici all'interno di un'entità devono essere restituiti.

#### Esempio:

```graphql
{
  user(id: 1) {
    name
    email
    posts {
      title
      content
    }
  }
}
```

### Cosa Succede in Questo Esempio:
- La query chiede i dati di un utente con `id: 1`.
- Vuole i campi `name` e `email` dell'utente.
- Inoltre, chiede i **post** associati a quell'utente, ma solo i campi `title` e `content` di ogni post.

### Componenti di Base di una Query GraphQL

1. **Root Field (Campo Radice)**: Ogni query parte con un campo radice. In questo caso, `user` è il campo radice, e il server capirà che deve cercare un utente nel database.
   
2. **Argomenti**: Alcuni campi possono accettare argomenti. In questo esempio, l'argomento `id: 1` specifica quale utente viene richiesto. Gli argomenti possono essere facoltativi o obbligatori, a seconda di come è stato definito lo schema.

3. **Selezione dei Campi**: GraphQL consente di specificare esattamente quali campi restituire. Invece di restituire tutte le informazioni dell'utente, la query richiede solo `name` ed `email`, e questo evita di ottenere dati non necessari.

4. **Nested Queries (Query Nidificate)**: GraphQL consente di richiedere dati correlati all'interno della stessa query. In questo esempio, oltre ai dati dell'utente, vengono richiesti anche i **post** dell'utente con i campi `title` e `content`.

### Vantaggi delle Query in GraphQL
- **Evita l'over-fetching e l'under-fetching**: Ottieni solo i dati richiesti, senza dati in eccesso (over-fetching) o insufficienti (under-fetching).
- **Richieste flessibili**: Puoi ottenere dati complessi e correlati con una sola richiesta.
- **Efficiente**: Riduce il numero di chiamate al server rispetto alle API REST, poiché consente di ottenere dati nidificati con una singola query.

### Altri Elementi delle Query GraphQL
- **Alias**: Permettono di rinominare i campi nella risposta.
- **Variabili**: Parametri dinamici che puoi passare nella query per rendere il codice più flessibile.
- **Frammenti**: Parti di query riutilizzabili, ideali per evitare la duplicazione del codice.

GraphQL offre un modo più potente e flessibile per richiedere dati rispetto alle tradizionali API REST, adattando la richiesta esattamente ai bisogni del client.

______________________________________

# Making a Graphql Server

(apollo server )


https://www.apollographql.com/docs/apollo-server/

![Screenshot 2024-09-10 alle 11 12 58](https://github.com/user-attachments/assets/b9c898b6-ac0c-4549-a5bd-f96cdf3d239c)


![Screenshot 2024-09-10 alle 11 13 08](https://github.com/user-attachments/assets/ca73a8d0-1de9-4972-b3b6-42f2493269a5)



________________________

# Schema e types


In GraphQL, lo **schema** e i **types** (tipi) sono concetti fondamentali che definiscono la struttura dei dati disponibili per le query e mutazioni. Essi stabiliscono quali tipi di operazioni possono essere eseguite e quali dati possono essere richiesti o modificati.

### 1. **Schema**
Lo **schema** è il cuore di ogni server GraphQL. Esso descrive le operazioni disponibili (query, mutazioni e, opzionalmente, subscription) e specifica i tipi di dati che il client può richiedere o inviare. In pratica, è un contratto tra il server e i client che lo utilizzano.

Uno schema in GraphQL viene definito utilizzando il **GraphQL Schema Definition Language (SDL)**, che è molto leggibile e simile a un linguaggio di dichiarazione.

#### Esempio di schema base:

```graphql
schema {
  query: Query
  mutation: Mutation
}
```

- **Query**: È il tipo principale che definisce come leggere i dati.
- **Mutation**: È il tipo che definisce come modificare (creare, aggiornare o cancellare) i dati.

### 2. **Types (Tipi)**
I **tipi** in GraphQL sono le definizioni delle strutture dei dati disponibili all'interno del sistema. Possono essere pensati come classi o modelli che descrivono come un dato specifico deve essere formato e quali campi (proprietà) contiene. 

Ci sono vari tipi principali:

#### a. **Tipi scalari**
Questi sono i tipi primitivi (valori atomici) in GraphQL. Alcuni tipi scalari predefiniti sono:
- `String`: Una sequenza di caratteri.
- `Int`: Un numero intero.
- `Float`: Un numero a virgola mobile.
- `Boolean`: Un valore booleano (true o false).
- `ID`: Un identificatore unico (solitamente usato per identificare oggetti).

Esempio di definizione di un tipo scalare in un campo di una query:

```graphql
type Query {
  hello: String
}
```

Qui il tipo `hello` è una stringa (`String`), quindi quando viene eseguita la query, il campo `hello` restituirà una stringa.

#### b. **Object types (Tipi di oggetto)**
I tipi di oggetto sono i tipi principali usati per rappresentare entità complesse con campi multipli.

Esempio di un tipo di oggetto:

```graphql
type User {
  id: ID!
  name: String!
  email: String!
}
```

Qui, `User` è un tipo di oggetto che ha tre campi: `id` (di tipo `ID`), `name` (di tipo `String`) ed `email` (di tipo `String`). Il punto esclamativo (`!`) indica che quel campo è **non nullo**, cioè deve sempre avere un valore.

#### c. **Input types (Tipi di input)**
I tipi di input vengono usati per passare dati durante una mutazione. Funzionano in modo simile ai tipi di oggetto, ma non possono includere campi nidificati o complessi, perché servono solo per passare dati da usare all'interno delle operazioni.

Esempio di tipo di input:

```graphql
input CreateUserInput {
  name: String!
  email: String!
}
```

Questo tipo di input può essere usato per passare dati a una mutazione per creare un nuovo utente.

#### d. **Enum types (Tipi enumerativi)**
I tipi enumerativi limitano i valori che un campo può assumere a una lista predefinita.

Esempio di tipo enumerativo:

```graphql
enum Role {
  ADMIN
  USER
  GUEST
}
```

Questo tipo `Role` definisce tre valori: `ADMIN`, `USER`, e `GUEST`. Un campo che usa questo tipo potrà avere solo uno di questi valori.

#### e. **List types (Tipi di lista)**
In GraphQL, puoi definire campi che restituiscono una lista di un certo tipo.

Esempio:

```graphql
type Query {
  users: [User]!
}
```

Qui, il campo `users` restituirà una lista di oggetti `User`.

### 3. **Unione tra schema e types**
Lo schema unisce tutte le definizioni di tipi e definisce come devono essere utilizzate nelle query e mutazioni. 

Esempio di uno schema completo:

```graphql
# Definiamo un tipo User
type User {
  id: ID!
  name: String!
  email: String!
}

# Definiamo le query disponibili
type Query {
  users: [User]!
  user(id: ID!): User
}

# Definiamo un input per le mutazioni
input CreateUserInput {
  name: String!
  email: String!
}

# Definiamo le mutazioni disponibili
type Mutation {
  createUser(input: CreateUserInput!): User!
}
```

In questo esempio:
- La query `users` restituisce una lista di utenti.
- La query `user` restituisce un singolo utente in base al suo `id`.
- La mutazione `createUser` crea un nuovo utente utilizzando i dati forniti attraverso il tipo di input `CreateUserInput`.

### Riassumendo
- Lo **schema** definisce la struttura generale dell'API GraphQL, includendo i tipi e le operazioni possibili (query, mutazioni).
- I **tipi** definiscono i dati che possono essere richiesti o inviati, fornendo una descrizione chiara delle entità e delle loro relazioni.












