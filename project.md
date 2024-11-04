# System aukcyjny



## Wprowadzenie

Specyfikacja wymagań funkcjonalnych w ramach informatyzacji procesu sprzedaży produktów w oparciu o mechanizm aukcyjny. 

## Procesy biznesowe

---
<a id="bc1"></a>
### BC1: Sprzedaż aukcyjna 

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2)

**Opis:** Proces biznesowy opisujący sprzedaż za pomocą mechanizmu aukcyjnego. |

**Scenariusz główny:**
1. [Sprzedający](#ac1) wystawia produkt na aukcję. ([UC1](#uc1))
2. [Kupujący](#ac2) oferuje kwotę za produkt wyższą od aktualnie najwyższej oferty. ([BR1](#br1))
3. [Kupujący](#ac2) wygrywa aukcję ([BR2](#br2))
4. [Kupujący](#ac2) przekazuje należność Sprzedającemu.
5. [Sprzedający](#ac1) przekazuje produkt Kupującemu.

**Scenariusze alternatywne:** 

2.A. Oferta Kupującego została przebita, a [Kupujący](#ac2) pragnie przebić aktualnie najwyższą ofertę.
* 2.A.1. Przejdź do kroku 2.

3.A. Czas aukcji upłynął i [Kupujący](#ac2) przegrał aukcję. ([BR2](#br2))
* 3.A.1. Koniec przypadku użycia.

---

## Aktorzy

<a id="ac1"></a>
### AC1: Sprzedający

Osoba oferująca towar na aukcji.

<a id="ac2"></a>
### AC2: Kupujący

Osoba chcąca zakupić produkt na aukcji.


## Przypadki użycia poziomu użytkownika

### Aktorzy i ich cele

[Sprzedający](#ac1):
* [UC1](#uc1): Wystawienie produktu na aukcję
* ...

[Kupujący](#ac2)
* [UC2](#uc2): Zaoferowanie kwoty za produkt na aukcji
* [UC3](#uc3): Wygranie aukcji
* [UC4](#uc4): Przekazanie należności

---
<a id="uc1"></a>
### UC1: Wystawienie produktu na aukcję

**Aktorzy:** [Sprzedający](#ac1)

**Scenariusz główny:**
1. [Sprzedający](#ac1) zgłasza do systemu chęć wystawienia produktu na aukcję.
2. System prosi o podanie danych produktu i ceny wywoławczej.
3. [Sprzedający](#ac1) podaje dane produktu oraz cenę wywoławczą.
4. System weryfikuje poprawność danych.
5. System informuje o pomyślnym wystawieniu produktu na aukcję.

**Scenariusze alternatywne:** 

4.A. Podano niepoprawne lub niekompletne dane produktu.
* 4.A.1. System informuje o błędnie podanych danych.
* 4.A.2. Przejdź do kroku 2.

---

<a id="uc2"></a>
### UC2: Zaoferowanie kwoty za produkt na aukcji

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2)

**Scenariusz główny:**
1. [Kupujący](#ac2) znajduje ofertę od [Sprzedającego](#ac1)
2. System sprawdza czy aukcja jest aktywna
3. [Kupujący](#ac2) podaje kwotę za którą chce dołączyć do aukcji
4. System weryfikuje poprawność [reguły](#br1)

**Scenariusze alternatywne:** 

2.A. Aukcja jest nieaktualna/nieaktywna
* 2.A.1. System informuje o wcześniejszym rozstrzygnięciu aukcji
* 2.A.2. Przejdź do kroku 1.
4.A. Podana kwota jest za niska
* 4.A.1. System informuje o braku poprawności [reguły](#br1)
* 4.A.2. Przejdź do kroku 3.

---

<a id="uc3"></a>
### UC3: Wygranie aukcji

**Aktorzy:** [Kupujący](#ac2)

**Scenariusz główny:**
1. Upływa czas aukcji.
2. System sprawdza poprawność [reguły](#br2).
3. Aukcja się zamyka.
4. [Kupujący](#ac2) zostaje poinformowany o wygraniu aukcji.

**Scenariusze alternatywne:** 

2.A.1. [Kupujący](#ac2) nie jest wygranym aukcji.
* 2.A.1.1. Cel się kończy.
2.A.2. Nikt nie licytował.
* 2.A.2.1. Aukcja zostaje zakończona bez sprzedaży.

---

<a id="uc4"></a>
### UC4: Przekazanie należności

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2)

**Scenariusz główny:**
1. [Kupujący](#ac2) odebrał informację o wygraniu aukcji i przechodzi do płatności.
2. [Kupujący](#ac2) dokonuje płatności na stronie.
3. System sprawdza poprawność [reguły](#br3).
4. Z konta [kupującego](#ac2) pobrane zostaje równowartość kwoty za wylicytowany produkt.
5. [Sprzedający](#ac1) otrzymuje płatność.

**Scenariusze alternatywne:** 

3.A.1 Płatność nie powiodła się
* 3.A.1.1 Wróć do punktu 2.
3.A.2 Kupujący nie dokonał płatności.
* 3.A.2.1

---
## Obiewkty biznesowe (inaczje obiekty dziedzinowe lub informatycjne)

### BO1: Aukcja

Aukcja jest formą zawierania transakcji kupna-sprzedaży, w której Sprzedający określa cenę wywoławczą produktu, natomiast Kupujący mogą oferować własną ofertę zakupu każdorazowo proponując kwotę wyższą od aktualnie oferowanej kwoty. Aukcja kończy się po upływie określonego czasu. Jeśli złożona została co najmniej jedna oferta zakupy produkt nabywa ten Kupujący, który zaproponował najwyższą kwotę. 

### BO2: Produkt

Fizyczny lub cyfrowy obiekt, który ma zostać sprzedany w ramach aukcji.

## Reguły biznesowe

<a id="br1"></a>
### BR1: Złożenie oferty

Złożenie oferty wymaga zaproponowania kwoty wyższej niż aktualnie oferowana o minimum 1,00 PLN.


<a id="br2"></a>
### BR2: Rozstrzygnięcie aukcji

Aukcję wygrywa ten z [Kupujący](#ac2)ch, który w momencie jej zakończenia (upłynięcia czasu) złożył najwyższą ofertę.

## Macierz CRUDL


| Przypadek użycia                                  | Aukcja | Produkt | ... |
| ------------------------------------------------- | ------ | ------- | --- |
| UC1: Wystawienia produktu na aukcję               |    C   |    C    | ... |
| ???                                               |  ...   |  ...    | ... |


