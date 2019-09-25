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

![recsys](images/recsys-amazon.png)

---

### Plate Recongnition

![plate](images/plate-recognition.jpg)

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

> Il concetto di dimensione si sviluppa nel momento in cui iniziamo a pensare agli esempi come se fossero punti in uno spazio **n**-dimensionale univocamente identificati dai loro attributi.

Pensando ai dati in questo modo, è possibile calcolare relazioni geometriche come la **distanza**.

![cube](images/n-cube.png)

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

![knn](images/knn.jpg)

---

- Quando k-NN è applicato a problemi di classificazione, il punto p viene classificato in base al voto dei suoi k vicini
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

![linear regression error](images/linear-regression-error.png)

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

### Condizioni patologiche

![over-under](images/over_under.png)

---

<!-- sectionTitle: Misurare le performance: le metriche-->
## Misurare le performance: le metriche

---

Misurare le performance di un algoritmo di apprendimento supervisionato durante la fase di validazione e test è parte **essenziale** di ogni pipeline di ML ben fatta.

<br />

- È possibile misurare le performance del modello su ogni split del dataset
- Al termine di ogni epoca è raccomadabile misurare le performance sul dataset di train e validation
- Le metriche misurate sui diversi dataset vanno rappresentate sullo **stesso grafico**
- Le differenze tra le performance di train e validation ci indicano se il modello soffre di condizioni patologiche.

---

Gli algoritmi di apprendimento supervisionato hanno l'**enorme vantaggio** di avere all'interno del dataset **le label** e le metriche usano le label per esprimere *"quanto bene"* l'algoritmo sta apprendendo.

La prima metrica presentata è l'accuratezza (accuracy).

---

#### Accuracy

<br />

L'accuracy è esattamente quello che la parole stessa esprime: quanto accurato il modello è stato nel predire il risultato corretto.

<br />

![formula](images/accuracy.png)

<br />

**Question time**: l'accuracy è una buona metrica se il dataset è sbilanciato?

*Un dataset è sbilanciato quando il numero di elementi per classe è molto diverso*

---

#### Confusion matrix

<br />

È una rappresentazione tabellare delle performance di un classificatore.

![confusion matrix](images/confusion-matrix.gif)

La matrice di confusione **non è una metrica**, ma è uno strumento necessario per calcolare altre metriche.

---

La matrice di confusione contiene:

<br />

- **TP** (True Positives): Tutte le istanze di A classificate come A
- **TN** (True Negatives): Tutte le non istanze di A non classificate come A
- **FP** (False Positives): Tutte le non istanze di A classificate come A
- **FN** (False Negatives): Tutte le istanze di A non classificate come A

---

#### Precision

<br />

La precision è un numero in $[0,1]$ che misura quanto è accurato il classificatore.

<br />

$$ \frac{TP}{TP + FP} $$

---

#### Recall

<br />

La recall è un numero in $[0,1]$ che misura la percentuale di elementi correttamente classificati, sul totale degli elementi di quella classe.

<br />

$$ \frac{TP}{TF + FN} $$

---

#### Mean absolute error

MAE (errore medio assouto) è la media delle differenza assolute tra il valore (classe, o valore numerico) reale e quello predetto.

È una metrica applicabile anche ai classificatori, ma usualmente viene usata per i **regressori**.

<br />

$$ \frac{1}{N} \sum_{i=1}^{N}{|y_i - \hat{y}_i|} $$

<br />

Il suo valore è tra $[0, \infty]$.

---

#### Mean squared error

<br />

MSE (errore quadratico medio) è la media delle differenze al quatrato tra il valore reale e quello predetto.

<br />

$$ \frac{1}{N} \sum_{i=1}^{N}{(y_i - \hat{y}_i)^{2}} $$

<br />

Il suo valore è tra $[0, \infty]$.

---

Metriche come **MAE** e **MSE** esprimono una relazione diretta tra valori reali e valori predetti.

Questa relazione è, solitaente, anche l'obiettivo che vogliamo **minimizzare** durante il processo di **ottimizzazione**.

