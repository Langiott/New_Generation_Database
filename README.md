# New_Generation_Database
In questo corso magistrale si concentra nello studio e lo sviluppo di database moderni. Questa materia non tratta concetti di Base di Dati ma la sua evoluzione e gli strumenti che si sono creati negli ultimi anni. In questo repository non troverete script o altro , se volete sapere nei dettagli come sviluppare il progetto , vi invito a scrivermi un email. Mi farebbe molto piacere 

## PROGETTO: Modellazione di un Social Network che utilizza Database a Grafo mediante Neo4j "socialITTU"

#### Obiettivo del Progetto
Il progetto ha lo scopo di sviluppare un social network chiamato **socialITTU** utilizzando **Neo4j**, un database a grafo. La struttura a grafo permette una gestione efficiente delle relazioni tra utenti, post, commenti e messaggi, ottimizzando interrogazioni e navigazione dei dati. 

#### Motivazione
I social network sono sistemi altamente connessi, ideali per l'uso di database a grafo. Rispetto ai database relazionali tradizionali, **Neo4j** consente di rappresentare le relazioni in modo esplicito, facilitando query complesse come il "trovare amici di amici", raccomandazioni, o l'analisi di comunità.

#### Vantaggi di Neo4j
1. **Efficienza nelle relazioni**: Le relazioni sono entità di prima classe, memorizzate direttamente con i nodi, rendendo più veloce l'accesso rispetto a database tradizionali.
2. **Navigazione rapida**: La struttura a grafo consente una rapida traversata dei nodi.
3. **Query complesse**: Il linguaggio **Cypher** permette di creare interrogazioni espressive e descrivere pattern complessi tra i dati.
4. **Flessibilità**: Il modello di grafo è facilmente adattabile a nuovi tipi di nodi e relazioni senza dover ristrutturare l'intero schema.

---

### Architettura di Neo4j

Neo4j organizza i dati in:
- **Nodi**: Rappresentano le entità (es. utenti, post, commenti).
- **Relazioni**: Connessioni tra nodi che esprimono legami (es. un utente segue un altro utente, un post riceve un commento).
- **Proprietà**: Attributi associati sia ai nodi che alle relazioni (es. data di creazione, contenuto del post).
- **Query Cypher**: Linguaggio di interrogazione ottimizzato per grafi.

---

### Modello di Dati del Social Network

Il modello di dati è composto da:
- **Entità** principali: *User*, *Post*, *Comment*, *Message*.
- **Relazioni** tra entità: *follows*, *likes*, *posts*, *comments*, *shares*.
  
Esempio di alcune relazioni chiave:
- `(User)-[:FOLLOWS]->(User)`
- `(User)-[:POSTS]->(Post)`
- `(Post)-[:COMMENTS]->(Comment)`

---

### Script fondamentali utilizzati

1. **Creazione di nodi utenti**:
    ```cypher
    CREATE (u1:User {userId: 1, username: "leo_king", password: "pwd123", picture: "leo_pic.jpg", bio: "Aspiring artist", credits: 20, location: "Rome", joinDate: date("2023-01-01"), status: "active"});
    ```

2. **Creazione di post**:
    ```cypher
    CREATE (p1:Post {postId: 1, content: "Exploring the ancient ruins today!", creationDate: datetime("2023-07-01T10:00:00"), mediaUrls: ["post_pic1.jpg"], type: "photo"});
    ```

3. **Creazione di commenti**:
    ```cypher
    CREATE (c1:Comment {commentId: 1, content: "Amazing ruins!", creationDate: datetime(), mediaUrls: [], type: "text"});
    ```

4. **Creazione di relazioni tra utenti (follows)**:
    ```cypher
    MATCH (u1:User {userId: 1}), (u2:User {userId: 2})
    CREATE (u1)-[:FOLLOWS]->(u2);
    ```

5. **Creazione di relazioni tra utenti e post (posts)**:
    ```cypher
    MATCH (u1:User {userId: 1}), (p1:Post {postId: 1})
    CREATE (u1)-[:POSTS]->(p1);
    ```

6. **Creazione di relazioni tra post e commenti (comments)**:
    ```cypher
    MATCH (u2:User {userId: 2}), (p1:Post {postId: 1}), (c1:Comment {commentId: 1})
    CREATE (u2)-[:COMMENTS]->(c1)-[:ON]->(p1);
    ```

### Query di Analisi Base

1. **Visualizzare utenti e i loro post**:
    ```cypher
    MATCH (u:User)-[:POSTS]->(p:Post)
    RETURN u.username, p.content, p.creationDate;
    ```

2. **Visualizzare tutti i commenti su un post**:
    ```cypher
    MATCH (p:Post)<-[:ON]-(c:Comment)
    RETURN p.content, c.content;
    ```

3. **Conteggio like per ogni post**:
    ```cypher
    MATCH (u:User)-[:LIKES]->(p:Post)
    RETURN p.postId, COUNT(u) AS NumberOfLikes;
    ```

Questa rappresentazione del progetto e degli script fornisce un quadro d'insieme efficace senza entrare troppo nei dettagli tecnici.

