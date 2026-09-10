# 10 - Szablon Analizy: Dla Twojej Samodzielnej Pracy

## 📋 UNIWERSALNY SZABLON DO ANALIZY MAŁOSYGNAŁOWEJ

Użyj tego szablonu za każdym razem gdy dostajesz nowy schemat do analizy. Wystarczy wydrukować i wpisać dane.

---

## 📝 ARKUSZ ROBOCZY - ANALIZA TRANZYSTORA

**Data:** ____________  
**Schemat nr:** ____________  
**Student:** ____________  

---

### CZĘŚĆ 1: IDENTYFIKACJA ELEMENTÓW

```
TRANZYSTOR:
┌─────────────────────────────────────────┐
│ Typ:                [ ] NPN [ ] PNP      │
│                     [ ] JFET [ ] MOSFET  │
│ Model: ________________                 │
│ h₁₁ = _____ Ω                           │
│ h₂₁ = _____                             │
│ h₁₂ = _____ (zwykle ≈ 0)                │
│ h₂₂ = _____ (zwykle ≈ 0)                │
└─────────────────────────────────────────┘

ZASILANIE:
Ucc = _____ V

REZYSTORY:
├─ Rc (kolektora) = _____ Ω
├─ Re (emitera) = _____ Ω   [ ] istnieje [ ] nie ma
├─ Rb (polaryzacji) = _____ Ω
├─ Rs (źródła) = _____ Ω
└─ Ry (obciążenia) = _____ Ω  [ ] istnieje [ ] nie ma

KONDENSATORY:
├─ Ca (wejścia) = _____ F   [ ] istnieje [ ] nie ma
├─ Ce (emitera) = _____ F   [ ] istnieje [ ] nie ma
└─ Cs (wyjścia) = _____ F   [ ] istnieje [ ] nie ma

ŹRÓDŁO SYGNAŁU:
├─ Amplituda: _____ V
├─ Częstotliwość: _____ Hz
└─ Impedancja: _____ Ω
```

---

### CZĘŚĆ 2: ANALIZA DC (PUNKT PRACY)

**Schemat DC:** (narysuj bez kondensatorów)

```
┌─────────────────────────────────────────┐
│                                         │
│      Tutaj narysuj schemat DC           │
│                                         │
│                                         │
│                                         │
└─────────────────────────────────────────┘
```

**Obliczenia:**

```
OBWÓD BAZY (DC):

U_BE ≈ 0.6V dla Si, 0.2V dla Ge

Prawo Kirchhoffa:
Ucc = I_B · Rb + U_BE + I_E · Re

Gdzie I_E ≈ I_C (emiter ≈ kolektor)

Ucc = I_B · Rb + U_BE + I_B · h₂₁ · Re

_____ = I_B · _____ + 0.6 + I_B · _____ · _____

_____ - 0.6 = I_B · (_____ + _____)

I_B = (_____ - 0.6) / (_____ + _____)

I_B = _____ mA
```

**Prąd kolektora:**

```
I_C = h₂₁ · I_B

I_C = _____ · _____ mA

I_C = _____ mA
```

**Napięcie U_CE:**

```
Obwód kolektora:
Ucc = I_C · Rc + U_CE + I_E · Re

Przyjmując I_E = I_C:

_____ = _____ · _____ + U_CE + _____ · _____

_____ = _____ + U_CE + _____

U_CE = _____ - _____ - _____

U_CE = _____ V

✓ Sprawdzenie: U_CE > 0.2V?  [ ] TAK  [ ] NIE
  Jeśli nie: tranzystor jest nasycony!
```

**Wynik DC:**

```
┌─────────────────────────────────────────┐
│ I_B = _____ mA                          │
│ I_C = _____ mA                          │
│ I_E = _____ mA                          │
│ U_BE = _____ V                          │
│ U_CE = _____ V                          │
│ Punkt pracy: [ ] Aktywny [ ] Nasycony  │
└─────────────────────────────────────────┘
```

---

### CZĘŚĆ 3: ANALIZA AC (MODEL MAŁOSYGNAŁOWY)

**Schemat AC:** (narysuj z kondensatorami jako zwarcia, zasilanie jako masa)

```
┌─────────────────────────────────────────┐
│                                         │
│      Tutaj narysuj schemat AC           │
│      z modelem h-parametrów             │
│                                         │
│                                         │
│                                         │
└─────────────────────────────────────────┘
```