----

#### Loss function

La funzione che lega i dati osservati e quelli predetti, è detta **loss function** (funzione perdita).

L'obiettivo di ogni algoritmo di machine learning espresso come algoritmo di ottimizzazione (come vedremo a breve) è quello di **minimizzare la perdita**.

<br /> <br />

Dopo questa introduzione ai *concetti fondamentali* del Machine Learning, possiamo dedicarci al modello più diffuso ed utilizzato, le reti neurali, e comprendere come il processo di apprendimento di questo modello parametrico viene effettuato.

---

<!-- sectionTitle: Reti Neurali -->

## Reti Neurali

---

### Neuroni biologici e artificiali

![neuronz](images/biological-artificial.png)

---

- **Dendriti**: numero di input che il neurone accetta; dimensione del dato di input.
- **Sinapsi**: i pesi associati ai dendriti. Questi sono i **parametri** che cambiano durante la fase di training.
- **Assone**: è il valore di output, dopo essere stato processto dal nucleo.
- **Nucleo**: (prossima slide)

---

#### Nucleo

<br />

Una funzione che lega l'input con i pesi associati alle sinapsi. Per simulare il comportamento del neuorne biologico (attivarsi con determinati stimoli di input), il nucleo è modellato usando una **funzione non lineare** $f$.

<br />

$$ O = f \left(\sum_{i=0}^{D-1}{x_i w_i + b}\right) $$

---

#### Non linearità

Un percettrone (perceptron), è una rete neurale composta da diversi neuroni **lineari**.

Un pereptron può classificare esempi in uno spazio D-dimensionale **se e solo se** gli esempi sono linearmente separabili (apprendere un iperpiano decisionale).

La **non linearità**, invece, **trasforma** l'iperpiano in una generica **ipersuperficie**.

---

![non-linear](images/activation_fns.png)

---


##### Il bias

Spesso dimenticato, ma **di fondamentale importanza**, è il termine che permette di apprendere (nel caso lineare) iperpiani **non centrati nell'origine**.

![no bias](images/no-bias.png)

---

![yes bias](images/yes-bias.png)

---

#### Perché le reti neurali?

A differenza dei metodi tradizionali, le reti neurali sono estremamente **flessibili**.

Un singola rete neurale (input -> rete -> output) è in grado al massimo di trovare una singola ipersuperfificie, e quindi apprendere un solo decision boundary.

![single-layer](images/single-layer.png)

---

Mettendo in cascata (**creando una rete deep**) diversi layer di neuoroni, è possibile (layer dopo layer) trasformare e combinare i diversi confini decisionali appresi, fino all'apprendimento di una funzione in grado di separare correttamente i dati.

---

#### Importante

Le reti neurali sono approssimatori di funzioni universali.

Apprendiamo, quindi **una funzione** che può essere vista come una generica **trasformazione** da un dominio (ad una determinata dimensione), ad un altro (solitamente ad una dimensione ridotta).

<br />

Apprendere trasofmrazioni da uno spazio all'altro e **molto potente** in quanto permette di **ridurre la complessità** dei problemi, trasferendoli da un dominio altamente dimensionale ad uno bassa dimensionalità.

---

### Reti complementamente connesse

![multi-layer](images/multi-layer.png)

---

$$ x = \begin{pmatrix}x_0\\ x_1 \\ \cdots \\ x_{D-1} \end{pmatrix} , W \in \mathbb{M}_{M \times D-1} , b = \begin{pmatrix}b_0\\ b_1 \\ \cdots \\ b_{M-1} \end{pmatrix} $$

<br />

L'output di un layer complemtamente connesso che **trasforma** un input **D-dimensionale** in un valore **M-dimensionale** è dato da:

<br />

$$ O = f(Wx + b) $$

---

## Ricapitoliamo

