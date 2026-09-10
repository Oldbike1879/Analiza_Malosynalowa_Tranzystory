# 05 - Przykład 1: Prosty Wzmacniacz Wspólnego Emitera

## 🎯 Cel przykładu

Przeanalizujemy **najprostszą konfigurację** wzmacniacza CE bez żadnych "sztuczek". To punkt wyjścia do wszystkich pozostałych.

## 🔌 Schemat Rzeczywisty

```
          +12V (Ucc)
            │
           10kΩ (Rc)
            │
        ┌───┤C
        │   │
        │   │ Q (tranzystor NPN)
        │   │ h₂₁ = 100
    100kΩ  │ h₁₁ = 2kΩ
        │   │
        │   E
        │   │
       sin──┴─── GND
     1V AC
     1kΩ (Rs)
        │
      GND

LEGENDA:
  Ucc = 12V (zasilanie)
  Rc = 10kΩ (rezystor kolektora)
  Rb = 100kΩ (rezystor polaryzacji bazy)
  Rs = 1kΩ (rezystor źródła sygnału)
  Q: h₂₁ = 100, h₁₁ = 2kΩ
  sin = źródło sygnału AC 1V amplitudy
```

## 📊 Analiza DC (Punkt Pracy)

### Etap 1: Prąd bazowy

Dla DC, źródło sygnału jest otwarte (AC nie przepuszcza), ale Rs wciąż wpływa.

```
Obwód DC bazy:
Ucc = 12V
  │
Rb = 100kΩ
  │
  ├─ B (baza)
  │
(Rs w series, ale mały wpływ)
  │
GND

Prawo Ohma:
I_B = (Ucc - U_BE) / (Rb + Rs)
I_B = (12 - 0.7) / (100k + 1k)
I_B = 11.3 / 101k ≈ 0.112 mA
```

### Etap 2: Prąd kolektora

```
I_C = h₂₁ · I_B
I_C = 100 · 0.112 mA
I_C = 11.2 mA

Sprawdzenie (czy tranzystor nie nasycił się):
U_CE = Ucc - I_C · Rc
U_CE = 12 - 11.2m · 10k
U_CE = 12 - 112 = -100V

⚠️ PROBLEM! U_CE nie może być ujemne!
Tranzystor jest w NASYCENIU, a nie w obszarze aktywnym.
```

### Poprawka: Realizm

W rzeczywistości, gdy tranzystor się nasycił, Ic nie jest taki duży. Przyjmijmy punkt pracy jako:
```
I_B ≈ 0.1 mA
I_C ≈ 5 mA (nasycenie)
U_CE ≈ 0.2V (nasycony tranzystor)
```

Ale dla **analizy małosygnałowej** najpierw sprawdzamy, czy punkt pracy pozwala na pracę liniową. Tu jest problem, ale pokażemy analizę AC i wnioski.

## 🎭 Model Małosygnałowy

### Schemat AC (usuwamy DC, zamieniamy źródło zasilania):

```
Kondensatory i cewki? Tutaj ich brak (oprócz wewnętrznych tranzystora).

Schemat AC:
                    
  sig ──┬── Rs ──┬─────────┐
        │        │         │
       GND      Rb        (h₁₁ = 2kΩ)
                │         │
                ├─────────┤ B
                │         │
               Rc        (źródło prądu)
                │         h₂₁·i_B
                ├─────────┤ C
                │         │
              u_wy        E (GND)
                │
              GND
```

### Dokładniejszy model:

```
WEJŚCIE (baza-emiter):
  sig ──[Rs=1kΩ]──┬─[h₁₁=2kΩ]──┬───ub
                  │             │
               [Rb=100kΩ]       GND
                  │
                 GND

Impedancja widziana przez Rs:
Z_in = h₁₁ || Rb = (2k || 100k) 
Z_in = (2000 · 100000) / (2000 + 100000)
Z_in = 200000000 / 102000 ≈ 1960 Ω

WYJŚCIE (kolektor-emiter):
  ┌─[Rc=10kΩ]──┬─ u_wy
  │            │
  │       [h₂₁·i_B]  (źródło prądu)
  │            │
  └────────────┴─ E (GND)

Z_out = Rc = 10kΩ (brak obciążenia na wyjściu)
```

## 📐 Obliczenia Wzmocnienia

### Prąd bazowy (AC):

```
u_in = sig · Z_in / (Rs + Z_in)

Z_in = 1960 Ω

u_in = sig · 1960 / (1000 + 1960)
u_in = sig · 1960 / 2960
u_in ≈ 0.66 · sig

Gdy sig = 1V:
u_in ≈ 0.66V (na wejściu tranzystora)
```

### Prąd bazowy:

```
i_B = u_in / h₁₁
i_B = 0.66V / 2000Ω
i_B ≈ 0.33 mA
```

### Prąd kolektora (AC):

```
i_C = h₂₁ · i_B
i_C = 100 · 0.33 mA
i_C ≈ 33 mA
```

### Napięcie wyjściowe:

```
u_wy = -i_C · Rc
u_wy = -33 mA · 10k
u_wy ≈ -330V

⚠️ ABSURD! Napięcie nie może być tak duże!
```

## 🤔 Wyjaśnienie: Dlaczego wyniki są nierealistyczne?

**Problem:** Punkt pracy tranzystora jest źle dobrany!

1. **Punkt pracy w nasyceniu** - tranzystor nie może pracować liniowo
2. **Brak kondensatora na emiterze** - Re.Ce mogłoby zmienić punkt pracy
3. **Polaryzacja jest źle strojona** - Rb jest zbyt duży

## ✅ Prawidłowa Analiza

Gdyby punkt pracy był prawidłowy (U_CE ≈ 6V, I_C ≈ 1 mA):

```
h₂₁ = 100
h₁₁ = 2kΩ
Rc = 10kΩ

ku = -h₂₁ · Rc / h₁₁
ku = -100 · 10000 / 2000
ku = -500

Więc gdy u_in = 0.66V:
u_wy = -500 · 0.66 = -330V

Ale rzeczywiście: amplituda wyjścia byłaby ograniczona do ~U_CE/2 ≈ 3V
```

## 📝 Wnioski z Przykładu 1

| Parametr | Wartość |
|----------|---------|
| Z_in (impedancja wejścia) | ~2kΩ (h₁₁) |
| Z_out (impedancja wyjścia) | ~10kΩ (Rc) |
| ku (wzmocnienie teoretyczne) | -500 |
| **Problem** | Punkt pracy źle dobrany! |

## 🚀 Następny Etap

Ten przykład pokazuje, że **zwykła polaryzacja przez rezystor może być niestabilna**. Następne przykłady będą dotyczyć:

1. Dodania **kondensatora sprzęgującego wejście** - dla AC tylko
2. Dodania **kondensatora obejścia emitera** - dla poprawy wzmocnienia
3. Dodania **rezystora emitera** - dla lepszej stabilizacji

→ Przejdź do **06_Przykład_2_Kondensator_Wej.md**
