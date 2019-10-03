<!-- classes: title -->

# Terza Parte

---

- Reti Neurali Convoluzionali (Convolutional Neural Networks)
- Migliorare il classificatore di immagini usando le CNN
- Introduzione all'object detection
- Implementazione di un classificatore e localizzatore di oggetti

---

<!-- sectionTitle: Convolutional Neural Networks -->

## Convolutional Neural Networks

---

Le reti neurali convoluzionali (CNN) sono i blocchi fondamentali di ogni applicazione di machine learning moderna. Sono utilizzate per:

- image classification
- object detection
- object detection and classification
- semantic segmentation
- generative models (audio/video/image)
- ...

---

### Image classification


![cat](images/cat.png)

---

### Object Detection and Classification

![cat](images/detect-cat.png)

<br />

(anche singolarmente)

---

### Semantic Segmentation


![sem seg](images/semseg.png)

---

### Generative Models

![pix2pix](images/pix2pix.png)

---

Tutte queste (e molte altre) applicazioni sono possibili grazie all' **apprendimento di filtri (kernel) convoluzionali**.

Per poter capire perché è bene apprendere questi filtri, è prima necessario capire l'operatore di convoluzione e come questo viene usato nella computer vision tradizionale.

---

## L'operazione di convoluzione


In **teoria dei segnali** l'operazione di convoluione è usata per studiare la rispotsa di un iustema fisico quando un determinato segnale è applicato al suo input.

Senza dilungarsi nella teoria, quel che è necessario sapere che:

<br />


- L'operazione di convoluzione tra due segnali (funzioni), produce una nuova funzione
- La convoluzione è sia discreta che continua
- La convoluzione mono-dimensionale può essere generalizzata al caso a più dimensioni
- L'operazione di convoluzione è commutativa

---

### Convoluzione discreta

Dati due segnali discreti $g[n]$ e $x[n]$, l'operazione di covoluzione è calcolato come:

<br />

$$ (x * g)[n] = \sum_{-\infty}^{+\infty}{x[m]g[n-m]} $$

<br />

---

Nel caso discreto a due dimensioni (immagini), l'operazione di convoluzione si definisce come:

<br />

$$ O(i,j) = \sum^{j}_{u=-k}{\sum_{v=-k}^{k}{F(u,v)I(u-v, j -v)}} $$

<br />

- $I$ è l'immagine di input
- $F$ è il filtro convoluzionale quadrato, di lato $2k$
- $O$ è il pixel di output nella posizione $(i,j)$.

![conv no stride](images/numerical_no_padding_no_strides.gif)

---

In computer vision  "tradizionale" i Kernel sono definiti **manualmente**, in modo tale da **estrarre determinate caratteristiche (features) di interesse** dall'immagine di input.

![edge](images/convolution_kernel.png)

<br />

A kernel (filtri) diversi, corrispondono diverse features estratte.

---

Nella formula della convoluzione è possibile notare come l'operazione sia effettuata per ogni posizione $(i,j)$

<br />

$$ O(i,j) = \sum^{j}_{u=-k}{\sum_{v=-k}^{k}{F(u,v)I(u-v, j -v)}} $$

<br />

In realtà, ci sono due parametri non mostrati nella formula che controllano come l'operazione di convoluzione viene effettuata: **lo stride** (orizzontale e verticale) ed il **padding**.

---

Questi due parametri altro non sono che il numero di pixel da "saltare" quando si fa scorrere il kernel sull'immagine di input (stride), e da aggiungere come cornice all'input (padding).

Se l'immagine è quadrata, ed applichiamo lo stesso stride $S$, si può calcolare la dimensione dell'output della convoluzione come:

<br />

$$ O_w = O_h = \left\lfloor\frac{I_w - 2k + 2P}{S}\right\rfloor + 1 $$

<br />

- $P$ è il padding applicato
- $2k$ è il lato del kernel convoluzionale (solitamente indicato come $K$)
- $I_w$,$I_h$ la dimensione lato dell'immagine di input

---

![padding and stride](images/numerical_padding_strides.gif)

Convoluzione tra un immagine $5 \times 5$, con uno **zero padding** $1 \times 1$ ed un kernel $3 \times 3$, usando stride $2 \times 2$

---

> Fin'ora abbiamo considerato **solo immagini a singolo canale** (scala di grigi), ma l'operazione di convoluzione può essere effettuata tra **volumi** di profondità arbitraria (immagini RGB, oppure volumi di qualsiasi profondità D).

---

### Convoluzioni tra volumi

![kernels](images/conv_kernels.png)

Un'immagine può essere vista come un volume di immagini in scala di grigi, messe una dietro l'altra.

<br />

Allo stesso modo, i kernel convoluzionali possono essere volumi di filtri della stessa profondità dell'immagine di input.

**Input C canali** $ \rightarrow $ **Singolo kernel a C canali**

---

Data un immagine RGB, la convluzione con un kernel $3 \times 3$:

1. La convoluzione di ogni canale per il rispettivo filtro a profindità 1

![conv](images/conv_1.gif)

---

2. La somma delle **feature map** estratte

![conv sum](images/conv_sum.gif)

---

3. Se è presente un termine di bias, viene aggiunto alla feature map risultante.

![conv bias](images/conv_bias.gif)

---

Quindi la formula per la convoluzione tra una immagine $I = \{I_1, \cdot, I_D\}$ ed un filtro $F = \{F_1, \cdot, F_D\}$ è:

<br />

