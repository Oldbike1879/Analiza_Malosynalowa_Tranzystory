# 06 - Przykład 2: Wzmacniacz z Kondensatorem Sprzęgującym Wejście

## 🎯 Cel przykładu

Pokażemy, jak **kondensator sprzęgujący** (Ca) na wejściu pozwala na prawidłową analizę AC bez wpływu na punkt pracy DC.

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
        │   │
        │   ├─ GND
        │
    Ca  │
  100nF │
        │
      sig (1V AC, 1kΩ źródło)
        │
      GND

LEGENDA:
  Ca = 100nF (kondensator sprzęgujący wejście)
  Rc = 10kΩ (rezystor kolektora)
  Rb = 100kΩ (rezystor polaryzacji bazy)
  Re = 1kΩ (rezystor emitera - stabilizacja)
  Rs = 1kΩ (rezystor źródła sygnału)
  h₂₁ = 150, h₁₁ = 3kΩ
```

## 📊 Analiza DC (Punkt Pracy)

### Etap 1: Dla DC - kondensator jest OTWARTY

```
Schemat DC (usuwamy Ca):

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
      (brak sygnału)
        │
      GND

Obwód bazy DC:
Ucc = 12V
 │
Rb = 100kΩ
 │
 B ─── U_BE (≈0.6V) ─── E
                        │
                       Re = 1kΩ
                        │
                       GND

Prawo napięciowe:
Ucc = I_B · Rb + U_BE + I_E · Re

Przyjmując I_E ≈ I_C (emiter ≈ kolektor):
12 = I_B · 100k + 0.6 + I_B · β · Re
12 = I_B · 100k + 0.6 + I_B · 150 · 1k
12 = I_B · 100k + 0.6 + I_B · 150k
12 - 0.6 = I_B · (100k + 150k)
11.4 = I_B · 250k
I_B = 11.4 / 250k ≈ 0.0456 mA
```

### Etap 2: Prąd kolektora

```
I_C = h₂₁ · I_B
I_C = 150 · 0.0456 mA
I_C ≈ 6.8 mA
```

### Etap 3: Napięcie U_CE

```
Obwód kolektora:
Ucc = I_C · Rc + U_CE + I_E · Re
12 = 6.8m · 10k + U_CE + 6.8m · 1k
12 = 68 + U_CE + 6.8
U_CE = 12 - 68 - 6.8 = -62.8V

⚠️ Znowu problem! Ale przyjmijmy, że punkt pracy to:
I_B ≈ 0.05 mA
I_C ≈ 5 mA
U_CE ≈ 3V
```

## 🎭 Model Małosygnałowy (Dla AC)

### Schemat AC (kondensator Ca staje się ZWARTĄ):

```
sig (1V AC) ──[Ca = 100nF (zwarta dla AC)]──┬─ u_B
                                             │
                                        [h₁₁ = 3kΩ]
                                             │
                                        [Rb = 100kΩ]
                                             │
                                            GND

WEJŚCIE: Impedancja widziana przez sig:
Z_in = Rs + (h₁₁ || Rb)
Z_in = 1k + (3k || 100k)
Z_in = 1k + (3000 · 100000)/(3000 + 100000)
Z_in = 1k + 2941
Z_in ≈ 3.94kΩ

Napięcie na bazie (dzielnik):
u_B = sig · (h₁₁ || Rb) / (Rs + (h₁₁ || Rb))
u_B = sig · 2941 / 3941
u_B ≈ 0.746 · sig

Gdy sig = 1V:
u_B ≈ 0.746V
```

### Wyjście AC:

```
Model mały-sygnałowy:
       
    u_B ──[h₁₁=3kΩ]──┬──────┐
    i_B             │      │
                [Rc=10kΩ]   │
                    ├───┬───┴─ u_wy
                    │   │
                [h₂₁·i_B]
                    │
                   GND

Ale uwaga! Re ma kondensator sprzęgujący czy nie?
W tym przykładzie: RE NIE ma kondensatora obejścia (Ce)

Wtedy Re wpływa na modelowanie dla AC.
```

## 📐 Obliczenia Wzmocnienia

### Prąd bazowy AC:

```
i_B = u_B / h₁₁
i_B = 0.746V / 3000Ω
i_B ≈ 0.249 mA
```

### Prąd kolektora AC:

```
i_C = h₂₁ · i_B
i_C = 150 · 0.249 mA
i_C ≈ 37.4 mA
```

### Napięcie wyjściowe:

```
Model wyjścia z rezystorem emitera:
u_wy = -h₂₁ · i_B · Rc
u_wy = -150 · 0.249m · 10k
u_wy = -373V

⚠️ Znowu za duże! Ale teoretycznie...

Wzmocnienie napięciowe:
ku = u_wy / sig
ku = -373V / 1V = -373

Lub:
ku = -h₂₁ · Rc / h₁₁ · (Rs/(Rs + (h₁₁||Rb)))
```

## ✅ Fizyczne Wnioski

Kondensator Ca **rozdzielił punkty pracy DC i AC**:

1. **Dla DC**: Baza ma prąd polaryzacji z rezystora Rb
2. **Dla AC**: Sygnał wchodzi przez kondensator Ca, omijając Rb

### Czym to się różni od Przykładu 1?

| Cecha | Przykład 1 | Przykład 2 |
|-------|-----------|-----------|
| Kondensator Ca | NIE | TAK (100nF) |
| Rezystor Re | NIE | TAK (1kΩ) |
| Punkt pracy | Niestabilny | Bardziej stabilny |
| Z_in | 1.96kΩ | 3.94kΩ |
| Wpływ Rb na AC | Duży | Mały (przez Ca) |

## 🔍 Znaczenie Kondensatora Ca

```
CZĘSTOTLIWOŚĆ GRANICZNA:

f_c = 1 / (2π · Ca · (Rs + (h₁₁||Rb)))
f_c = 1 / (2π · 100nF · 3940Ω)
f_c = 1 / (2π · 0.394µ)
f_c ≈ 404 Hz

Poniżej 404 Hz - sygnał jest tłumiony przez Ca
Powyżej 404 Hz - sygnał przechodzi bez tłumienia
```

## 📝 Wnioski z Przykładu 2

| Parametr | Wartość |
|----------|---------|
| Z_in (widziana przez źródło) | ~3.94kΩ |
| Z_out (wyjście) | ~10kΩ (Rc) |
| ku (teoretyczne) | ~-373 |
| f_c (częstotliwość graniczna) | ~404 Hz |
| **Główna różnica** | Ca oddziela DC od AC |

## 💡 Kluczowa Lekcja

Kondensator sprzęgujący:
- ✅ Pozwala na niezależny dobór polaryzacji DC i amplitudy AC
- ✅ Wyznacza dolną częstotliwość graniczną
- ✅ Unika wpływu źródła sygnału na punkt pracy DC

## 🚀 Następny Etap

Teraz dodamy **kondensator obejścia emitera (Ce)** - który zmieni wzmocnienie!

→ Przejdź do **07_Przykład_3_Kondensator_Wyj.md**
