<!-- classes: title -->

# Prima Parte

---

- Cos'è il machine learning e l'importanza del dataset
- Le reti neurali come modello di apprendimento universale
- Apprendimento come processo di ottimizzazione
- Discesa del gradiente per ricercare la soluzione
- Ottimizzatori

---

## Cos'è il Machine Learning?

> Il Machine Learning è un ramo dell'intelligenza artificiale in cui vengono definiti algoritmi con lo scopo di estrarre informazioni signficative dai **dati**

---

<!-- sectionTitle: Applicazioni -->
## Applicazioni

Le applicazioni del Machine Learning sono infinite. Siamo circondati da applicazioni intelligenti e probabilmente non ce ne rendiamo nemmeno conto.

---


### Sistemi di raccomandazione

TODO

---

### Plate Recongnition

TODO

---

### Face Detection

![](/images/face-detection.png)

---

Quando usiamo il nostro spartphone per inquadrare una persona, in real time vediamo la face detection in azione.

<br />

Ma come è possibile che questo accada?

<br />

Per un computer un'immagine non è altro che un insieme ordinato di vettori 3D (componenti RGB) posti uno accanto all'altro.

---

L'algoritmo (**modello**) usato dall'applicazione è stato **allenato** per identificare un **pattern** (il volto).

Il modello ha **appreso**, dopo aver visto migliaia di volte migliaglia di **esempi etichettati**, che ad un certo input corrisponde quello che noi chiamiamo volto.

<br />

Gli algoritmi di questo tipo appartengono alla famiglia dell'**apprendimento supervisionato**.

---

## Tassonomia degli algoritmi di ML

- Apprendimento **supervisionato**
- Apprendimento **non supervisionato**
- Apprendimento **semi-supervisionato**

<br />

In questo corso tratteremo *esclusivamente* gli algoritmi di apprendimento **supervisionato**.

---

Ogni categoria di algoritmi ha le sue peculiarità, ma tutti condividono lo steso obiettivo: **apprendere dai dati**.

<br />

Per questo motivo, **i dati** sono la parte **più importante** di ogni algoritmo di Machine Learning.

---

<!-- sectionTitle: Il dataset -->
## Il dataset

<!-- note
dato che il dataset è così importante, è bene diventare familiari con alcuni concetti che rigaurdano la sua struttura, ed il suo utilizzo.
-->

---

Un dataset altro non è che una collezione di dati:

<br />

$$ \text{dataset} = \left\{(e_i, l_i)\right\}^{k}_{i=1} $$

<br />

- $k$ è il numero di elementi del dataset
- $e$ è l'esempio (immagine, tupla di numeri, ...)
- $l$ è la label associata all'esempio

<br />

Il dataset è l'insieme **totale** dei dati a nostra dispozione.

---

Un algoritmo di ML deve *"osservare"* i dati molte volte per poter apprendere quali caratteristiche (**features**) presenti nei dati sono utili per risolvere il **task** (e.g. classificazione).

<!-- note
Esempio cani e gatti - classificazione.
-->

<br />

**Question time**: Possiamo usare lo stesso dataset per allenare il modello e misurare le performance del modello stesso?

---

### Dataset Split

![](images/datset-split.png)

---

- **Training set**: il subset da usare per allenare il modello
- **Validation set**: il subset da usare per misurare per performance del modello **durante** il training
- **Test set**: il subset da **non toccare mai** durante le fasi di training e validation, ma da usare **solo per la valutazione delle performance finale**.

---

## Apprendimento Supervisionato
<!-- sectionTitle: Apprendimento Supervisionato -->

![](/images/supervised-learning.png)

TODO

## 
