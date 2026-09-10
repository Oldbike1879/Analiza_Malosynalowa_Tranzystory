# 09 - Schemat Pracy: Krok po Kroku do Prawidłowej Analizy

## 🎯 Cel

Ten dokument pokazuje **dokładnie co i w jakiej kolejności robić**, gdy dostajesz schemat do analizy na zajęciach.

## 📋 ALGORYTM ANALIZY MAŁOSYGNAŁOWEJ

### FAZA 1: PRZYGOTOWANIE (2-3 minuty)

```
┌─────────────────────────────────────────┐
│ STEP 1: PRZECZYTAJ SCHEMAT              │
├─────────────────────────────────────────┤
│ ☑ Czy widzę tranzystor?                 │
│ ☑ Jaki typ? (NPN, PNP, JFET, MOSFET?)  │
│ ☑ Gdzie jest baza, kolektor, emiter?    │
│ ☑ Podane są h-parametry?                │
│ ☑ Jaka wartość Ucc?                     │
└─────────────────────────────────────────┘
        ↓
┌─────────────────────────────────────────┐
│ STEP 2: ZIDENTYFIKUJ ELEMENTY           │
├─────────────────────────────────────────┤
│ ☑ Rc (rezystor kolektora)               │
│ ☑ Re (rezystor emitera) - jeśli istnieje│
│ ☑ Rb (rezystor polaryzacji bazy)        │
│ ☑ Rs (rezystor źródła)                  │
│ ☑ Ry (rezystor obciążenia)              │
│ ☑ Ca (kondensator wejścia)              │
│ ☑ Ce (kondensator emitera)              │
│ ☑ Cs (kondensator wyjścia)              │
└─────────────────────────────────────────┘
        ↓
┌─────────────────────────────────────────┐
│ STEP 3: WYPISZ WSZYSTKIE WARTOŚCI       │
├─────────────────────────────────────────┤
│ Ucc = _____ V                           │
│ Rc = _____ Ω                            │
│ Re = _____ Ω (lub brak)                 │
│ Rb = _____ Ω (lub R1+R2 dzielnik)       │
│ Rs = _____ Ω                            │
│ Ry = _____ Ω (lub nieskończoność)       │
│ Ca = _____ F (lub brak)                 │
│ Ce = _____ F (lub brak)                 │
│ Cs = _____ F (lub brak)                 │
│ h₁₁ = _____ Ω                           │
│ h₂₁ = _____                             │
└─────────────────────────────────────────┘
```

### FAZA 2: ANALIZA DC (5-10 minut)

```
┌─────────────────────────────────────────┐
│ STEP 4: PUNKT PRACY (jeśli wymagany)    │
├─────────────────────────────────────────┤
│ A) Rysuj schemat DC (bez kondensatorów) │
│ B) Oblicz I_B = (Ucc - U_BE) / Rb       │
│ C) Oblicz I_C = h₂₁ · I_B               │
│ D) Oblicz U_CE = Ucc - I_C·Rc - I_C·Re  │
│                                         │
│ WYNIK:                                  │
│ I_B = _____ mA                          │
│ I_C = _____ mA                          │
│ U_CE = _____ V                          │
│                                         │
│ ⚠️ Sprawdzenie: U_CE > 0,2V?            │
│    (Jeśli < 0,2V: tranzystor nasycony) │
│    (Jeśli < 0V: BŁĄD w obliczeniach!)   │
└─────────────────────────────────────────┘
```

### FAZA 3: ANALIZA AC - MODEL MAŁOSYGNAŁOWY (10-15 minut)

