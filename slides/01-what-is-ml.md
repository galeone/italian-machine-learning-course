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

![face detection](images/face-detection.png)

---

Quando usiamo il nostro spartphone per inquadrare una persona, in real time vediamo la face detection in azione.

<br />

Ma come è possibile che questo accada?

<br />

Per un computer un'immagine non è altro che un insieme ordinato di vettori 3D (componenti RGB) posti uno accanto all'altro.

---
## Apprendere dai dati
<!-- sectionTitle: Apprendere dai dati-->

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

![dataset split](images/dataset-split.png)

---

- **Training set**: il subset da usare per allenare il modello
- **Validation set**: il subset da usare per misurare per performance del modello **durante** il training
- **Test set**: il subset da **non toccare mai** durante le fasi di training e validation, ma da usare **solo per la valutazione delle performance finale**.

---

### Epoche di training
<br />

Gli algoritmi di ML sono algoritmi iterativi che lavorano sul **training set**.

Ogni volta che il training set è stato osservato completamente dall'algoritmo, diciamo che è passata **un'epoca**.

---

## Spazi n-dimensionali

Gli spazi n-dimensionali sono un modo di modellare dataset contenenti esempi con **n** attributi ognuno.

Ogni esempio $e_i$ è completamente descritto dai suoi **n** attributi $ x_{j=0}, \cdots, x_{n-1} $.
<br />

$$ e_i = (x_0, x_1, \cdots, x_{n-1}) $$

---

Un'utile intuizione è quella di pensare ad ogni singolo esempio del dataset come se fosse **una riga in un dataset**, dove gli **attributi sono le colonne**.
<br />

**ESEMPIO**: un immagine 28 x 28 in scala di grigi ha esattamente 28 x 28 = 284 distinti attributi (colonne).

---

> Il concetto di dimensione si sviluppa nel momento in cui iniiamo a pensare agli esempi come se fossero punti in uno spazio **n**-dimensionale univocamente identificati dai loro attributi.

Pensando ai dati in questo modo, è possibile calcolare relazioni geometriche come la **distanza**.

---

## Iris Dataset

Per comprendere al meglio il concetto di dimensione, useremo il noto "Iris Dataset".

Il dataset contiene 3 classi, e 50 esempi per classe. La classe è il tipo di fiore. Gli attribtui sono tutti continui, ad eccezione per la classe/label.

---

- lunghezza del petalo (cm)
- altezza del petalo (cm)
- lunghezza del sepalo (cm)
- altezza del sepalo (cm)
- classe: setosa, versicolor, virginica

![versicolor](images/versicolor.jpg)

---

**Question time**: quante dimensioni ha questo dataset?

---

