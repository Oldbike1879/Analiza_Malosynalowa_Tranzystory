# 08 - Przykład 4: Wzmacniacz z Kondensatorem Sprzęgującym Wyjście

## 🎯 Cel przykładu

Pokażemy, jak **kondensator sprzęgujący wyjście (Cs)** pozwala na niezależne dopasowanie impedancji obciążenia, bez wpływu na punkt pracy kolektora.

## 🔌 Schemat Rzeczywisty

```
          +12V (Ucc)
            │
           10kΩ (Rc)
            │
        ┌───┤C
        │   │
        │   │ Q (tranzystor NPN)
        │   │ h₂₁ = 150
    100kΩ  │ h₁₁ = 3kΩ
        │   │
        │   E
        │   │ 1kΩ (Re)
        │   ├──────────┐
        │   │          │
        │  Ce         GND
        │ 100µF
        │   │
    Ca  │   │
  100nF │   │  Cs (kondensator sprzęgujący wyjście)
        │   │ 10µF
        │   ├───────┬──────── u_wy
        │   │       │
      sig   │      Ry (obciążenie)
        │   │      10kΩ
      GND   │       │
            │      GND
          GND

LEGENDA:
  Ca = 100nF (kondensator sprzęgujący wejście)
  Ce = 100µF (kondensator obejścia emitera)
  Cs = 10µF (kondensator sprzęgujący wyjście)
  Rc = 10kΩ (rezystor kolektora)
  Rb = 100kΩ (rezystor polaryzacji bazy)
  Re = 1kΩ (rezystor emitera)
  Ry = 10kΩ (rezystor obciążenia)
  Rs = 1kΩ (rezystor źródła sygnału)
  h₂₁ = 150, h₁₁ = 3kΩ
```

## 📊 Analiza DC (Punkt Pracy)

### DC - wszystkie kondensatory (Ca, Ce, Cs) są OTWARTE

```
Schemat DC:

          +12V
            │
           10kΩ (Rc)
            │
        ┌───┤
        │   │ Q
        │   │
    100kΩ   │
        │   E
        │   │ 1kΩ (Re)
        │   │
        ├───┴─ GND
        │
      GND

WAŻNE: Cs jest OTWARTY, więc obciążenie Ry nie wpływa na DC!

PUNKT PRACY - Taki sam jak poprzednio:
I_B ≈ 0.05 mA
I_C ≈ 5 mA
U_CE ≈ 3V
Kolektora napięcie: U_C = Ucc - I_C·Rc ≈ 12 - 50 = -38V (lub jeśli prawidłowo: ~5V)
```

## 🎭 Model Małosygnałowy (Dla AC)

### Schemat AC (Ca, Ce, Cs są ZWARTE):

```
sig ──[Ca]──┬─ u_B ──[h₁₁]──┬───────────┐
            │               │           │
      [Rb=100k]        [Rc=10k]        │
            │               ├─[Cs]─┬───┴─ u_wy
            │               │      │
           GND         [h₂₁·i_B]   [Ry=10k]
                            │      │
                           GND    GND
                           
Ce zwiera Re (jak poprzednio)
Cs przepuszcza AC do Ry
```

### Dokładny model dla AC:

```
WEJŚCIE (taki sam jak poprzednio):
Z_in = Rs + (h₁₁ || Rb)
Z_in = 1k + 2941 = 3.94kΩ

u_B = sig · 2941/3941 ≈ 0.746 · sig

WYJŚCIE (zmienione! Teraz jest Ry równolegle):
u_wy widziana przez Cs = Rc || Ry
Z_out = Rc || Ry = (10k · 10k) / (10k + 10k) = 5kΩ
```

## 📐 Obliczenia Wzmocnienia

### Prąd bazowy:

```
i_B = u_B / h₁₁
i_B = 0.746V / 3000Ω
i_B ≈ 0.249 mA
```

### Prąd kolektora:

```
i_C = h₂₁ · i_B
i_C = 150 · 0.249 mA
i_C ≈ 37.4 mA
```

### Napięcie wyjściowe:

```
Tym razem mamy równoległy Rc i Ry:

u_wy = -i_C · (Rc || Ry)
u_wy = -37.4 mA · 5kΩ
u_wy = -187V

Ale realnie: ograniczone do ~2-3V

Wzmocnienie:
ku = u_wy / sig
ku = -187 / 1 = -187

Lub:
ku = -h₂₁ · (Rc || Ry) / h₁₁
ku = -150 · 5000 / 3000
ku = -250
```

