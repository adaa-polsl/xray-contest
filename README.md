# Konkurs organizowany przez Koło Naukowe Data Science 

Serdecznie zapraszamy wszystkich Studentów do udziału w konkursie organizowanym przez Koło Naukowe Data Science (https://www.facebook.com/SKNDataScience) oraz grupę naukową ADAA (http://adaa.polsl.pl/). Za najlepsze rozwiązania przewidziane są nagrody (smartbandy, książki oraz unikalne gadżety politechniczne).

Celem konkursu jest opracowanie algorytmu, który określi czy na analizowanych zdjęciach RTG znajdują się przedmioty niebezpieczne (takie jak broń, noże, nożyce).

W konkursie mogą uczestniczyć zespoły max 3 osobowe. Konkurs prowadzony jest w 2 grupach wiekowych (każda z grup ma oddzielny ranking i osobną pulę nagród):

* studenci studiów inżynierskich,
* studenci studiów magisterskich.

Jeżeli w zespole jest co najmniej 1 osoba ze studiów inżynierskich to zespół zaliczany jest do inżynierskiej grupy wiekowej.

## Dane treningowe i testowe

Zdjęcia treningowe (`*.jpg`, ~4.7GB) wraz z etykietami (`labels.csv`) dostępne są na:

* mirror Google Drive: https://drive.google.com/file/d/1SBtAwUC2HahJBROMjXmdEq3VG2Qx08SO/view?usp=sharing (pobieranie z poziomu konsoli może być utrudnione),
* mirror AWS S3: https://skn-rtg.s3.amazonaws.com/train.zip (pobieranie jest możliwe poprzez komendę `wget` w systemach unixowych).
    
Zdjęcia, na których występują przedmioty niebezpieczne oznaczone są w pliku `labels.csv` etykietą `1` (pozostałe zdjęcia mają przypisaną etykietę `0`).

Zdjęcia testowe (~0.9GB) bez etykiet dostępne są na:

* mirror Google Drive: https://drive.google.com/file/d/1YCTxq9vw7MZpWs7Hi3K6Nl7J0o0aMhhp/view?usp=sharing
* mirror AWS S3: https://skn-rtg.s3.amazonaws.com/test.zip

## Format rozwiązania

Dla każdego zdjęcia testowego algorytm powinien zwracać liczbę z zakresu 0-1, określającą jak bardzo prawdopodobne jest to, że na zdjęciu znajduje się przedmiot niebezpieczny (im liczba ta bliższa `1` tym wystąpienie bardziej prawdopodobne).

Wyniki powinny zostać zapisane do pliku `CSV` zawierającego w kolejnych liniach `<nazwa_pliku>,<prawdopodobieństwo>` np.

```
1.jpg,0.04
7.jpg,0.75
3.jpg,1
4.jpg,0
6.jpg,0.4
```

Separatorem pól jest przecinek, znakiem dziesiętnym jest kropka. Plik wynikowy nie powinien posiadać nagłówka - w pierwszej linii powinna się już znaleźć nazwa zdjęcia wraz z szacowanym prawdopodobieństwem. Kolejność wierszy (nazw zdjęć) nie ma znaczenia.

Przykładowy kod Python zapisujący plik CSV w takim formacie: 

```python
# nazwy_plikow - optymalnie np.array z nazwami pliku ['1.jpg',.....]
# y_pred - np.array z wyznaczonymi przez model prawdopodobieństwami z zakresu 0-1 (dla klasy pozytywnej, więc kształ to Nx1)
pd.DataFrame({'nazwa_pliku':nazwy_plikow,'prawdopodobienstwo':y_pred[:,1]}).to_csv('pred.csv', index = False, header = False)
```

## Zgłaszanie rozwiązań

Rozwiązania należy zgłaszać poprzez [stronę Facbook Koła](https://www.facebook.com/SKNDataScience) dodając do wiadomości załącznik w postaci archiwum ZIP zawierającego:

* plik CSV z odpowiedziami dla zbioru testowego,
* kod źrodłowy rozwiązania.

W treści wiadomomości należy również podać skład zespołu oraz grupę wiekową.

Nagrodzone zostaną rozwiązania o najwyższej wartości AUC (pola pod krzywą ROC). Aplikacja do wstępne oceny rozwiązań konkursowych znajduje się pod adresem https://xraycontest.shinyapps.io/xray_contest/. 

## Przebieg konkursu

* do niedzieli 5 maja (włącznie) - zgłoszenie rozwiązania poprzez stronę Facebook Koła (https://m.me/SKNDataScience),
* wtorek 7 maja - ogłoszenie wyników podczas spotkania Koła, nagrodzenie uczestników.

## Linki

* Strona Facebook Koła: https://www.facebook.com/SKNDataScience

* Zbiór treningowy wraz z etykietami (~4.7GB):
    * Mirror Google Drive: https://drive.google.com/file/d/1SBtAwUC2HahJBROMjXmdEq3VG2Qx08SO/view?usp=sharing
    * Mirror AWS S3: https://skn-rtg.s3.amazonaws.com/train.zip
    
* Zbiór testowy (~0.9GB):
    * Mirror Google Drive: https://drive.google.com/file/d/1YCTxq9vw7MZpWs7Hi3K6Nl7J0o0aMhhp/view?usp=sharing
    * Mirror AWS S3: https://skn-rtg.s3.amazonaws.com/test.zip

* Przykładowe rozwiązanie w postaci [jupyter notebook](https://github.com/adaa-polsl/xray-contest/blob/master/Example.ipynb)'a. Wymagane dla tego rozwiązania zależności do środowiska Python 3 (zalecana wersja 3.6) można znaleźć w pliku `requirements.txt`.

* Darmowe rozwiązania chmurowe do uruchamiania obliczeń:
    * [Google colaboratory](https://colab.research.google.com/) - dostęp do 2 wirtualnych rdzeni Intel Xeon, 13GB ram oraz dzielonego GPU Nvidia Tesla K80 (do dyspozycji ok 0,5GB pamięci). 33GB wolnej przestrzeni dyskowej jest czyszczone po zakończeniu maksymalnie 12h sesji. Wymagane jest posiadanie konta google. Możliwa jest instalacja aplikacji przez standardowe komendy typu `apt`. Szeroki opis funkcjonalności można znaleźć w notebooku `Welcome.ipynb`, który jest generowany automatycznie lub w wielu artykułach dostępnych w sieci.
    * [Intel AI DevCloud](https://software.intel.com/en-us/ai/devcloud) Należy się zarejestrować, podać (w miarę) prawdziwe informacje o wykorzystaniu. W opisie powinno wystarczyć: "RTG baggage classification for 1st contest Data Science Student Science Club at Silesian University of Technology (Gliwice, Poland).". Zaletą jest dostęp do wielu węzłów składających się z 2 procesorów 6-rdzeniowych z 96/192GB ramu oraz przestrzeń dyskowa, która nie jest czyszczona po zakończeniu sesji. 30-dniowy dostęp można przedłużyć po przesłaniu opisu zastosowania. Od wypełnienia formularza do przyznania dostępu może minąć kilka dni. Opis i zasady wykorzystywania tego rozwiązania można znaleźć w obszernym FAQ na dole strony usługi lub po zalogowaniu.

* Aplikacja do wstępnej oceny rozwiązań konkursowych: https://xraycontest.shinyapps.io/xray_contest/ (ocena dokonywana jest na 10% zbioru testowego).
