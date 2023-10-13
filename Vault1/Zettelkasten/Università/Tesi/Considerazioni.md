**Considerazioni**

Nota bene (cose da ricordare):
- La struttura a bus

- Dovrebbe considerare due aree di servizio eterogenee "elettricamente connesse", ad esempio una con solo turbina eolica e l'altra con fotovoltaico e storage. Ottiene questo risultato modificando opportunamente la formalizzazione della Bianchi. 
  Praticamente abbiamo due aree:
	1. sistema di stazioni (per semplificare immaginiamone una sola), collegato al fotovoltaico e ad uno storage
	2. sistema di stazioni (per semplificare immaginiamone una sola), collegato ad una turbina 
- Dovrebbe modificare la funzione obiettivo per cercare di stabilire un bilanciamento tra le due aree di servizio, che naturalmente avranno degli input eterogenei, sia per quanto riguarda la domanda di potenza dai veicoli, sia per quanto riguarda la sorgente di energia. 
- L'ipotesi da lei citata di controllare la domanda è legittima. La potenza di domanda complessiva, trattata dalla Bianchi come un segnale dato non modificabile (nel gergo dell'automatica un disturbo) potrebbe essere scomposta in due componenti controllate $\hat u^{ev} = \hat u_1^{ev} + \hat u_2^{ev} = \alpha \cdot \hat u^{ev} + (1-\alpha) \cdot \hat u^{ev}$. Potrebbe così introdurre e determinare un nuovo controllo $\alpha(t)$ in base allo stato delle due aree di servizio.

- [x] Capire il codice di Millie
- [x] Commentare il codice di Millie
- [x] Creare una copia del setup
- [x] Modificare il secondo setup con 2 aree di servizio
