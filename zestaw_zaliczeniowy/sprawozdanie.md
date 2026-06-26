## Lab 1 i Lab 2 — Perceptron (Klasyfikator Liniowy)

### Opis zadania

Zadaniem było przetestowanie najprostszego modelu – perceptronu – najpierw na prostym zbiorze `iris` (2 cechy), a następnie na trudniejszym zbiorze obrazów ubrań `Fashion-MNIST` (porównanie łatwych klas, np. spodnie vs buty, oraz trudnych par, np. sweter vs płaszcz). Przeanalizowano również znalezione przez model "szablony" wag oraz macierz pomyłek.

### Wnioski

- **Iris:** Dla klas liniowo separowalnych (jak _setosa_ vs _versicolor_) perceptron bez problemu osiąga 100% dokładności, poprawnie wyznaczając linię podziału.
- **Fashion-MNIST (Łatwa para):** Model osiąga bardzo wysoką skuteczność (bliską 100%), ponieważ kontury i ogólne cechy spodni oraz butów diametralnie się od siebie różnią. Wizualizacja wag pokazuje wyraźny kształt przypominający nogawki.
- **Fashion-MNIST (Trudna para):** Przy klasyfikacji swetrów i płaszczy skuteczność gwałtownie spada. Modele liniowe nie radzą sobie z obiektami o zbliżonych kształtach i nakładających się pikselach. Macierz pomyłek wskazuje na częste mylenie tych kategorii.

---

## Lab 3 — Wielowarstwowy Perceptron (MLP) w NumPy

### Opis zadania

Zadanie polegało na samodzielnej implementacji sieci jednowarstwowej i wielowarstwowej od zera przy użyciu wyłącznie biblioteki `numpy`. Sieć miała rozwiązać problem logiczny XOR (który wymaga warstwy ukrytej), a następnie zostać rozbudowana do obsługi funkcji Softmax i klasyfikacji wieloklasowej (3 wybrane klasy) na zbiorze `Fashion-MNIST`.

### Wnioski

- Jeden neuron nie potrafi rozwiązać problemu XOR, ponieważ nie da się go rozdzielić pojedynczą prostą kreską. Wprowadzenie warstwy ukrytej pozwala sieci "zakrzywić" przestrzeń cech.
- Własnoręcznie napisany algorytm propagacji wstecznej (backpropagation) z funkcją Softmax pozwala na poprawną naukę klasyfikacji ubrań. Pokazuje to, że głębokie uczenie opiera się na czystej matematyce i pochodnych, a nie na "magii" gotowych frameworków.

---

## Lab 4 — Sieci Konwencjonalne (CNN) w TensorFlow

### Opis zadania

Zbudowano prostą sieć konwencjonalną (CNN) w TensorFlow/Keras dla danych `Fashion-MNIST`. Głównym zadaniem samodzielnym było jednak zaprojektowanie i porównanie dwóch różnych architektur CNN na trudniejszym, kolorowym zbiorze `CIFAR-10` (obrazy RGB, 10 klas).

### Wnioski

- Tradycyjne sieci MLP gubią informację o tym, jak piksele leżą obok siebie. Sieci CNN za pomocą filtrów (konwolucji) świetnie wyciągają lokalne wzorce (krawędzie, kształty), co daje im ogromną przewagę.
- Podczas testów na zbiorze `CIFAR-10` architektura głębsza (z większą liczbą filtrów i warstwami Dropout zapobiegającymi przeuczeniu) osiągnęła znacznie lepszy wynik i stabilniejszy proces nauki niż sieć płytka.

---

## Lab 5 — Augmentacja danych i Walidacja Krzyżowa (CV)

### Opis zadania

Zbadano wpływ sztucznego transformowania obrazów (losowe obroty, przybliżenia, odbicia lustrzane) na zdolności generalizacyjne modelu. Przeprowadzono eksperyment typu _mini grid_ (przeszukiwanie hiperparametrów) połączony z 2-krotną walidacją krzyżową (2-fold CV).

### Wnioski

- Augmentacja danych działa jak cyfrowa odżywka dla modelu – "zmusza" go do nauki ogólnych kształtów zamiast zapamiętywania konkretnego ułożenia pikseli na pamięć (zapobiega przeuczeniu).
- Nigdy nie augmentujemy zbioru testowego, ponieważ musi on reprezentować realne, czyste dane, na których sprawdzamy faktyczną jakość modelu.
- Walidacja krzyżowa pozwala obiektywnie ocenić stabilność modelu i wybrać najlepszą kombinację parametrów bez ryzyka, że uzyskaliśmy dobry wynik przypadkiem.

---

## Lab 6 — Sieci Rekurencyjne (RNN/LSTM) w analizie tekstu

### Opis zadania

Po wstępnym etapie modelowania sekwencji (predykcja sinusoidy), głównym celem było stworzenie sieci LSTM do klasyfikacji emocji w tekstach (tweety ze zbioru `dair-ai/emotion`). Zadanie wymagało zamiany słów na wektory (embedding) i przetworzenia ich sekwencyjnie.

### Wnioski

- Zwykłe sieci gubią informację o kolejności słów w zdaniu. Architektura LSTM radzi sobie z tym dzięki mechanizmowi bramek, które decydują, jakie informacje zapamiętać, a jakie odrzucić.
- **Różnica w stanach:** Stan ukryty `h_t` odpowiada za bieżący kontekst i bezpośrednie wyjście w danym kroku, natomiast stan komórki `C_t` pełni rolę "pamięci długoterminowej", która przenosi najważniejsze informacje przez całe zdanie. Dwa stany są potrzebne, aby skutecznie oddzielić wiedzę chwilową od długoterminowej.
