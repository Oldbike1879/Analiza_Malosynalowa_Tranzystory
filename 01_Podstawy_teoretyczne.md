# 01 - Podstawy Teoretyczne H-Parametrów

## 🎓 Czym są h-parametry?

H-parametry to sposób opisania tranzystora jako czarnej skrzynki (quadripolu), która ma:
- **2 wejścia** (baza, emiter)
- **2 wyjścia** (kolektor, emiter)

Zamiast pamiętać dokładne równania fizyczne półprzewodnika, używamy **parametrów hybrydowych (h)**, które opisują relacje między napięciami i prądami.

## 📋 Cztery h-parametry

Tranzystor można opisać układem równań:

```
u_BE = h₁₁ · i_B + h₁₂ · u_CE
i_C = h₂₁ · i_B + h₂₂ · u_CE
```

### Gdzie:

| Symbol | Nazwa | Jednostka | Znaczenie fizyczne |
|--------|-------|-----------|-------------------|
| **h₁₁** | Impedancja wejściowa | [Ω] | Opór między bazą a emiterem |
| **h₂₁** | Wzmocnienie prądowe | [-] | Ile razy większy prąd kolektora niż bazowy |
| **h₁₂** | Sprzężenie zwrotne | [-] | Wpływ napięcia wyjściowego na wejście |
| **h₂₂** | Admitancja wyjściowa | [S] | Przewodność między kolektorem a emiterem |

## 🎯 Uproszczenia dla początkujących

Na pierwszym roku zwykle przyjmujemy:
- **h₁₂ ≈ 0** - nie ma perjęcia zwrotnego
- **h₂₂ ≈ 0** - wyjście ma bardzo wysoką impedancję (Ro → ∞)

**JEDNAK!** W rzeczywistych układach h₁₂ i h₂₂ nie są dokładnie zerem, bo:
- Jeśli by były dokładnie 0, czarne skrzynki byłyby niezależy
- W analizie małosygnałowej te parametry mają sens fizyczny

## 🔌 Model Małosygnałowy Tranzystora

Gdy pracujemy z małymi zmianami sygnału (amplituda << napięcie polaryzacji), tranzystor można modelować jako **liniowy dwójnik**.

### Równania małosygnałowe:

```
ũ_BE = h₁₁ · ĩ_B + h₁₂ · ũ_CE
ĩ_C = h₂₁ · ĩ_B + h₂₂ · ũ_CE
```

Gdzie **ũ** i **ĩ** to małe zmiany (sygnały AC).

### Ekwiwalentny obwód:

```
        ┌─ h₁₁ ─┬─────────┐
        │        │         │
    i_B ├───┐    │         ├─── u_BE
        │   │    └────┬────┘
        │   └──h₁₂·u_CE
        │              │
        │          u_CE
        │              │
    i_C ├────h₂₁·i_B──┬───── h₂₂
        │              │
        └──────────────┴─────
```

## 📊 Typowe wartości dla małosygnałowego tranzystora bipolarnego

```
h₁₁ (r_BE) = 100 Ω do 10 kΩ
           (zależy od punktu pracy)

h₂₁ (β)    = 50 do 300
           (często podawane dla danego IC)

h₁₂        = 10⁻⁴ do 10⁻³
           (bardzo małe, blisko zera)

h₂₂        = 10⁻⁵ do 10⁻⁴ S
           (bardzo małe, rzadko uwzględniane)
```

## 🔬 Skąd się biorą h-parametry?

Producent tranzystora podaje je w datasheecie jako funkcję punktu pracy:
- Są zmierzone dla konkretnych Ic, Uce, T
- Dla różnych temperatur i warunków mogą się zmieniać

**Na datasheecie będziesz szukać:**
- `hfe` = h₂₁ (wzmocnienie prądowe)
- `hie` = h₁₁ (impedancja wejściowa)
- `hre` = h₁₂ (sprzężenie zwrotne)
- `hoe` = h₂₂ (admitancja wyjściowa)

## 💡 Intuicja fizyczna

- **h₁₁**: Jak trudno jest "wcisnąć" prąd do bazy? (Wysoka = trudno)
- **h₂₁**: Ile razy wzmacniany jest prąd bazowy? (Niska wartość = słaba wzmocnienie)
- **h₁₂**: Czy zmiana napięcia wyjściowego wpływa na wejście? (Zwykle tak mało, że ignorujemy)
- **h₂₂**: Ile prądu wycieknie między kolektorem a emiterem gdy jest napięcie? (Zwykle pomijalnie mało)

## 🎬 Następny krok

Teraz kiedy znasz h-parametry, nauczymy się budować **model małosygnałowy** na podstawie schematu rzeczywistego.

→ Przejdź do **02_Model_malosynalowy.md**
