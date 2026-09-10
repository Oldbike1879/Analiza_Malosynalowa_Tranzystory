# 07 - Przykład 3: Wzmacniacz z Kondensatorem Obejścia Emitera

## 🎯 Cel przykładu

Pokażemy, jak **kondensator obejścia emitera (Ce)** znacznie **zwiększa wzmocnienie napięciowe**, ponieważ dla AC "wyłącza" rezystor Re.

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
  100nF │   │
        │   │
      sig (1V AC, 1kΩ)
        │
      GND

LEGENDA:
  Ca = 100nF (kondensator sprzęgujący wejście)
  Ce = 100µF (kondensator obejścia emitera)
  Rc = 10kΩ (rezystor kolektora)
  Rb = 100kΩ (rezystor polaryzacji bazy)
  Re = 1kΩ (rezystor emitera)
  Rs = 1kΩ (rezystor źródła sygnału)
  h₂₁ = 150, h₁₁ = 3kΩ
```

## 📊 Analiza DC (Punkt Pracy)

### DC - kondensatory CA i CE są OTWARTE

```
Schemat DC (brak Ca i Ce):

          +12V
            │
           10kΩ (Rc)
            │
        ┌───┤
        │   │ Q
        │   │
    100kΩ   │
        │   E
        │   │ 1kΩ (Re) - zwykły rezystor, Ce nie wpływa
        │   │
        ├───┴─ GND
        │
      GND

PUNKT PRACY - Taki sam jak w Przykładzie 2:
I_B ≈ 0.05 mA
I_C ≈ 5 mA
U_CE ≈ 3V
```

## 🎭 Model Małosygnałowy (Dla AC)

### KLUCZOWA RÓŻNICA: Ce ZWIERA Re dla AC!

```
Schemat AC (Ca i Ce są ZWARTE):

sig ──[Ca=100nF]──┬─ u_B ──[h₁₁]──┬────────┐
                  │               │        │
            [Rb=100kΩ]       [Rc=10kΩ]    │
                  │               ├────┬──┴─ u_wy
                  │               │    │
                 GND         [h₂₁·i_B]
                                  │
                                 GND
                                 
Re zwiera się do GND przez Ce (dla AC),
więc nie ma już sprzętu napięciowego na Re!
```

### Dokładny model z Ce:

```
WEJŚCIE (bez Re dla AC!):
sig ──[Ca]──┬─ u_B
            │
    [Rb || h₁₁]  (Ce nie wpływa na bazy)
            │
           GND

Z_in = Rs + (h₁₁ || Rb)
Z_in = 1k + (3k || 100k)
Z_in = 1k + 2941 = 3.94kΩ

u_B = sig · 2941/3941 ≈ 0.746 · sig
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

### Napięcie wyjściowe (TERAZ INNE!):

```
WAŻNE: Re jest dla AC zwarte, więc nie ma spadku napięcia na Re!

u_wy = -i_C · Rc
u_wy = -37.4 mA · 10kΩ
u_wy = -374V

Ale realnie: ograniczone do ~3-5V (amplituda)

Wzmocnienie:
ku = u_wy / sig
ku = -374 / 1 = -374

Lub prościej:
ku = -h₂₁ · Rc / h₁₁
ku = -150 · 10000 / 3000
ku = -500
```

## 🔄 Porównanie: Z Ce vs BEZ Ce

### BEZ kondensatora Ce (Przykład 2):

```
Dla AC: Re NIE jest zwarte
Model wzmacniającego rezystora emitera:

Z_emitera = Re = 1kΩ

Wzmocnienie jest ZREDUKOWANE przez Re:
ku ≈ -h₂₁ · Rc / (h₁₁ + h₂₁ · Re)
ku ≈ -150 · 10000 / (3000 + 150 · 1000)
ku ≈ -150000 / 153000
ku ≈ -0.98 (bardzo małe wzmocnienie!)
```

