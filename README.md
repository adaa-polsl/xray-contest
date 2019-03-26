# Konkurs organizowany przez Koło Naukowe Data Science 

Serdecznie zapraszamy wszystkich Studentów do udziału w konkursie organizowanym przez Koło Naukowe Data Science (https://www.facebook.com/SKNDataScience) oraz grupę naukową ADAA (http://adaa.polsl.pl/). Za najlepsze rozwiązania przewidziane są nagrody (smartbandy, książki oraz unikalne gadżety politechniczne).

W konkursie mogą uczestniczyć zespoły max 3 osobowe. Konkurs prowadzony jest w 2 grupach wiekowych (każda z grup ma oddzielny ranking i osobną pulę nagród):

* studenci studiów inżynierskich,
* studenci studiów magisterskich.

Jeżeli w zespole jest co najmniej 1 osoba ze studiów inżynierskich to zespół zaliczany jest do inżynierskiej grupy wiekowej.

## Dane

Celem konkursu jest opracowanie algorytmu, który określi czy na analizowanych zdjęciach RTG znajdują się przedmioty niebezpieczne (takie jak broń, noże, nożyce). Zdjęcia treningowe (`*.jpg`) wraz z etykietami (`labels.csv`) dostępne są [na dysku google](https://drive.google.com/file/d/1SBtAwUC2HahJBROMjXmdEq3VG2Qx08SO/view?usp=sharing) (pobieranie z poziomu konsoli może być utrudnione) oraz [AWS S3](https://skn-rtg.s3.amazonaws.com/train.zip) (pobieranie jest możliwe poprzez komendę `wget` w systemach unixowych) (rozmiar ~4.7GB). Zdjęcia, na których występują przedmioty niebezpieczne oznaczone są w pliku `labels.csv` etykietą `1` (pozostałe zdjęcia mają przypisaną etykietę `0`).

## Prezentacja i format rozwiązań konkursowych

Prezentacja i ocena rozwiązań odbędzie się we wtorek 16 kwietnia podczas spotkania Koła. Celem każdego z uczestników będzie uruchomienie opracowanego modelu na zbiorze testowym (hasło do archiwum zostanie podane podczas spotkania). Dla każdego zdjęcia algorytm powinien zwracać liczbę z zakresu 0-1, określającą jak bardzo prawdopodobne jest to, że na zdjęciu znajduje się przedmiot niebezpieczny (im liczba ta bliższa `1` tym wystąpienie bardziej prawdopodobne).

Wyniki powinny zostać zapisane do pliku `<id_zespołu>.csv` zawierającego w kolejnych liniach `<nazwa_pliku>,<prawdopodobieństwo>` np.

```
1.jpg,0.04
7.jpg,0.75
3.jpg,1
4.jpg,0
6.jpg,0.4
```

Separatorem pól jest przecinek, znakiem dziesiętnym jest kropka. Nagrodzone zostaną rozwiązania o najwyższej wartości AUC (pola pod krzywą ROC).

## Termin zgłoszeń

Ze względów organizacyjnych, zespoły, które zdecydują się przedstawić swoje rozwiązanie 16 kwietnia, bardzo prosimy o poinformowanie nas o tym do niedzieli 14 kwietnia (włącznie) przez stronę Koła na Facebook (https://www.facebook.com/SKNDataScience). Podczas prezentacji rozwiązania wymagany jest własny komputer oraz pobrane archiwum ze zbiorem testowy.

## Przebieg konkursu

* marzec 26 kwietnia - omówienie konkursu podczas spotkania Koła,
* do niedzieli 14 kwietnia (włącznie) - potwierdzenie chęci prezentacji rozwiązania,
* wtorek 16 kwietnia - prezentacja, ocena rozwiązań, nagrodzenie uczestników.
