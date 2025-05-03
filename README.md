# Geslachtsherkenning met AI – UTKFace + CNN (Verslagproject)

Dit project is een verslag en demonstratie van een AI-model dat het geslacht (man of vrouw) voorspelt op basis van een gezichtsafbeelding. 
Het model wordt getraind op de UTKFace dataset en maakt gebruik van een Convolutional Neural Network (CNN) gebouwd met TensorFlow. 

Je kunt dit project stap voor stap volgen in een Jupyter Notebook (.ipynb-bestand).

## Doel van het project

Dit project is niet bedoeld als herbruikbare software, maar als documentatie en demonstratie van een machine learning proces. 
Het doel is om te laten zien hoe je zelf een geslachtsvoorspellende AI kunt trainen, evalueren en testen, met overwegingen bij de opbouw van het model.

## Belangrijk

Voor het uitvoeren van dit project heb je Jupyter Notebook nodig, aangezien alle stappen zijn beschreven en uitgevoerd in een .ipynb bestand.
De laatste cel van het notebook bevat de code om het model te testen, waarmee je direct afbeeldingen kunt laten voorspellen. Dit betekent dat je mijn voorgetrainde model kunt gebruiken zonder het volledige trainingsproces opnieuw uit te voeren.
Als je ervoor kiest om alle cellen uit te voeren, wordt mijn voorgetrainde model vervangen door je eigen model, dat ongeveer dezelfde resultaten zal opleveren, maar toch kleine verschillen kan vertonen door de aard van het trainingsproces.
Let op: Om het model zelf te trainen, heb je nog steeds de [UTKFace dataset](https://www.kaggle.com/datasets/jangedoo/utkface-new) of een andere geschikte verzameling afbeeldingen nodig.

## Bezoek de demo

Wil je zonder installatie zien hoe het werkt? Bezoek dan de online [demo](https://deanj.dev/geslacht-ai)

## Uitleg van het proces

### Dataset – UTKFace

De gebruikte dataset is [UTKFace](https://www.kaggle.com/datasets/jangedoo/utkface-new), een veelgebruikte dataset met gezichten. 
Elke bestandsnaam bevat metadata, waaronder het geslacht (0 = man, 1 = vrouw). De gezichten zijn gevarieerd in leeftijd, etniciteit en belichting.

Bestandsvoorbeeld:
```
25_1_0_20170116174525125.jpg
```
Hier betekent `1` dat het geslacht vrouwelijk is.

### Preprocessing

- Alle afbeeldingen worden geschaald naar 100x100 pixels.
- De pixelwaarden worden genormaliseerd naar het bereik 0.0 – 1.0.
- Alleen het geslacht wordt uit de bestandsnaam gehaald en gebruikt als label.
- Data wordt gesplitst in 80% training en 20% testdata met `train_test_split`.

### Modelarchitectuur (CNN)

Het model bestaat uit:

- 3 convolutional lagen:
  - Conv2D (32 filters) + MaxPooling2D
  - Conv2D (64 filters) + MaxPooling2D
  - Conv2D (128 filters) + MaxPooling2D
- Flatten layer
- Dense (64 neuronen, ReLU)
- Dropout (0.3) om overfitting te voorkomen
- Output: Dense (1 neuron, sigmoid voor binaire classificatie)

### Keuzes en overwegingen

- **Optimizer**: Adam – snelle convergentie
- **Loss function**: Binary Crossentropy – standaard voor binaire classificatie
- **Activatie**: ReLU voor verborgen lagen, Sigmoid voor de output
- **Early Stopping**: Model stopt automatisch bij geen verbetering in validatie-accuratesse
- **Epochs**: Maximaal 10, maar training stopt vaak eerder door early stopping

### Evaluatie

- Testset wordt gebruikt om de nauwkeurigheid van het model te meten.
- Resultaten worden getoond in de output van de notebook.
- Er worden voorbeeldvoorspellingen getoond, inclusief vergelijking tussen werkelijke en voorspelde geslachten.

### Zelf testen

Gebruik de laatste cel van het notebook om nieuwe afbeeldingen te testen.  
Afbeeldingen moeten in de map `custom_test/` staan in JPG, JPEG of PNG formaat.

## Installatie

### 1. Installeer Python 3.11

Download [Python 3.11](https://www.python.org/downloads/)

### 2. Maak een virtuele omgeving aan

Windows:
```
python -m venv venv
venv\Scripts\activate
```

Mac/Linux:
```
python3.11 -m venv venv
source venv/bin/activate
```

### 3. Installeer de vereisten

```
pip install jupyter tensorflow opencv-python numpy matplotlib scikit-learn
```

### 4. Start de notebook

```
jupyter notebook
```

Open vervolgens het `.ipynb` bestand in de browser en doorloop de cellen stap voor stap.

## Structuur

- `data/UTKFace` – de dataset (niet meegeleverd, moet zelf gedownload worden)
- `custom_test/` – map voor afbeeldingen die je zelf wilt testen
- `gender_model.keras` – het getrainde modelbestand (wordt aangemaakt na training)
- `neuraal_netwerk.ipynb` – het hoofdnotebook met uitleg, code en stappen

## Vereisten

- Python 3.11
- Jupyter Notebook
- tensorflow
- opencv-python
- numpy
- matplotlib
- scikit-learn
- [UTKFace dataset](https://www.kaggle.com/datasets/jangedoo/utkface-new) (handmatig downloaden)

## Belangrijk

- De `.ipynb` notebook dient als verslag en demonstratie.
- Niet bedoeld als kant-en-klaar herbruikbaar pakket.
- Bekijk de demo op deanj.dev/geslacht-ai

## Licentie

MIT – Vrij te gebruiken en te bestuderen.  
Gebruik dit project op verantwoorde wijze. De auteur is niet aansprakelijk voor foutieve voorspellingen of misbruik van het model.