$$ O(i,j) = \sum^{D}_{d=1}{\sum^{j}_{u=-k}{\sum_{v=-k}^{k}{F_d(u,v)I(_du-v, j -v)}}} $$

Il risultato è quindi una singola feature map (somma) la cui risoluzione è la stessa che si sarebbe ottenuta con una convoluzione su singolo canale.

---

## Reti neurali convoluzionali: l'idea

> Anziché definire manualmente il kernel (filtro) per estrarre specifiche features dall'immagine
>
> rendiamo **il kernel** apprendibile e facciamo sì che il processo di apprendimento, modifichi i parametri
> del filtro, in modo tale che l'operazione di convoluzione tra esso e l'input estragga features significative per
> risolvere il task (specificato dalla loss function).

---

## Apprendere filtri convoluzionali

> Apprendere filtri convoluzionali consiste nel **definire un numero arbitrario N di filtri da apprendere** ed eseguire N convoluzioni su volumi, in maniera indipendente.

Ogni filtro convoluzionale è **un neurone** che osserva una regione locale dell'immagine (sulla quale scorre).

![local receptive field](images/local_rf.png)

---

![features](images/conv_net.png)

Ogni layer convoluzionale apprende la capacità di estrarre features via via più astratte all'aumentare della profondità della rete, combinando le features elementari estratte dai layer precedenti.

---

## Classificazione ed estrazione di features

Essendo a tutti gli effetti una **rete neurale**, possiamo definire l'architettura in modo tale da estrarre **un numero arbirario di features** (a bassa dimensionalitù) ed utilizzarlo come **input di una classificatore** (rete FC).

![fe](images/feature-extractor.png)

---

Definendo le architetture **a blocchi** (blocchi di feature extraction e classificazione indipendenti) possiamo pensare di **riutilizzare** feature extractor allenati da altri su dataset di grandi dimensioni.

<br />

Persumibilmente questi feature extractor hanno appreso la capacità di estrarre features "buone".

---

## Transfer Learning & Fine Tuning

Il riutilizzo del feature extractor puù avvenire in due modi:

- Transfer Learning: il feature extractor viene scaricato (modello pre-trainato) e viene usato **solo** per estrarre le features e diventare l'input della **testa** di classificazione
- Fine Tuning: il feature ectractor viene **rifinito** durante il processo di train, quindi non sarà solo l'input della **testa**, ma diventerà parte dell'architettura da **allenare**.

---

## Localizzazione

Individuare la bounding box che racchiude un oggetto all'interno di una immagine può essere fatto usando una rete neurale convoluzionale che rispetta la struttura appena definita.

Infatti, avendo a dispozione un dataset di immagini contenenti un oggetto annotato e le coordinate della bounding box, possiamo definire una architettura in grado di **regredire** le coordinate.

![loc as reg](images/loc-as-reg.png)

---

## Localizzazione e classificazione

È un sottoinsieme del task (più complesso) di object detection.

Supponiamo di avere in scena solo un oggetto ed una bounding box da regredire.

<br />

È possibile definire una rete neurale con **due teste**:

1. Regression head: per la regressione delle coordinate (più essere class agnostic o class specific)
2. Classification head: per la classificazione dell'oggetto

---

È possibile **allenare simultaneamente** la rete a risolvere entrambi i task: questo è un esempio di multi-task learning.

![double head](images/double-head.png)

---

### Metriche

Il task di classificazione e localizzazione richiede la misura di due metriche in simultanea:

<br />

- La precisione di classificazione, cioè tutte le metriche valide per un classificatore (come l'accuracy)
- La precisione per la detection

Misurare la precisione per la detection, in realtà richiede di trattare il problema come un problema di **classificazione binaria**.

---

### Intersection Over Union

Per decidere se una bounding box predetta è a tutti gli effetti una "detection" è possibile utilizzare l'intersection over union.

$$ IoU = \frac{A \cap B}{A \cup B} $$

<br />

Il suo valore è tra 0 (nessuna detection) ed 1 (overlap completo).

---

![iou](images/iou.png)

---

Per *decidere* se una bounding box predetta è da considerare una **detection**, si fissa una soglia di IoU e vengono considerate come detection solo quelle predizioni di bounding box che superano la soglia.

<br />

Così facendo ci ritroviamo nel caso di una classificazione binaria, in cui, però, possiamo solo avere:

- True positives: detection
- False positives: detection errate (non passano la soglia)

È impossibile avere False negatives o true negatives, dato che non esistono i negativi.

---

## Precision

Per il motivo precedentemente introdotto, l'unica metrica misurabile è la **precision**

<br />

$$ P = \frac{TP}{TP + FP} $$

---

## Domande

1. L'operazione di convoluzione che risultato produce?
2. La convoluzione tra una immagine ed un kernel/filtro convoluzionale, come viene effettuata?
3. Quali sono le fasi della convoluzione tra volumi?
4. Apprendimento della capacità di estrarre features mediante convoluzioni: come?
5. È possibile regredire coordinate usando un feature extractor di una rete (CNN) allenata in classifcazione?
6. Differenza tra transfer learning e fine tuning
7. Al variare della profondità della rete, le features estratte come sono?
8. Per regredire le coordinate di una bounding box: quanti neuroni di output e che loss usare?
9. Spiegare l'Intersection Over Union
10. Spiegare i true positives, true negatives, false positives e false negatives quando facciamo object localization e detection.

---

Introduzione all'object detection + TensorFlow Hub

- Colab: https://bit.ly/2lUTeAM