```
┌─────────────────────────────────────────┐
│ STEP 5: MODEL AC                        │
├─────────────────────────────────────────┤
│ A) Rysuj schemat AC:                    │
│    - Usuwaj kondensatory (stają się zwartami) │
│    - Zasilanie Ucc → masa               │
│    - Rezystory pozostają                │
│    - Tranzystor → model h-parametrów    │
│                                         │
│ B) Oblicz impedancje                    │
│                                         │
│    Z_in = Rs + (h₁₁ || Rb)              │
│    Z_in = _____ Ω                       │
│                                         │
│    Z_out = Rc || Ry (jeśli Ry istnieje) │
│    Z_out = _____ Ω                      │
└─────────────────────────────────────────┘
        ↓
┌─────────────────────────────────────────┐
│ STEP 6: WZMOCNIENIE NAPIĘCIOWE (ku)    │
├─────────────────────────────────────────┤
│ Wzór podstawowy:                        │
│                                         │
│ ku = -h₂₁ · R_out / h₁₁                 │
│                                         │
│ Gdzie:                                  │
│ h₂₁ = _____ (dany)                      │
│ h₁₁ = _____ Ω (dany)                    │
│ R_out = Rc lub (Rc||Ry) lub (Rc||Ry+Re)│
│ R_out = _____ Ω                         │
│                                         │
│ WYNIK:                                  │
│ ku = _____ (liczba bez jednostki)       │
│ Interpretacja: sygnał wzmacniany ku     │
│                razy (minus = odwróci)   │
└─────────────────────────────────────────┘
        ↓
┌─────────────────────────────────────────┐
│ STEP 7: CZĘSTOTLIWOŚCI GRANICZNE        │
├─────────────────────────────────────────┤
│ Jeśli Ca istnieje:                      │
│ f_c_Ca = 1 / (2π · Ca · (Rs+Z_in))      │
│ f_c_Ca = _____ Hz                       │
│                                         │
│ Jeśli Ce istnieje:                      │
│ f_c_Ce = 1 / (2π · Ce · Re)             │
│ f_c_Ce = _____ Hz                       │
│                                         │
│ Jeśli Cs istnieje:                      │
│ f_c_Cs = 1 / (2π · Cs · Z_out)          │
│ f_c_Cs = _____ Hz                       │
└─────────────────────────────────────────┘
```

### FAZA 4: PODSUMOWANIE I WNIOSKI (5 minut)

```
┌─────────────────────────────────────────┐
│ STEP 8: TABELA WYNIKÓW                  │
├─────────────────────────────────────────┤
│                                         │
│ IMPEDANCJE:                             │
│ Z_in = _____ Ω                          │
│ Z_out = _____ Ω                         │
│                                         │
│ WZMOCNIENIE:                            │
│ ku = _____                              │
│                                         │
│ PASMO:                                  │
│ f_dolna = _____ Hz                      │
│ f_górna = _____ Hz (jeśli dane)         │
│                                         │
│ CHARAKTERYSTYKA:                        │
│ Konfiguracja: wspólny emiter            │
│ Typ: [ ] wzmacniacz [ ] buffer [ ] inne │
│ Zastosowanie: _____________________     │
│                                         │
└─────────────────────────────────────────┘
        ↓
┌─────────────────────────────────────────┐
│ STEP 9: KRYTYCZNA ANALIZA               │
├─────────────────────────────────────────┤
│                                         │
│ ☑ Czy ku jest realistyczne?             │
│   (Zwykle 10-1000 dla CE)               │
│                                         │
│ ☑ Czy impedancje mają sens?             │
│   Z_in: k ohmy (tysiące)                │
│   Z_out: kilka k ohmów (kolektora)      │
│                                         │
│ ☑ Czy punkt pracy jest w obszarze       │
│   aktywnym? (0.2V < U_CE < Ucc-1V)      │
│                                         │
│ ☑ Czy kondensatory wyznaczają pasmo?    │
│   (Powinny być znaczniki f_c)            │
│                                         │
│ Jeśli coś wygląda dziwnie → sprawdź    │
│ obliczenia jeszcze raz!                 │
│                                         │
└─────────────────────────────────────────┘
```

## 🧮 Wzory do Szybkiego Dostępu

### Impedancje:

```
Z_in = Rs + (h₁₁ || Rb)

Z_out = Rc || (1/h₂₂)  ≈ Rc  (gdy h₂₂ ≈ 0)

(R1 || R2) = (R1 · R2) / (R1 + R2)

Parallel.rezystorów:
- Dwa rezystory: (R1 · R2) / (R1 + R2)
- Trzy rezystory: 1 / (1/R1 + 1/R2 + 1/R3)
```