Avendo ogni esempio 4 attributi (più l'informazione della classe) è già difficile visualizzare tutta l'informazione assieme sullo stesso grafico.

<br />

Come visualizziamo 4 dimensioni sullo stesso grafico? E invece 284?

<br />

---

Per un dataset a bassa dimensionalità come l'Iris, possiamo ricorrdere ad una tecnica **manuale** di visualizzazione dei dati, che che ci permette di avere un'idea del dataset con il quale stiamo lavorando.

Come prima cosa, assegniamo un colore distinto ad ogni diversa classe:

- Setosa = blu
- Versicolor = verde
- Virginica = rosso

E successivamente visualizziamo le relazioni tra le features **a coppie**.

---

![iris 1](images/iris1.png)

---

![iris 2](images/iris2.png)

---

Quest'ultimo grafico, mostra che **esistono tre partizioni naturali (cluster)** nel dataset e che per trovarle possiamo usare i soli due attributi "petal widht" e "petal lenght".

<br />

*Ma tutto questo è stato fatto in maniera manuale e "visiva".*

---

> L'obiettivo degli algoritmi di classificazione è di apprendere autonomamente quali sono le **feature** (caratteristiche, dimensioni) discriminative, così da **apprendere una funzione** in grado di classificare correttamente elementi apparteneti a classi differenti.

---

## Apprendimento Supervisionato
<!-- sectionTitle: Apprendimento Supervisionato -->

![supervised learning](images/supervised-learning.png)

---

### Modelli parametrici e non parametrici

<br />

È possibile classificare gli algoritmi di machine learning (supervisionato e non) in base alla presenza di **parametri apprendibili** o meno, all'interno del modello.

- **Algoritmi non parametrici**: sono una maniera classica di affrontare il problema di classificazione/regressione. Il più comune algoritmo di non parametrico è il **k-NN** (k-Nearest-Neighbours).
- **Algoritmi parametrici**: hanno bisogno di un processo di **train** durante il quale **modificano il valore dei loro parametri** per adattarsi al dataset e risolvere il task.

---

### L'algoritmo k-NN

L'algoritmo si basa sul concetto di **distanza**.

Per classificare un nuovo elemento (punto p), abbiamo bisogno di misurare la **distanza** di p rispetto a **ogni elemento del dataset**.

$$ || p - q_i || = \left( \sum_{j=0}^{D-1}|p_{j}-q_{i,j}|^{p}\right)^\frac{1}{p} $$

---

- Quando k-NN è applicato a problemi di classificazione, il punto p viene classificato in base al voto dei syou k vicini
- Quand k-NN è applicato a problemi di regressione, l'output dell'algoritmo è la media dei k-NN.

---

### Modelli parametrici

<br />

Dato un valore di input $x = (x_0, x_1, \cdots, x_n)$ e la sua label associata $y$, definiamo modello parametrico la funzione $f_\theta$ dove $\theta$ è l'insieme dei parametri da cambiare durante la fase di training per "adattarsi ai dati" (fit the data).

---

L'esempio più semplice ed intuitivo di modello parametrico è la **regressione lineare**.

![linear regression](images/linear-regression.png)

---

Questo modello tenta di modellare la relazione tra due variabili (dipendente y, e indipendente x), "fittando" l'equazione di una retta ai dati osservati.

$$ f_\theta: y = mx + b $$

I parametri sono $ \theta = \{m,b\} $

<br />

**Question time**: che assunzioni stiamo facendo sui dati?

---

Il metodo **iterativo**, standard de-facto, per trovare i valori dei parametri è il **metodo dei minimi quadrati**.

Questo metodo calcola la linea che "meglio fitta" i dati, **minimizzando** la somma dei quadrati delle distanze tra i punti e la linea stimata all'iterazione precedente.

---

> L'obiettivo degli algoritmi di apprendimento supervisionato, è quello di iterativamente "aggiustare" i parametri $ \theta $ in modo tale che $f_\theta$ modelli correttamente il _fenomeno osservato_.

---

Modellare un fenomeno usando un modello parametrico con una equazione nota è OK quando abbiamo la certezza che i il fenomeno abbia un andamento lineare e le variabili da considerare siano solo 2.

---

Ma se il numero di variabili (le dimensioni del dataset) è molto maggiore, e non abbiamo alcuna informazione su come i dati si dispongano (se linearmente, o esponenzialmente, o formino cluster, ...) usare un modello di questo tipo **non** porta a buoni risultati.

---

In questi casi, modelli con un numero **molto grande di parametri** come le **reti neurali** possono essere usati, in quanto questi modelli sono **approssimatori universali** in gradi di modellare ogni funzione, e quindi apprendere una funzione incognita che fitti il dataset.

---

Usare modelli con molti parametri può sembrare la soluzione perfetta, ma nella pratica, avere modelli molto flessibili può portare a risultati patologici come l'**overfitting**.

---

#### Condizioni patologiche

![over-under](images/over_under.png)

---

<!--- TODO: metriche? --->

---

---

### Loss function

La funzione che lega i dati osservati e quelli predetti, è detta **loss function** (funzione perdita).

L'obiettivo di ogni algoritmo di machine learning espresso come algoritmo di ottimizzazione (come vedremo a breve) è quello di **minimizzare la perdita**.

---
