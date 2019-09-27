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

Tutte queste (e molte altre) applicazioni sono possibili grazie all'apprendimento di filtri (kernel) dell'operatore di convoluzione.

Per poter capire perché è bene apprendere questi filtri, è prima necessario capire l'operatore di convoluzione e come questo viene usato nella computer vision tradizionale.

---

## L'operazione di convoluzione


In **teoria dei segnali** l'operazione di convoluione è usata per studiare la rispotsa di un iustema fisico quando un determinato segnale è applicato al suo input.

Senza dilungarsi nella teoria, quel che è necessario sapere è che:

- L'operazione di convoluzione tra due segnali (funzioni), produce una nuova funzione
- La convoluzione è sia discreta che continua
- La convoluzione mono-dimensionale può essere generalizzata al caso a più dimensioni.

---

### Convoluzione discreta

Dati due segnali discreti $g[n]$ e $x[n]$, l'operazione di covoluzione è calcolato come:

$$ (x * g)[n] = \sum_{-\infty}^{+\infty}{x[m]g[n-m]} $$

<br />

---

Nel caso discreto a due dimensioni (immagini), l'operazione di convoluzione si definisce come:

$$ O(i,j) = \sum^{j}_{u=-k}{\sum_{v=-k}^{k}{F(u,v)I(u-v, j -v)}} $$

- $I$ è l'immagine di input
- $F$ è il filtro convoluzionale quadrato, di lato $2k$
- $O$ è il pixel di output nella posizione $(i,j)$.

---

In computer vision  "tradizionale" i Kernel sono definiti **manualmente**, in modo tale da **estrarre determinate caratteristiche (features) di interesse** dall'immagine di input.

Ad esempio:

![edge](images/convolution_kernel.png)

---

## Domande

---

Convolutional Neural Networks for Image Classificatio and Object Detection

- Colab: 