### Wzmocnienie:

```
ku = -h₂₁ · R_out / h₁₁

Gdzie R_out:
- Bez Ce, bez obciążenia: R_out = Rc
- Z Ce, bez obciążenia: R_out = Rc
- Bez Ce, z obciążeniem: R_out = Rc || Ry
- Z Ce, z obciążeniem: R_out = Rc || Ry
```

### Częstotliwości graniczne:

```
f_c = 1 / (2π · C · R)

f_c_Ca = 1 / (2π · Ca · (Rs + (h₁₁||Rb)))
f_c_Ce = 1 / (2π · Ce · Re)
f_c_Cs = 1 / (2π · Cs · (Rc||Ry))
```

## 🎬 Przykładowy Przebieg Analizy (5 minut)

```
SCHEMAT:
        +12V
         │
        10k (Rc)
         │
     ┌───┤ NPN
 100k ├──┤ h₂₁=100, h₁₁=2k
     │   │
    sin  ├─ 1k (Re)
    1V   │
    1k  GND
     │
    GND

ANALIZA:

1. ELEMENTY:
   Ucc=12V, Rc=10k, Rb=100k, Re=1k, Rs=1k
   h₂₁=100, h₁₁=2k
   Brak Ca, Ce, Cs

2. PUNKT PRACY (DC):
   I_B = (12-0.7)/(100k+1k) = 0.11 mA
   I_C = 100 · 0.11 = 11 mA
   U_CE = 12 - 11m·10k - 11m·1k = -109V
   ⚠️ PROBLEM! Tranzystor nasycony!

3. MODEL AC:
   Z_in = 1k + (2k || 100k) = 1k + 1.96k = 2.96k Ω
   Z_out = 10k Ω (brak obciążenia)

4. WZMOCNIENIE:
   ku = -100 · 10k / 2k = -500

5. WNIOSKI:
   - Punkt pracy źle dobrany
   - Impedancja wejścia: 3 kΩ
   - Impedancja wyjścia: 10 kΩ
   - Teoretyczne wzmocnienie: -500
   - Problem: Re bez Ce → wzmocnienie będzie zredukowane
```

## 🚀 Praktyczne Wskazówki

```
KIEDY MASZ PROBLEM:

1. Czytaj schemat BARDZO UWAŻNIE
   - Czasem połączenia są na górze, nie na dole
   - Rezystory mogą być jak linie
   - Kondensatory mogą być pominięte

2. Rób model AC na osobnej kartce
   - Zamieniaj kondensatory na zwarcia
   - Zamieniaj zasilanie na masę
   - Rysuj model h-parametrów

3. Jeśli wynik wygląda dziwnie:
   - Sprawdzić zasilanie (Ucc)
   - Sprawdzić wartości rezystorów
   - Sprawdzić h-parametry
   - Sprawdzić czy punkt pracy jest prawidłowy

4. Zawsze zapisuj jednostki:
   - [Ω] dla rezystancji
   - [S] dla admitancji
   - [Hz] dla częstotliwości
   - [mA] dla prądów
   - [V] dla napięć

5. Używaj kalkulatora z funkcjami:
   - Mnożenie i dzielenie
   - π (3.14159...)
   - Pierwiastki (dla obliczeń pochodnych)
```

## 📝 Checklist Przed Zakończeniem Analizy

- [ ] Przeczytałem schemat poprawnie
- [ ] Zidentyfikowałem wszystkie elementy
- [ ] Obliczył/a punkt pracy (jeśli wymagany)
- [ ] Narysowałem/a model AC
- [ ] Obliczyłem/a impedancje wejścia i wyjścia
- [ ] Obliczyłem/a wzmocnienie (ku)
- [ ] Obliczyłem/a częstotliwości graniczne
- [ ] Sprawdziłem/a czy wyniki mają sens
- [ ] Zapisałem/a jednostki przy każdej wartości
- [ ] Mogę wyjaśnić każdy krok komuś innemu

## 🎯 Następny Krok

Teraz nauczysz się używać **szablonu do samodzielnej analizy**.

→ Przejdź do **10_Szablon_Analizy.md**
