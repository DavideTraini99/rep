
## Progetto Spring Boot 

Il progetto proposto consente di ricercare file in base al nome, alla data di modifica o al tipo di file (png, jpg, jpeg, tiff) ricevendo statistiche riguardo la dimensione. 

Nel nostro caso il Client è Postman che consente, grazie a chiamate di tipo GET, di inserire parametri di ricerca ed ottenere gli elementi desiderati sotto forma di JSON.

Una volta avviato il programma, il servizio sarà disponibile all'indirizzo http://localhost:8080/

I dati in ingresso sono stati prelevati grazie alle API di dropbox 
 - #file-search
 - #files-get_metadata

La prima restituisce un oggetto di tipo JSONObject contenente un JSONArray relativo a più elementi, mentre la seconda restituisce un  JSONObject relativo ad un unico elemento.
Perciò è stato necessario creare un file (https://github.com/MarcoP1999/OOPproject/blob/master/src/JSONPath.txt)  contenente i path relativi a diversi elementi salvati nell'account Dropbox utilizzato e scritti sotto forma di JSONArray. 
È stato poi generato un ciclo per scorrere il JSONArray e sfruttare i path contenuti per iterare la chiamata a get_metadata la quale restituisce il JSONObject relativo ad ogni elemento del JSONArray; ogni elemento restituito è poi stato inserito all'interno di un JSONArray che sarà successivamente utilizzato per l'elaborazione.
Proprio per questo motivo sono state create due classi distinte per l'elaborazione dei dati, una che presenta i metodi per lavorare con un JSONObject, l'altra con metodi relativi ad un JSONArray.


Per quanto riguarda la ricerca di elementi si possono quindi distinguere ricerche su oggetti restituiti da "search" e ricerche su oggetti restituiti da "get_metadata". 
Perciò la tipologia di JSONObject è diversa in base a quale dato si analizza 
 

**get_metadata:**

 1. ***(GET) search_tipo_dimMeta?corpo="formato"&corpo="operatore"&corpo="dimensione"***
Restituisce il JSON contenente tutti gli elementi che rispettano il formato e la dimensione (passati come parametri). Riporta inoltre dimensione media (geometrica e aritmetica), minima e massima dei file cercati.

 2. ***(GET) search_tipo_dim_altezzalarghezzaMeta?corpo="formato"&corpo="operatore"&corpo="altezza"&corpo="larghezza"&corpo="operatore"&corpo="dimensione"***
Restituisce il JSON contenente tutti gli elementi che rispettano formato, altezza, larghezza e dimensione (passati come parametri).  Riporta inoltre dimensione media (geometrica e aritmetica), minima e massima.



 3. ***(GET) search_dataMeta?corpo="data"&corpo="data"***
Restituisce il JSON contenente tutti gli elementi modificati dal Client in una data compresa tra le due passate come parametri.
 
 5. ***(GET) search_nomeMeta?body="nomefile"***
Restituisce il JSON contenente tutti gli elementi che hanno nome (o parte iniziale di esso) uguale a quello passato come parametro.



**search**

 

 1. ***(GET) search_tipo_dim?corpo="formato"&corpo"operatore"=&corpo="dimensione"***
Restituisce il JSON contenente tutti gli elementi che rispettano il formato e la dimensione (passati come parametri). Riporta inoltre dimensione media (geometrica e aritmetica), minima e massima
dei file cercati.

 3. ***(GET) search_data?corpo="data"&corpo="data"***
Restituisce il JSON contenente tutti gli elementi modificati dal Client in una data compresa tra le due passate come parametri.

 3. ***(GET) search_nome?body="nomefile"***
Restituisce il JSON contenente tutti gli elementi che hanno iniziale del nome (o nome completo) uguale a quello passato come parametro.


Abbiamo deciso di non utilizzare un Model in cui immagazzinare gli elementi più rilevanti, ma di andare a lavorare direttamente con il JSON ricevuto dopo il parsing. 
L'abbiamo fatto per una successiva verifica: dopo aver elaborato i dati, essi sono stati copiati in un file per una seconda rielaborazione, così da verificare l'effettiva possibilità di reinterpretare i dati restituiti dal nostro web service. 

    

> ## **Diagramma Casi D'uso**

![enter image description here](https://github.com/MarcoP1999/OOPproject/blob/master/src/UML/NewModel%20Use%20Case%20Diagram1.jpg)



> ## **Diagramma Classi**

 - **univpm.progetto.controller**
![enter image description here](https://github.com/MarcoP1999/OOPproject/blob/master/src/UML/Diagramma_Classi/Controller.png)

 - **univpm.progetto.elaborazione** ![enter image description here](https://github.com/MarcoP1999/OOPproject/blob/master/src/UML/Diagramma_Classi/elaborazione.png)
 - **univpm.progetto.exception**![enter image description here](https://github.com/MarcoP1999/OOPproject/blob/master/src/UML/Diagramma_Classi/Exception.png)
- **univpm.progetto.filtri_e_statistiche**
![enter image description here](https://github.com/MarcoP1999/OOPproject/blob/master/src/UML/Diagramma_Classi/Filtri_Statistiche.png)
- **univpm.progetto.Json**
![enter image description here](https://github.com/MarcoP1999/OOPproject/blob/master/src/UML/Diagramma_Classi/JSON.png)
 - **univpm.progetto.verifiche**![enter image description here](https://github.com/MarcoP1999/OOPproject/blob/master/src/UML/Diagramma_Classi/verifica.png)

> ## **Diagramma di Sequenza**



## Ricerca su meta:


 - **data_Meta**



![enter image description here](https://github.com/MarcoP1999/OOPproject/blob/master/src/UML/Diagramma_sequenze/sequenze_data_meta.png)
 - **nome_Meta**

![enter image description here](https://github.com/MarcoP1999/OOPproject/blob/master/src/UML/Diagramma_sequenze/sequenze_nome_meta.png)
 - **dim_Meta**



![enter image description here](https://github.com/MarcoP1999/OOPproject/blob/master/src/UML/Diagramma_sequenze/sequenze_dim_meta.png)
 - **alt_largh_Meta**



![enter image description here](https://github.com/MarcoP1999/OOPproject/blob/master/src/UML/Diagramma_sequenze/sequenze_alt_largh_meta.png)

## Ricerca su search:
 - **data**

![enter image description here](https://github.com/MarcoP1999/OOPproject/blob/master/src/UML/Diagramma_sequenze/sequenze_data_search.png)
 - **nome**


![enter image description here](https://github.com/MarcoP1999/OOPproject/blob/master/src/UML/Diagramma_sequenze/sequenze_nome_search.png)
 - **dim**


![enter image description here](https://github.com/MarcoP1999/OOPproject/blob/master/src/UML/Diagramma_sequenze/sequenze_dim_search.png)


## Autori

 - **Proietti Marco**  - [Link GitHub](https://github.com/MarcoP1999)
 - **Traini Davide** -  [Link GitHub](https://github.com/DavideTraini99)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkzMzAxMDIwNSwtMTU4MDg1NjgwOCwtOT
ExNDQyNTAsMTM5NDA5OTM0NiwxODUzOTkxODQ3LC0xMTE5NDgx
Njc5LC01NzgyNzM1NjksMTU2ODQxNjg4OSwxNDExOTk0NTgxLD
EzOTg4ODYyNDQsLTgxOTQ2NzY2MCwtMTE2MDE2NDk4MCwtMTY2
MTQwODg4NSw5NTk2MTY2NzQsMTM1NzI0NjI1LDE0OTgwNDIwNz
gsLTY5MTIxMjIxMiwyNjI2MjIyMTcsLTI0MzIwOTk4OSw1NTkw
NzMwNTRdfQ==
-->