- Il dataset è composto da dati, che possono essere visti come punti in uno spazio D-dimensionale.
- Un percettrone è in grado di separare correttamente solo dati che sono linearmente separabili.
- Aggiungere la non linearità rende il percettrone in grado di separare dati non linearmente separabili, ma **deforma il confine decisionale**.
- Mettere in cascata (**rete deep**) più layer di neuorni, permette di **ridurre la dimensionalità**, e apprendere migliori confini decisionali.
- È possibile variare la **topologia** delle reti (come vedremo).

---

> Dopo aver definito i dati e l'architettura: come possiamo allenare la nostra rete per apprendere la funzione incognita?

---

## Apprendimento ed ottimizzazione

---

### La loss function

È una funzione usata per mettere in relazione **l'output del modello** con la **predizione desiderata**.

<br />

Di loss function "standard" ne esistono diverse, ognuna delle quali influenza la qualità delle predizioni del modello.

---

Per un problema di **classificazione** su $ M $ classi distinte, possiamo modellare la rete neurale come una funzione che dato un input D-dimensionale produce un vettore M-dimensionale di predizioni, in funzione dei suoi parametri $W$.

<br />

$$ \hat{y} = F_W(x) : \mathbb{R}^D \rightarrow \mathbb{R}^{M} $$

---

Ottenere la **label predetta** a partire dal vettore M-dimensionale è banale:

<br />

$$ \hat{l} = \argmax_{0 \le i \le M-1}{\hat{y}_{i}} $$

<br />

Ma come possiamo specificare (dare in pasto alla loss function) la label presente nel dataset per il dato di input?

---

Si potrebbe usare direttamente il valore della label stessa (non fatelo).

<br />

Oppure si può **codificare** la label usando la rappresentazione 1-hot. (1-hot encoding).

$$ y = \begin{pmatrix}y_0\\ y_1 \\ \cdots \\ y_{M-1} \end{pmatrix} : y_i = \begin{cases} 1, &\text{se i = posizione assegnata a l} \\ 0, &\text{altrimenti} \end{cases} $$

---

La formulazione generale della loss function tra valore predetto $\hat{y}$ e valore reale in codifica one-hot $y$ è:

<br />

$$ \mathcal{L}_i (y, \hat{y}): \mathbb{N}^{M} \times \mathbb{R}^{M} \rightarrow \mathbb{R} $$

<br />

Per un dataset di $k$ elementi, il valore della loss è il valore medio:

<br />

$$ \mathcal{L}(F;\text{dataset}) = \frac{1}{k}\sum_{i=1}^{k}{\mathcal{L}_{i}(y, \hat{y})} $$

---

La formulazione della loss dipende dal problema, ma la più intuitiva (e frequentemente utilizzata) tra le loss è la **distanza euclidea** (L2 loss).


$$ \mathcal{L} = \frac{1}{k}\sum_{i=1}^{k}{||\hat{y}_i - y_i ||_{2}} $$

---

### Ottimizzazione

<br />

La ricerca operativa ci offre metodi per trovare la soluzione di un problema di ottimizzazione dove la funzione da ottimizzare ha caratteristiche ben definite (e.g. è convessa).

<br />

Le reti neurali sono approssimatori universali, quindi non possiamo fare alcuna considerazione che sfrutti la geometria della funzione.

Di conseguenza...

---

> Non è possibile usare i tradizionali metodi offerti dall ricerca operativa per ottimizzare (minimizzare) la loss function.
>
> È dunque necessario procedere alla ricerca della soluzione in maniera **iterativa**, partendo da una soluzione iniziale e rifinendola ad ogni step (fase di train del modello).

---

Abbiamo due alternative per ricercare l'ottimo della funzione:

<br />

1. **Perturbazioni casuali**: si applica una perturbazione $\Delta W$ al set di parametri corrente, si valuta il valore della loss dopo aver applicato la perturbazione $L(\text{dataset}, W + \Delta W)$ e se il valore è minore del precedente, si aggiornano i parametri.

2. **Stima della direzione dell'aggiornamento**: anziché generare un nuovo set di parametri in maniera causauale, è possibile **guidare** il processo di ricerca dell'ottimo nella **direzione di massima discesa della funzione**.