**Impedancja wejściowa:**

```
Z_in = Rs + (h₁₁ || Rb)

Równoległy h₁₁ i Rb:
(h₁₁ || Rb) = (h₁₁ · Rb) / (h₁₁ + Rb)

(h₁₁ || Rb) = (_____ · _____) / (_____ + _____)

(h₁₁ || Rb) = _____ / _____

(h₁₁ || Rb) = _____ Ω

Z_in = _____ + _____

Z_in = _____ Ω
```

**Impedancja wyjściowa:**

```
Jeśli NIE ma obciążenia (Ry → ∞):
Z_out = Rc

Z_out = _____ Ω

───────────────────────────────

Jeśli JEST obciążenie:
Z_out = Rc || Ry

Z_out = (Rc · Ry) / (Rc + Ry)

Z_out = (_____ · _____) / (_____ + _____)

Z_out = _____ / _____

Z_out = _____ Ω
```

---

### CZĘŚĆ 4: WZMOCNIENIE NAPIĘCIOWE (ku)

**Wybierz odpowiednią konfigurację:**

```
[ ] A) BEZ Ce, BEZ obciążenia
        ku = -h₂₁ · Rc / h₁₁

[ ] B) Z Ce, BEZ obciążenia
        ku = -h₂₁ · Rc / h₁₁

[ ] C) BEZ Ce, Z obciążeniem
        ku = -h₂₁ · (Rc || Ry) / (h₁₁ + h₂₁ · Re)

[ ] D) Z Ce, Z obciążeniem
        ku = -h₂₁ · (Rc || Ry) / h₁₁
```

**Obliczenia:**

```
R_out = _____ Ω (używane w formule)

ku = -h₂₁ · R_out / h₁₁

ku = -_____ · _____ / _____

ku = -_____ / _____

ku = _____
```

**Interpretacja:**

```
Wzmocnienie: _____ razy

[ ] Dodatnie (sygnał w fazie)
[ ] Ujemne (sygnał przesunięty o 180°)

Amplituda wyjścia ≈ |ku| · amplituda wejścia
Amplituda wyjścia ≈ _____ · 1V = _____ V
```

---

### CZĘŚĆ 5: CZĘSTOTLIWOŚCI GRANICZNE

**Jeśli Ca istnieje:**

```
f_c_Ca = 1 / (2π · Ca · (Rs + Z_in_bez_Ca))

Z_in_bez_Ca = h₁₁ || Rb = _____ Ω

f_c_Ca = 1 / (2π · _____ · (_____ + _____))

f_c_Ca = 1 / (2π · _____ · _____) 

f_c_Ca = 1 / (2π · _____)

f_c_Ca ≈ _____ Hz
```

**Jeśli Ce istnieje:**

```
f_c_Ce = 1 / (2π · Ce · Re)

f_c_Ce = 1 / (2π · _____ · _____)

f_c_Ce = 1 / (2π · _____)

f_c_Ce ≈ _____ Hz
```

**Jeśli Cs istnieje:**

```
f_c_Cs = 1 / (2π · Cs · Z_out)

f_c_Cs = 1 / (2π · _____ · _____)

f_c_Cs = 1 / (2π · _____)

f_c_Cs ≈ _____ Hz
```

**Dolna częstotliwość graniczna (f_dolna):**

```
f_dolna = max(f_c_Ca, f_c_Ce, f_c_Cs)

f_dolna ≈ _____ Hz

(Wybierz największą z obliczonych częstotliwości)
```

---

### CZĘŚĆ 6: PODSUMOWANIE WYNIKÓW

