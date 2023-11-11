# Dokumentacja
### Skrypt zmieniający adres fizyczny interfejsu sieciowego komputera

###### Skrypt został wykonany w języku **Python** ze względu na prostotę oraz szeroki zakres zastosowania tego języka. Program powinien być używany na urządzeniach z systemem z rodziny systemów Linuxowych. **Próba uruchomiania programu na innych systemach może grozić nieprzewidywalnymi zachowaniami i brakiem funkcjonowania.** 

```python
#!/usr/bin/env python
```
###### Powyższa linijka informuje kompilator że, będzimy pracować w **Pythonie 2.7** z uwagi na większe wsparcie sprzętu w działaniu skryptów w tej wersji języka.
### Wykorzystane biblioteki

```python
    import subprocess
```
###### Do wykonania tego programu wykorzystamy bibliotekę **subprocess** która udostępnia nam możliwość wykonywania komend systemowych w terminalu oraz dopasowywanie ich do działania wybranego programu. Poniżej zamieszczony jest link do dokumentacji biblioteki *subprocess*.

<https://docs.python.org/3/library/subprocess.html>

```python
    import optparse
```
###### Następną biblioteką potrzebną do realizacji tego projektu będzie optparse. Udostępnia ona możliwość wywoływanie komend w terminalu z różnymi opcjami. W tym wypadku opcjami których użyjemy będą -i lub --infterface sygnalizujących urządzeniu że po tych słowach kluczowych użytkownik wpisze interfejs siecowy którego będzie dotyczyć zmiana adresu MAC. Następnymi opcjami z których skorzystamy są -m lub --mac sygnalizujących że po tych słowach kluczowych użytkownik wprowadzi nowy adres fizyczny. Poniżej zamieszczony jest link do dokumentacji biblioteki optparse

<https://docs.python.org/3/library/optparse.html>

```python
    import re
```
###### Ostatnią biblioteką pomocną w tworzeniu tego skryptu będzie re. Jest to biblioteka umożliwiająca nam skorzystanie z wyrażeń regularnych, która pozwoli nam w fazie końcowej skryptu sprawdzić nasz aktualny adres MAC oraz porównać go z nowym adresem fizycznym wprowadzonym przez użytkownika w celu sprawdzenia czy adres został zmieniony. Poniżej zamieszczony jest link do dokumentacji biblioteki re.

<https://docs.python.org/3/library/re.html>

### Utworzone funkcje

```python
    def get_arguments():
    parser = optparse.OptionParser()
    parser.add_option("-i", "--interface", dest="interface", help="Interface to change its MAC address")
    parser.add_option("-m", "--mac", dest="new_mac", help="New MAC address")
    (options, arguments) = parser.parse_args()
    if not options.interface:
        parser.error("[-] Please specify an interface, use --help for more info")
    elif not options.new_mac:
        parser.error("[-] Please specify an new MAC address, use --help for more info")
    return options
```
###### Powyższa funkcja będzie pobierała od użytkownika interfejs sieciowy oraz nowy adres MAC.Do zmiennej *parser* przypisujemy *optparse.OptionParse()* w celu inicjalizacji opcji. W następnych dwóch linijkach dodajemy opcje niezbędne do zmiany adresu fizycznego urządzenia. Następnie do dwoch zmiennych *(options, arguments)* przypisujemy *parser.parse_args()* w celu zatwierdzenia opcji które dodaliśmy. W następnym kroku sprawdzamy czy użytkownik podał odpowiednie opcje niezbędne do pobrania przez funkcję interfejsu sieciowego oraz adresu fizycznego. Gdy użytkownik nie poda tych danych zostanie wyświetlony błąd adekwatny do brakującej opcji. Na samym końcu funkcja zwraca opcje gdyż tylko na nich operowaliśmy.

```python
    def change_mac(interface, new_mac):
    print("[+] Changing mac address for " + interface + " to " + new_mac)
    subprocess.call(["ifconfig", interface, "down"])
    subprocess.call(["ifconfig", interface, "hw", "ether", new_mac])
    subprocess.call(["ifconfig", interface, "up"])
```
###### Funkcja powyżej będzie zmianiała dares fizyczny wybranego przez użytkownika interfejsu siecowego. Funkcja przyjmuje 2 argumenty, argument *interface* oznaczaja interfejs sieciowy wybrany przez użytkownika podczas wywoływania funkcji *get_arguments()*. 