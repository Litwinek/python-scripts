# Dokumentacja
### Skrypt zmieniający adres fizyczny interfejsu sieciowego komputera

###### Skrypt został wykonany w języku **Python** ze względu na prostotę oraz szeroki zakres zastosowania tego języka. Program powinien być używany na urządzeniach z systemem z rodziny systemów Linuxowych. **Próba uruchomiania programu na innych systemach może grozić nieprzewidywalnymi zachowaniami i brakiem funkcjonowania.** 

```python
#!/usr/bin/env python
```
###### Powyższa linijka informuje kompilator że, będzimy pracować w **Pythonie 2.7** z uwagi na większe wsparcie sprzętu w działaniu skryptów w tej wersji języka.

```python
    import subprocess
```
###### Do wykonania tego programu wykorzystamy bibliotekę **subprocess** która udostępnia nam możliwość wykonywania komend systemowych w terminalu oraz dopasowywanie ich do działania wybranego programu. Poniżej zamieszczony jest link do dokumentacji biblioteki *subprocess*.

<https://docs.python.org/3/library/subprocess.html>