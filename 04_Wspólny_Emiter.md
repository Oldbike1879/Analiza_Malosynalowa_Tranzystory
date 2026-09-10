# 04 - Wspólny Emiter: Pełna Analiza

## 🎯 Co to jest konfiguracja wspólnego emitera?

**Wspólny Emiter (Common Emitter - CE)** to najczęściej używana konfiguracja tranzystora bipolarnego. Nazwa pochodzi stąd, że **emiter jest wspólnym punktem dla wejścia i wyjścia**.

```
Schemat topologiczny:

Wejście (baza)  ────┐
                     ├─── TRANZYSTOR ───┬──── Wyjście (kolektor)
Masa (emiter)   ────┘                   │
                                        └──── Masa
```

## 📊 Charakterystyka konfiguracji CE

| Cecha | Wartość |
|-------|---------|
| **Wzmocnienie napięciowe** | Wysokie (10-1000) |
| **Wzmocnienie prądowe** | Średnie (~h₂₁) |
| **Impedancja wejściowa** | Średnia (kΩ) |
| **Impedancja wyjściowa** | Wysoka (≈ Rc) |
| **Przesunięcie fazy** | 180° (sygnał odwrócony) |
| **Pasmo przenoszenia** | Średnie do szerokie |

## 🔌 Typowy Schemat CE

```
          +Ucc (zasilanie, np. 12V)
            │
           Rc (rezystor kolektora)
            │
       ┌────┤C
   Cs  │ B  │
  ──┬──┤    │ Q (tranzystor)
    │  Rb   │
    │  │    E (emiter do masy)
    │  │    │
   sig ├────┘
    │  │
   Rs  Rb2
    │  │
   GND ─┴─ GND

LEGENDA:
  Ucc = zasilanie (12V)
  Rc = rezystor kolektora (~1k-10k Ω)
  Rb = rezystor polaryzacji bazy
  Rs = rezystor źródła sygnału (~1k Ω)
  Cs = kondensator sprzęgujący wyjście
  sig = źródło sygnału AC
```

## 📐 Analiza DC (Punkt Pracy)

### Etap 1: Wyznacz prąd bazowy

Gdy kondensatory są otwarte (dla DC):

```
Ucc
 │
Rb (rezystor polaryzacji)
 │
├─── B (baza)
 │
│ (tu wstawić rezystor źródła Rs jeśli ma znaczenie)
 │
GND

Prawo Ohma dla obwodu bazy:
I_B = (Ucc - U_BE) / Rb

Gdzie U_BE ≈ 0.6-0.7V dla tranzystora Si
```

### Etap 2: Oblicz prąd kolektora

```
Z równania tranzystora:
I_C = β · I_B

Gdzie β ≈ h₂₁ (wzmocnienie prądowe)

Lub (gdy znamy punkt pracy z datasheetu):
I_C = h₂₁ · I_B
```

### Etap 3: Wyznacz napięcie U_CE

```
Obwód kolektora:
Ucc
 │
Rc
 │
├─── C (kolektor)
 │
U_CE (szukane!)
 │
E (emiter) ─── GND

Prawo napięciowe Kirchhoffa:
Ucc = I_C · Rc + U_CE

Stąd:
U_CE = Ucc - I_C · Rc
```

## 🎭 Model Małosygnałowy CE

Gdy tranzystor pracuje w punkcie Q, możemy go zastąpić modelem:

```
MODEL WEJŚCIA (baza-emiter):

    ┌─── h₁₁ ───┐
    │            ├─── u_BE (zmiana napięcia)
i_B ├───┐        │
    │   └─ h₁₂·u_CE

MODEL WYJŚCIA (kolektor-emiter):

    ┌────────┬─── i_C = h₂₁·i_B + h₂₂·u_CE
u_CE ┤        │
    └─ 1/h₂₂ ─┘

Połączone w schemat:

        Rc
        ├──┐
        │  ├──── u_wy (wyjście AC)
   i_B  │  │
   ────┬┤  │
        │ [h₂₁·i_B]  (źródło prądu)
        │  │
    h₁₁ ├──┘
        │
       GND
```

## 📝 Krok po Kroku: Analiza Małosygnałowa