<br />

La soluzione iniziale del problema è il set di parametri $W$ della rete neurale.

---

### Scelta della soluzione iniziale

<br />

Non esiste un unico modo di inizializzare i parametri, ma esisono due suggerimenti che ogni inizializzazione deve rispettare:

<br />

- **Non inizializzare i parametri a zero**: rende impossibile trovare una nuova soluzione usando gradient descent (vedi dopo)
- **Rompere la simmetria**: due hidden units (neuroni nello stesso layer) che condividono lo stesso input devono essere inizializzati con **valori diversi**.

---

### Gradient Descent

<br />

Per una funzione in una variabie, l'operazione di derivata ci descrive il comportamento della funzione $f$ valutata in un intorno infinitamente piccolo centrato su $x$.

<br />

$$ \frac{d f(x)}{dx} = \lim_{h \rightarrow 0}\frac{f(x + h) - f(x)}{h} $$

<br />

La generalizzazione dell'operazione per una funzione a n-variabili è data dal gradiente:

$$ \nabla \mathcal{L}(W) = (\frac{d L}{d w_1}, \cdots, \frac{d L}{d w_n}) $$

<br />

Il gradiente indica **la direzione lungo la quale la funzione cresce**, quindi:

<br />

$$ d = - \nabla \mathcal{L}(W) $$

---

## Batch Gradient Descent

La regola di **aggiornamento dei parametri** diventa dunque:

<br />

$$ W \leftarrow W - \mu \nabla \mathcal{L}(\text{dataset}; W) $$

dove $\mu$ è il **learning rate**.

Il learning rate è un **iperparametro** e sceglierlo è **difficile**.


---

## Mini-batch Gradient Descent

Anziché calcolare il valore della loss function su tutto il dataset (difficilamente applicabile nella realtà, quando i dataset sono enormi), la loss si calcola iterativamente su dei mini-batch (di cardinalità $b$).

<br />

$$ W \leftarrow W - \mu \nabla \mathcal{L}((x_{[i, i+b]}, y_{[i, i+b]}); W) $$.

---

## Algoritmi di ottimizzazione

Esisono diversi algoritmi di ottimizazione, i quali differiscono per la regola di aggiornamento dei parametri.

- **Vanilla Gradient Descent**: (precedentemente spiegato), stima la direzione dell'aggiornamento usando il gradiente e applica aggiornamenti "grandi tanto quanto il learning rate".
- **Momentum update**: "limita" la dimensione dell'aggiornamento usando un termine di "attrito" 
- E molti altri (la loro descrizione va oltre la complessità del corso).

![update-surface](images/update-surface.png)

---

![cool](images/loss_surface.gif)

Per approfondire [Algoritmi di ottimizzazione per il training delle reti neurali](https://talks.pgaleone.eu/Algoritmi%20di%20ottimizzazione%20per%20il%20training%20delle%20reti%20neurali/optalgo.slide#1)

---

## Domande

1. Dataset split: quali e perché.
2. Cos'è un epoca?
3. Differenze tra modelli parametrici e non parametrici.
4. Descrivi l'algoritmo k-NN.
5. Overfitting e underfitting: sono condizioni patologiche, perché? Quando si verificano?
6. La matrice di confusione è una metrica?
7. Cosa misurano precision e recall?
8. Descrivi la struttura (usando la formula) di un neurone artificiale.
9. Perché la non linearità è importante?
10. Il termine di bias, perchè è necessario inserirlo?
11. Reti neurali completamente connesse: cosa accade layer-dopo-layer all'input?
12. Loss function: perché è necessaria? Cosa misura?
13. Soluzione iniziale al problema di minimizzazione: che regole seguire?
14. Descrivi la regola di aggiornamento "vanilla", nel caso batch e mini-batch.

---

Introduzione a TensorFlow 2.0 e TensorFlow Datasets

- Colab: https://bit.ly/2lno7O5