```
┌─────────────────────────────────────────────────────┐
│ WYNIKI ANALIZY                                      │
├─────────────────────────────────────────────────────┤
│                                                     │
│ IMPEDANCJE:                                         │
│ ├─ Z_in = _____ Ω                                   │
│ └─ Z_out = _____ Ω                                  │
│                                                     │
│ WZMOCNIENIE:                                        │
│ ├─ ku = _____                                       │
│ ├─ |ku| = _____ (wartość bezwzględna)               │
│ └─ Przesunięcie fazy: [ ] 0°  [ ] 180°             │
│                                                     │
│ PASMO PRZENOSZENIA:                                 │
│ ├─ f_dolna = _____ Hz                               │
│ ├─ f_górna = _____ Hz (jeśli dana)                  │
│ └─ Pasmo = _____ Hz                                 │
│                                                     │
│ CHARAKTERYSTYKA:                                    │
│ ├─ Konfiguracja: Wspólny emiter                    │
│ ├─ Typ wzmacniacza: [ ] napięciowy                 │
│ │                  [ ] prądowy                      │
│ │                  [ ] mocy                         │
│ ├─ Stabilność: [ ] dobra [ ] słaba                 │
│ └─ Uwagi: _____________________________             │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

### CZĘŚĆ 7: WERYFIKACJA WYNIKÓW

**Sprawdzenie logiczne:**

```
[ ] Z_in jest kilka k ohmów (ma sens dla CE)
[ ] Z_out jest kilka k ohmów (ma sens dla CE)
[ ] |ku| jest 10-1000 (ma sens dla CE)
[ ] Sygnał jest odwrócony (minus ku)
[ ] Punkt pracy jest w obszarze aktywnym
[ ] Kondensatory wyznaczają pasmo
[ ] Wszystkie obliczenia są w jednostkach SI
```

**Jeśli coś nie gra:**

```
Sprawdzę:
[ ] Czy dobrze przepisałem wartości ze schematu?
[ ] Czy h-parametry są poprawne?
[ ] Czy rozpoznałem konfigurację (CA, Ce, Cs)?
[ ] Czy prawidłowo obliczyłem równoległy?
[ ] Czy używam prawidłowego wzoru na ku?
[ ] Czy punkt pracy ma sens?
```

---

### CZĘŚĆ 8: DODATKOWE NOTATKI

```
┌─────────────────────────────────────────┐
│ OBSERWACJE I UWAGI:                     │
│                                         │
│ _____________________________________   │
│                                         │
│ _____________________________________   │
│                                         │
│ _____________________________________   │
│                                         │
│ _____________________________________   │
│                                         │
│ _____________________________________   │
│                                         │
└─────────────────────────────────────────┘
```

---

## 💡 WSKAZÓWKI DO SZABLONU

### Kiedy go używać:
- ✅ Na każdych zajęciach (nowy schemat)
- ✅ Przy przygotowaniu do kolokwium
- ✅ Przy ćwiczeniach domowych
- ✅ Gdy chcesz sprawdzić swoją logikę

### Jak go wypełniać:
1. Wydrukuj szablon (jedna strona lub dwie)
2. Czytaj UWAŻNIE schemat
3. Wypełniaj po kolei każdą sekcję
4. Rób obliczenia na papierze (nie w głowie!)
5. Dwukrotnie sprawdzaj jednostki
6. Narysuj schematy AC i DC
7. Porównaj wynik z oczekiwaniami

### Co jeśli brakuje ci miejsca?
- Użyj drugiej kartki
- Rób notatki mniejszym pismem
- Możesz zrobić sobie własną wersję szablonu

---

## 🚀 Gotowy Do Pracy!

Teraz masz **wszystkie narzędzia** do analizy małosygnałowej:

1. ✅ Teoretyczne podstawy (h-parametry)
2. ✅ Metodę budowania modelu
3. ✅ Praktyczne przykłady (4 różne)
4. ✅ Schemat pracy (algorytm)
5. ✅ Szablon analizy (do każdego schematu)

---

## 📞 Gdy Się Zacinasz

```
PROBLEM → CO ROBIĆ

"Nie wiem, jak zamodelować
 tranzystor"
→ Wróć do 01_Podstawy_teoretyczne.md

"Nie rozumiem kondensatorów"
→ Przeczytaj 02_Model_malosynalowy.md

"Nie potrafię czytać schematów"
→ Przejrzyj 03_Czytanie_schematu.md

"Nie wiem jakiego wzoru użyć"
→ Sprawdź 04_Wspólny_Emiter.md

"Moja analiza nie ma sensu"
→ Porównaj z przykładami 05-08

"Nie wiem co robić krok po kroku"
→ Czytaj 09_Schemat_Pracy.md

"Chcę trenować na nowych schematach"
→ Używaj szablonu 10_Szablon_Analizy.md
```

---

**POWODZENIA Z NAUKĄ! 🚀⚡**