### Dane wejściowe:
- Ucc = ? V
- Rc = ? Ω
- Rb = ? Ω
- h₁₁ = ? Ω
- h₂₁ = ?
- Rs = ? Ω (rezystor źródła)
- Ry = ? Ω (rezystor obciążenia, jeśli istnieje)

### Krok 1: Oblicz impedancję wejściową widzianą przez źródło

```
Wejście do bazy tranzystora = h₁₁

Impedancja całkowita wejścia (widziana przez Rs):
Z_in = h₁₁ || Rb

(||  oznacza połączenie równolegle)

Wzór na równoległy:
Z_in = (h₁₁ · Rb) / (h₁₁ + Rb)
```

### Krok 2: Oblicz impedancję wyjściową

```
Na wyjściu mamy Rc równolegle z obciążeniem Ry (jeśli istnieje).

Z_out = Rc || (1/h₂₂)

Gdy h₂₂ ≈ 0 (admitancja bardzo mała):
Z_out ≈ Rc

Gdy jest obciążenie Ry:
Z_out = Rc || Ry = (Rc · Ry) / (Rc + Ry)
```

### Krok 3: Oblicz wzmocnienie napięciowe (ku)

```
Wzmocnienie między bazą i emiterem a kolektorem i emiterem:

ku = -h₂₁ · (Rc || Ry) / h₁₁

Znak minus oznacza przesunięcie fazy o 180°

Gdy brak obciążenia (Ry → ∞):
ku = -h₂₁ · Rc / h₁₁

Przykład liczbowy:
h₂₁ = 100, Rc = 1000 Ω, h₁₁ = 2000 Ω
ku = -100 · 1000 / 2000 = -50
```

## 🧮 Efekt Rezystora Emitera (Re)

Gdy emiter nie jest bezpośrednio do masy, ale przez rezystor Re:

```
SCHEMAT Z Re:
       +Ucc
        │
       Rc
        │
    ┌───┤C
    │   │
   Rb  │ Q
    │  │
    │  E
    │  │
    │ Re (rezystor emitera)
    │  │
    └──┴─ GND

Dla DC: Punkt pracy zmienia się, rezystor stabilizuje pracę
Dla AC: Model się komplikuje, ale można uprościć

Jeśli Re ma zwarcze (Ce):
- Ce zwiera Re dla AC
- Model wraca do poprzedniego
- Wzmocnienie = -h₂₁ · Rc / h₁₁

Jeśli Re nie ma zwarca:
- Re wpływa na impedancję wejściową
- Model bardziej złożony
```

## 🎬 Przykład Praktyczny

```
SCHEMAT:
          +12V
            │
           10k (Rc)
            │
        ┌───┤
    ┌───┤ B │
    │   │   │ Q (h₂₁=100, h₁₁=2kΩ)
   100k ├───┤ E
    │   │   │
  1V,1k ┴─ GND
   │
  GND

ANALIZA:

1) Impedancja wejściowa:
   Z_in = h₁₁ || Rb = (2000 || 100000) = 1960 Ω ≈ 2k

2) Impedancja wyjściowa:
   Z_out = Rc = 10k Ω

3) Wzmocnienie:
   ku = -100 · 10000 / 2000 = -500

WNIOSKI:
- Układ wzmacnia sygnał 500 razy (bardzo dużo!)
- Sygnał jest odwrócony (minus)
- Impedancja wejścia to 2kΩ
```

## 📋 Checklist: Analiza CE

Gdy widzisz schemat, zawsze rób:

- [ ] Identyfikujesz Rc (rezystor kolektora)
- [ ] Identyfikujesz Rb (rezystor polaryzacji)
- [ ] Znajdujesz h₂₁ i h₁₁
- [ ] Obliczasz Z_in = h₁₁ || Rb
- [ ] Obliczasz Z_out = Rc (lub Rc || Ry)
- [ ] Obliczasz ku = -h₂₁ · Rc_eff / h₁₁
- [ ] Sprawdzasz czy są kondensatory (Ce, Cs, Ca)

## 🚀 Następny krok

Teraz przeanalizujemy **konkretne przykłady** z różnymi konfiguracjami elementów.

→ Przejdź do **05_Przykład_1_Prosty_WE.md**