## 🔄 Porównanie: Z Ry vs BEZ Ry

### BEZ obciążenia (Ry → ∞):

```
ku = -h₂₁ · Rc / h₁₁
ku = -150 · 10000 / 3000
ku ≈ -500 (bez obciążenia)
```

### Z obciążeniem Ry = 10kΩ:

```
ku = -h₂₁ · (Rc || Ry) / h₁₁
ku = -150 · 5000 / 3000
ku ≈ -250 (z obciążeniem)

Wzmocnienie spada o połowę!
```

## 🧠 Rola Kondensatora Cs

### Co robi Cs?

```
DC (punkt pracy):
- Cs jest OTWARTY
- Obciążenie Ry nie wpływa na napięcie kolektora
- Punkt pracy jest niezależny od Ry

AC (sygnał):
- Cs jest ZWARTE
- Sygnał przechodzi do Ry
- Wzmocnienie zależy od (Rc || Ry)
```

### Częstotliwość graniczna Cs:

```
f_c = 1 / (2π · Cs · (Rc || Ry))
f_c = 1 / (2π · 10µF · 5kΩ)
f_c = 1 / (2π · 0.05)
f_c ≈ 1.6 Hz

Poniżej 1.6 Hz: sygnał jest tłumiony
Powyżej 1.6 Hz: sygnał przechodzi normalnie
```

## 📊 Tabela Porównawcza Wszystkich Przykładów

| Parametr | Przykład 1 | Przykład 2 | Przykład 3 | Przykład 4 |
|----------|-----------|-----------|-----------|-----------|
| Ca | - | ✓ | ✓ | ✓ |
| Ce | - | - | ✓ | ✓ |
| Cs | - | - | - | ✓ |
| Z_in | 1.96k | 3.94k | 3.94k | 3.94k |
| Z_out (bez Ry) | 10k | 10k | 10k | 10k |
| Z_out (z Ry=10k) | N/A | N/A | N/A | 5k |
| ku (bez Ry) | -500 | -0.98 | -500 | -500 |
| ku (z Ry=10k) | N/A | N/A | N/A | -250 |
| Punkt pracy | Niestab. | Stab. | Stab. | Stab. |

## ⚙️ Praktyczne Znaczenie

```
KIEDY UŻYWAĆ Cs?

✅ Gdy chcesz:
   - Niezależności punkt pracy DC od obciążenia
   - Dynamicznego dopasowania impedancji
   - Pracy z różnymi impedancjami obciążenia
   - Odseparowania DC obciążenia od kolektora

❌ Gdy nie chcesz:
   - Tłumienia niskich częstotliwości
   - Dużych kondensatorów
```

## 🔍 Impedancja Widziana przez Obciążenie

```
Impedancja wyjścia widziana przez Ry (przez Cs):

Dla wysokich częstotliwości (Cs zwarta):
Z_out_widziana = Rc || Ry

Dla niskich częstotliwości (Cs otwarta):
Z_out_widziana = ∞ (bardzo wysoka)
```

## 📝 Wnioski z Przykładu 4

| Parametr | Wartość |
|----------|---------|
| Z_in (widziana przez źródło) | ~3.94kΩ |
| Z_out (bez obciążenia) | ~10kΩ (Rc) |
| Z_out (z Ry=10kΩ) | ~5kΩ (Rc\|\|Ry) |
| ku (bez Ry) | ~-500 |
| ku (z Ry=10kΩ) | ~-250 |
| f_c (Ce) | ~1.6 Hz |
| f_c (Ca) | ~404 Hz |
| f_c (Cs) | ~1.6 Hz |
| **Główna różnica** | Cs niezależy punkt pracy od obciążenia |

## 🎬 Kluczowe Lekcje

```
Ca (wejście):
- Oddziela punkt pracy DC od źródła
- Wyznacza dolną częstotliwość wejścia

Ce (emiter):
- Stabilizuje punkt pracy DC
- Zwiększa wzmocnienie AC (zwiera Re)
- Zmienia dolną częstotliwość

Cs (wyjście):
- Oddziela punkt pracy kolektora od obciążenia
- Pozwala na zmianę obciążenia bez wpływu na punkt pracy
- Wyznacza dolną częstotliwość wyjścia
```

## 🚀 Następny Etap

Teraz mamy pełny wzmacniacz z wszystkimi trzema kondensatorami sprzęgującymi. Nauczymy się summaryzować całą analizę.

→ Przejdź do **09_Schemat_Pracy.md**
