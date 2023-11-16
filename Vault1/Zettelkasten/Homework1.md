Date: 2023-11-07
Time: 10:39
Tags: #ML #Università 
Up: [[ML]]

---
# Homework1

## Cose da fare:

- [ ] Fare un codice approssimativo
- [ ] Fare dei grafici per vedere la distribuzione del dataset
- [ ] Fare un controllo sugli outlines
- [ ] Controllare il bilanciamento delle classi di output
- [ ] Grafici di correlazione tra le features
- [ ] Matrice di correlazione per vedere pattern tra le features
- [ ] Aggiungere il post-pruning, già scritto in daAggiungere.ipynb
- [ ] 


1. **Esplorazione dei dati**:
    - Calcola statistiche descrittive del tuo dataset (media, mediana, deviazione standard, ecc.).
    - Esamina la distribuzione delle classi nelle etichette di output per capire se ci sono sbilanciamenti.
    - Visualizza la correlazione tra le features per identificare eventuali relazioni.
2. **Pre-elaborazione dei dati**:
    - Gestisci i dati mancanti, se presenti, scegliendo la strategia più adatta (rimozione, imputazione, ecc.).
    - Normalizza o standardizza le features se necessario.
    - Tratta eventuali outliers.
3. **Caratteristiche aggiuntive o ingenieria delle caratteristiche**:
    - Crea nuove features che potrebbero essere più informative per il tuo problema.
    - Esegui la selezione delle caratteristiche se hai molte features e vuoi ridurre la complessità del modello.
4. **Esperimenti con diversi modelli**:
    - Prova diversi algoritmi di classificazione (al di fuori degli alberi decisionali) per vedere come si comportano rispetto al tuo problema.
    - Sperimenta con diverse configurazioni di iperparametri per migliorare le prestazioni dei modelli.
5. **Validazione incrociata**:
    - Utilizza la validazione incrociata per ottenere stime più robuste delle prestazioni del modello.
    - Esplora tecniche di cross-validation come la K-fold cross-validation.
6. **Ottimizzazione degli iperparametri**:
    - Utilizza metodi di ottimizzazione degli iperparametri come la ricerca casuale o la ricerca in griglia per trovare la combinazione migliore.
7. **Confronto tra modelli**:
    - Confronta le prestazioni dei diversi modelli utilizzando metriche appropriate (precision, recall, F1-score, ROC-AUC, ecc.).
8. **Interpretazione del modello**:
    - Seleziona un modello interpretabile (come un albero decisionale) e interpreta le sue decisioni.
    - Utilizza tecniche di spiegazione del modello per comprendere meglio come il modello prende le sue decisioni.
9. **Valutazione delle prestazioni su dati di test**:
    - Riserva un insieme di dati di test separato e valuta le prestazioni del modello su questo insieme solo alla fine.
10. **Documentazione**:
    - Assicurati di documentare il tuo processo decisionale, le scelte di pre-elaborazione, i modelli testati e i risultati ottenuti.


---
# Soluzione

## Introduction
The problem presented is a classification problem, over 2 dataset to train the model, and 2 test, to evaluate the result obtained by the training. The first dataset contains 50000 elements with 100 parameters.  

## First Test
The first step taken to work on this homework works on finding a solution. To see if everything was well managed I try to train and test the dataset over a random method. The test is made over the dataset1. In particular I split the data to create 2 set, one for the training and one for the test. Doing so, I could evaluate the result, in order to generate an appropriate model for the blind test. I didn't think about a pre-processing method, I could use a dataset standardization, or check the outlines to see if I could improve the distribution to get a better solution. Avoiding every kind of simplification, or improvements, I just run the code over the DecisionalTree() method, obtaining a proper solution. Just to verify the correct evaluation over the test, I measured the accuracy: 0.976036, which is very close to the average result I was obtaining, I take this as point of start to improve the code. It's quite good considering the condition already explained before. 

Since I created a base, now I can start to decorate and develop a more complex code.
First of all I want to understand how the data are distributed, so I can represent them in a graphical way. Since there was an enormous amount of data I have randomly token a small amount of data for each set, to be more graphically understandable:
![[Pasted image 20231116220434.png]] 


Another method to evaluate a classification problem is using a confusion matrix, to understand, beyond the correct result, if there are more or less false positive or false negative and if the model tends to confuse 2 or more classes. The matrix shows that the evaluation is good, but it can be improved.
![[Pasted image 20231116181213.png]]


I applied standardization to ensure that all features share similar scales, with a mean centered around 0 and a standard deviation of 1. This choice was motivated by the need to enhance the performance and convergence of different machine learning algorithms, especially those that can be influenced by variations in the scale of input features.

Using Classification report I can access to more accurate performance information getting:
![[Pasted image 20231116230144.png]]



---
# References
