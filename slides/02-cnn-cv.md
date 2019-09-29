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

---

## Domande

---

Introduzione all'object detection + TensorFlow Hub

- Colab: https://bit.ly/2lUTeAM