### Z KONDENSATOREM Ce (Przykład 3):

```
Dla AC: Re jest zwarte (Ce pracuje jak zwarcie)
Model bez rezystora emitera:

Z_emitera ≈ 0 (dla AC)

Wzmocnienie WZRASTA:
ku = -h₂₁ · Rc / h₁₁
ku = -150 · 10000 / 3000
ku ≈ -500 (OGROMNE wzmocnienie!)
```

## 🧠 Fizyczne Wyjaśnienie

```
Co robi Ce?

DC (punkt pracy):
- Re stabilizuje punkt pracy
- Zapewnia ujemne sprzężenie zwrotne
- Tłumi różnice temperaturowe

AC (sygnał):
- Ce zwiera Re na częstotliwościach powyżej f_c
- Usuwa sprzężenie zwrotne dla AC
- ZWIĘKSZA wzmocnienie AC do maksimum
- f_c = 1 / (2π · Ce · Re)
  f_c = 1 / (2π · 100µF · 1kΩ)
  f_c = 1 / (2π · 0.1)
  f_c ≈ 1.6 Hz
```

## 📊 Tabela Porównawcza

| Cecha | Przykład 2 (bez Ce) | Przykład 3 (z Ce) |
|-------|-------------------|------------------|
| Re dla DC | 1kΩ (aktywny) | 1kΩ (aktywny) |
| Re dla AC | 1kΩ (aktywny) | 0Ω (zwarte) |
| Stabilność punkt. pracy | Dobra | Dobra |
| Wzmocnienie AC | ~-1 (mały) | ~-500 (duży) |
| Górna f granicz. | Wyższa | Niższa |
| Praktyczne zastosowanie | Gdy chcemy stabilność | Gdy chcemy dużo wzmocnienia |

## 🚀 Czem powinno być Ce?

### Częstotliwość graniczna (gdzie Ce zaczyna pracować):

```
f_c = 1 / (2π · Ce · Re)

Gdy f_c = 10 Hz (chcemy AC od 10 Hz):
Ce = 1 / (2π · 10 · 1000)
Ce ≈ 16 µF

W schemacie użyto Ce = 100µF, czyli f_c ≈ 1.6 Hz
To znaczy, że Ce pracuje od ~1.6 Hz i wyżej.
```

## ⚙️ Praktyczne Znaczenie

```
KIEDY UŻYWAĆ Ce?

✅ Gdy chcesz:
   - Maksymalnego wzmocnienia napięciowego
   - Pracy z niskimi częstotliwościami (audio, DC+AC)
   - Obejścia rezystora emitera dla AC

❌ Gdy nie chcesz:
   - Dużych kondensatorów (Ce musi być duży)
   - Tłumienia niskich częstotliwości
   - Skomplikowania schematu
```

## 📝 Wnioski z Przykładu 3

| Parametr | Wartość |
|----------|---------|
| Z_in (widziana przez źródło) | ~3.94kΩ |
| Z_out (wyjście) | ~10kΩ (Rc) |
| ku (z Ce) | ~-500 |
| f_c (Ce) | ~1.6 Hz |
| f_c (Ca) | ~404 Hz |
| **Główna różnica** | Ce obejmuje Re dla AC |

## 🎬 Klucz do Zrozumienia

```
Ce jest jak "inteligentny przełącznik":
- Na DC: Re jest aktywny (DC nie przechodzi przez Ce)
- Na AC: Re jest zwarte (AC przechodzi przez Ce)

To pozwala mieć:
- Dobrą stabilność DC (dzięki Re)
- Duże wzmocnienie AC (dzięki Ce)

Najlepsze z obu światów!
```

## 🚀 Następny Etap

Teraz dodamy **kondensator sprzęgujący wyjście (Cs)** - który ogranicza dolną częstotliwość!

→ Przejdź do **08_Przykład_4_Rezystor_Emitera.md**
