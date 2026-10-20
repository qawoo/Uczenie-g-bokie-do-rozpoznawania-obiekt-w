# Sprawozdanie laboratoryjne

**Przedmiot:** Uczenie głębokie do rozpoznawania obiektów  
**Zajęcia nr / temat:** 1 — Obraz jako dane; pierwszy klasyfikator obrazów (MLP)  
**Autor / grupa:** [uzupełnij]  
**Data:** 20.10.2026

## 1. Cel ćwiczenia

Celem ćwiczenia było przygotowanie klasyfikatora obrazów za pomocą sieci neuronowej MLP i sprawdzenie, jak zmiana liczby warstw ukrytych i neuronów wpływa na jego skuteczność. Porównane zostały trzy architektury, a ich działanie oceniono na zbiorze FashionMNIST.

## 2. Metoda i implementacja

Wykorzystałem język Python, bibliotekę PyTorch i zbiór FashionMNIST składający się z 60 000 obrazów treningowych i 10 000 testowych. Są to zdjęcia ubrań w skali szarości, o rozmiarze 28 × 28 pikseli, podzielone na 10 klas. Wybrałem FashionMNIST, ponieważ na nim opierał się również kod z zajęć, a MLP łatwiej porównywać dla małych obrazów jednokanałowych niż dla CIFAR-10.

Obrazy przekształcono do tensorów i znormalizowano (średnia 0.2860, odchylenie 0.3530). Model wykorzystywał `Flatten`, warstwy `Linear`, funkcję aktywacji `ReLU` oraz wyjście dla 10 klas. Wykorzystano optymalizator Adam (`lr=0.001`), funkcję straty CrossEntropyLoss, rozmiar paczki 128 i 8 epok. Porównywane warianty: `(128,)`, `(256, 128)` oraz `(512, 256, 128)`. Kod znajduje się w notatniku `laboratorium_1_rozwiazanie.ipynb`.

## 3. Wyniki

| Model | Architektura | Liczba parametrów | Accuracy na teście |
|---|---|---:|---:|
| A — mały | `(128,)` | 101 770 | **[po treningu w Colab]** |
| B — bazowy | `(256, 128)` | 235 146 | **88,69% (wynik z przesłanego ćwiczenia)** |
| C — duży | `(512, 256, 128)` | 567 434 | **[po treningu w Colab]** |

Model bazowy uzyskał 88,69% accuracy po 8 epokach treningu w załączonym notatniku ćwiczeniowym. Tabela wymaga uzupełnienia wynikami pozostałych modeli z jednego wspólnego uruchomienia, ponieważ losowość treningu może wpłynąć na porównanie.

![Krzywe uczenia modelu bazowego z ćwiczeń](wykres_bazowy_z_cwiczen.png)

**Wykres i analiza najlepszego modelu:** [powstają automatycznie po uruchomieniu notatnika].

**Przykładowe poprawne i błędne predykcje:** [powstają automatycznie po uruchomieniu notatnika].

## 4. Analiza i interpretacja

W notatniku bazowym strata treningowa spadała od 0,484 do 0,223, a testowa od 0,406 do 0,324. Wskazuje to na poprawę dopasowania modelu podczas 8 epok. Nie można jednak na tej podstawie ocenić pozostałych wariantów. Po wykonaniu trzech treningów należy wskazać najczęstsze pomyłki na podstawie macierzy pomyłek i porównać krzywe uczenia.

MLP spłaszcza obrazy do 784 liczb, przez co nie korzysta wprost z informacji o sąsiedztwie pikseli. Może to utrudniać rozróżnianie podobnych rodzajów odzieży.

## 5. Wnioski

W ćwiczeniu udało się zbudować model bazowy MLP rozpoznający ubrania ze skutecznością 88,69% na zbiorze testowym. Aby ocenić wpływ architektury, potrzebne są jeszcze wyniki modeli małego i dużego. Końcowy wniosek o najlepszym wariancie zostanie automatycznie przygotowany po uruchomieniu nowego notatnika.
