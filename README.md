# graphQL-course

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






