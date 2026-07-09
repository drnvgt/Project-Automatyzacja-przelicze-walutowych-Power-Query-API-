# Automatyzacja przeliczeń walutowych (Power Query & API)

## Cel projektu
Projekt stworzony w celu przećwiczenia pracy z API, transformacją danych w Power Query i logiką biznesową stojącą za automatyzacją procesów finansowych. Odtwarza mechanizm przeliczania walut podobny do tego, jaki oferują systemy ERP — celem nie było stworzenie unikalnego narzędzia, tylko pokazanie umiejętności operowania danymi i narzędziami (Excel, Power Query, API) w praktycznym, zbliżonym do rzeczywistości scenariuszu.

## Problem biznesowy
W środowiskach wielowalutowych (np. raportowanie kosztów z kilku krajów do jednej centrali) ręczne przeliczanie kursów walut jest czasochłonne i podatne na błędy — zarówno przez nieaktualne kursy, jak i pomyłki przy ręcznym wpisywaniu. Projekt rozwiązuje ten problem przez automatyczne pobieranie aktualnych kursów bezpośrednio ze źródła i podłączenie ich do procesu przeliczania.

## Źródło danych
- **API Europejskiego Banku Centralnego (EBC)** — oficjalne, darmowe źródło referencyjnych kursów walut, aktualizowane na bieżąco. Dane pobierane bezpośrednio w Power Query bez potrzeby ręcznego eksportu czy pobierania plików.

## Metodologia / przepływ pracy
1. **Pobranie danych** — połączenie z API EBC w Power Query i pobranie aktualnych kursów walut (CHF, PLN → EUR).
2. **Transformacja** — dopasowanie formatu kursów do struktury danych transakcyjnych (typy danych, nazwy kolumn, granularność czasowa).
3. **Łączenie danych** — połączenie tabeli transakcji (kwoty w walucie lokalnej) z tabelą kursów po kluczu waluta + data.
4. **Przeliczenie** — obliczenie kolumny `EUR_Amount` jako kwota lokalna × odpowiedni kurs.
5. **Wynik końcowy** — jednolity zbiór danych z kwotami wyrażonymi w EUR, gotowy do dalszej analizy finansowej lub raportowania.

## Kluczowe funkcjonalności
- **Automatyczne pobieranie danych** — kursy walut pobierane bezpośrednio z API EBC przy użyciu Power Query, bez ręcznej ingerencji.
- **Eliminacja błędów ręcznych** — brak potrzeby ręcznego wpisywania czy aktualizowania kursów walut.
- **Ujednolicenie danych** — przygotowanie spójnego zbioru danych (`EUR_Amount`) niezależnie od waluty źródłowej transakcji.
- **Powtarzalność** — proces można odświeżyć jednym kliknięciem (Refresh w Power Query) zamiast powtarzać ręczną pracę przy każdej aktualizacji danych.

## Wykorzystane narzędzia
- MS Excel (Power Query / Power Query M)
- API Europejskiego Banku Centralnego (EBC)

## Ograniczenia
- Projekt obsługuje obecnie dwie waluty źródłowe (CHF, PLN) — rozszerzenie na kolejne waluty wymaga dodania ich do zapytania API.
- Kursy pobierane są jako kursy referencyjne EBC (publikowane raz dziennie) — nie są to kursy transakcyjne banków komercyjnych, co może powodować niewielkie odchylenia względem rzeczywistych rozliczeń.
- Proces nie zawiera automatycznej walidacji poprawności danych wejściowych (np. wykrywania duplikatów transakcji).
```

## Autor
[drnvgt](https://github.com/drnvgt)
