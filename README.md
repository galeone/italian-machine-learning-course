# Introduzione al machine learning [corso in Italiano]

<small>(English version below)</small>

Materiale per un crash-course teorico/pratico al machine learning con TensorFlow 2.0.

Argumenti trattati:

- Introduzione al machine learnining: cos'è il machine learning, il dataset, le famiglie di algoritmi esistenti
- Il processo di apprendimento: loss function, gradient descent ed algoritmi di ottimizzazione
- Introduzione a TensorFlow 2.0: eager execution, l'ecosistema, introduzione a TensorFlow Datasets
- Definire pipeline di input ottimizzate con la `tf.data` API
- Classificazione di immagini con reti completamente connesse
- Reti neurali convoluzionali: teoria ed applicazioni
- Conversione e confronto tra una rete completamente connessa per classificazione e una rete neurale convoluzionale
- Classificazione di immagini con reti neurali convoluzinali
- Classificazione e localizzazione di un oggetto in un'immagine: apprendere a regredire coordinate e classificare contemporaneamente
- Usare TensorFlow Hub per fare Transfer Learning e Fine Tuning

## Parte teorica

La teoria è trattata usando delle slide. Le slide sono nella cartella `slides`. Il tool usato per scriverle e crearle (nel branch `gh-pages`) è fusuma: https://github.com/hiroppy/fusuma

Le slide sono disponibili online:

https://pgaleone.eu/italian-machine-learning-course

## Parte pratica

La parte pratica è trattata usando Google Colab notebook:

- Introduzione a TensorFlow 2.0 ed a TensorFlow Datasets: https://bit.ly/2lno7O5
- Introduzione alle reti neurali convoluzionali: https://bit.ly/2lUTeAM
- Introduzione all'object detection, Transfer Learning e Fine Tuning con TensorFlow Hub: https://bit.ly/2MeO8IK

I notebook sono stati caricati su questo repo, così è possibile discutere qui di cambiamenti (usare issue e merge request).

---

# Introduction to machine learning [Italian course]

Material for a theoretical practical machine learning crash course with TensorFlow 2.0.

Topics covered:

- Introduction to machine learning: what is machine learning, the dataset, the machine learning families and algorithms
- The learning process: loss function, gradient descent and optimizations algorithm
- Introduction to TensorFlow 2.0: eager execution, ecosystem, TensorFlow Datasets
- Data Input Pipeline with TensorFlow `tf.data` API
- Image classifier with Fully Connected layers
- Convolutional Neural Networks: theory and applications
- Converting the image classifier from fully connected to convolutional
- Image classification with CNN
- Single object detection: learning to regress coordinates and classify at the same time
- Transfer Learning and Fine tuning with TensorFlow Hub

### Theoretical part

The theoretical part is covered using slides. The slides are in the folder `slides`, and they have been written and built (branch `gh-pages') using fusuma: https://github.com/hiroppy/fusuma

Slides available online:

https://pgaleone.eu/italian-machine-learning-course

### Practical part

The practical part is covered using Google Colab notebooks:

- Introduction to TensorFlow 2.0 and TensorFlow Datasets: https://bit.ly/2lno7O5
- Introduction to Convolutional Neural Networks: https://bit.ly/2lUTeAM
- Introduction to Object Detection and Tranfer Learning with TensorFlow Hub: https://bit.ly/2MeO8IK

The same notebook have been uploaded to this repo so we can discuss about changes here (feel free to open issues and submit pull requests).
