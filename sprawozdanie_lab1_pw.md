
# Sprawozdanie laboratoryjne

**Przedmiot:** Uczenie głębokie do rozpoznawania obiektów  
**Temat:** Laboratorium 1 – Obraz jako dane; pierwszy klasyfikator obrazów (MLP)  
**Autor:** Piotr Wójtowicz  
**Data:** 20.10.2026

## 1. Cel ćwiczenia

Celem ćwiczenia było stworzenie sieci neuronowej, która rozpoznaje rodzaje ubrań na zdjęciach. Wykorzystano do tego perceptron wielowarstwowy (MLP).

Sprawdzono również, jak zmiana liczby warstw i neuronów wpływa na dokładność modelu. Porównano trzy różne architektury sieci oraz przeanalizowano ich wyniki i popełniane błędy.

## 2. Metoda i implementacja

Do wykonania zadania wykorzystano język Python oraz biblioteki PyTorch, torchvision, matplotlib i scikit-learn. Kod uruchomiono w środowisku Google Colab.

Wybrano zbiór FashionMNIST, ponieważ był wykorzystywany na zajęciach i zawiera stosunkowo proste obrazy. W porównaniu do CIFAR-10 jest łatwiejszy do analizy przy użyciu podstawowej sieci MLP.

Zbiór FashionMNIST zawiera:
- 60 000 obrazów treningowych,
- 10 000 obrazów testowych,
- 10 kategorii ubrań,
- obrazy o wymiarach 28 × 28 pikseli w skali szarości.

Przed treningiem obrazy zamieniono na tensory i poddano normalizacji. Następnie każdy obraz został spłaszczony do wektora 784 wartości, który trafiał na wejście sieci neuronowej.

Przetestowano trzy architektury:

- Model A: jedna warstwa ukryta (128 neuronów).
- Model B: dwie warstwy ukryte (256 i 128 neuronów).
- Model C: trzy warstwy ukryte (512, 256 i 128 neuronów).

Wszystkie modele wykorzystywały funkcję aktywacji ReLU oraz funkcję straty CrossEntropyLoss.

Parametry treningu:
- Liczba epok: 8
- Batch size: 128
- Optymalizator: Adam
- Learning rate: 0.001
- Liczba klas wyjściowych: 10

Modele trenowano przy takich samych ustawieniach, aby można było porównać wpływ architektury na skuteczność klasyfikacji.

## 3. Wyniki

Do oceny modeli wykorzystano accuracy, czyli procent poprawnie rozpoznanych obrazów w zbiorze testowym.

### Porównanie architektur

| Model | Architektura | Liczba parametrów | Accuracy |
|---|---|---:|---:|
| A – mały | (128,) | 101 770 | WPISZ_WYNIK_A |
| B – bazowy | (256, 128) | 235 146 | 88,69% |
| C – duży | (512, 256, 128) | 567 434 | WPISZ_WYNIK_C |

Wynik 88,69% pochodzi z modelu bazowego wytrenowanego w notatniku ćwiczeniowym przez 8 epok.

Porównanie architektur pozwala sprawdzić, czy zwiększenie liczby neuronów i warstw poprawia zdolność sieci do rozpoznawania obrazów. Większe modele mają więcej parametrów, ale nie zawsze muszą osiągać lepsze wyniki.


### Krzywe uczenia

W notatniku Jupyter przedstawiono wykres zmian straty
treningowej i testowej podczas kolejnych epok.

Wykres pozwala ocenić, jak przebiegało uczenie modelu
oraz czy pojawiały się oznaki przeuczenia.

### Przykładowe predykcje

W notatniku przedstawiono przykłady poprawnych
i błędnych klasyfikacji obrazów FashionMNIST.

Model może mieć trudności z rozpoznawaniem ubrań
o podobnym wyglądzie, np. koszulek i koszul.

### Macierz pomyłek

Macierz pomyłek, jeśli została wygenerowana,
znajduje się w notatniku Jupyter.

Pozwala sprawdzić, które kategorie ubrań
były najczęściej ze sobą mylone.


## 4. Analiza i interpretacja

Model bazowy osiągnął dokładność 88,69%, co oznacza, że poprawnie sklasyfikował większość obrazów testowych.

Podczas jego treningu strata na danych treningowych zmniejszyła się z około 0,484 do 0,223, a strata testowa z około 0,406 do 0,324.

Oznacza to, że podczas kolejnych epok model coraz lepiej radził sobie z rozpoznawaniem kategorii ubrań.

Jednym z problemów klasyfikacji FashionMNIST jest podobieństwo niektórych kategorii, np. koszulek i koszul z długim rękawem czy swetrów i płaszczy. Takie ubrania mogą mieć podobne kształty, szczególnie na małych obrazach w skali szarości.

Ważnym ograniczeniem modelu MLP jest spłaszczanie obrazu do jednego wektora liczb. Powoduje to, że sieć nie wykorzystuje bezpośrednio informacji o przestrzennym rozmieszczeniu pikseli.

Zwiększenie liczby warstw daje modelowi większe możliwości uczenia się złożonych zależności, ale jednocześnie zwiększa liczbę parametrów i zapotrzebowanie na obliczenia.

Trzeba również pamiętać, że bardzo rozbudowane modele mogą ulegać przeuczeniu, czyli osiągać dobre wyniki na danych treningowych, ale gorsze na nowych obrazach.

## 5. Wnioski

W ćwiczeniu przygotowano klasyfikator obrazów wykorzystujący perceptron wielowarstwowy MLP.

Model bazowy osiągnął dokładność 88,69% na zbiorze testowym FashionMNIST. Pokazuje to, że nawet stosunkowo prosta sieć neuronowa może skutecznie rozpoznawać różne kategorie ubrań.

Porównanie trzech architektur pozwala zbadać wpływ liczby warstw i neuronów na dokładność klasyfikacji oraz złożoność obliczeniową modelu.

Sama większa liczba parametrów nie gwarantuje uzyskania lepszego wyniku. Istotne są również sposób uczenia, dobrane hiperparametry i zdolność modelu do rozpoznawania nowych danych.

W przyszłości można spróbować zastosować sieć splotową CNN, która lepiej wykorzystuje przestrzenną strukturę obrazów i może skuteczniej rozpoznawać podobne kategorie ubrań.
