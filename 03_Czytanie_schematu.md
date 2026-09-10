# 03 - Czytanie Schematu i Identyfikacja Elementów

## 🎯 Co będziesz umieć po tej części?

Będziesz potrafić przeanalizować schemat rysowany na tablicy i:
- Zidentyfikować konfigurację tranzystora (wspólny emiter, baza, kolektor)
- Zobaczyć gdzie są kondensatory sprzęgujące i oddzielające
- Określić rezystory polaryzacji i obciążenia
- Wynotować wszystkie dane: Ucc, Rc, Re, Rb, h-parametry, Ce, Ca, Cs

## 📍 Znakowanie w Schemacie

Zapamiętaj te symbole:

```
TRANZYSTOR BIPOLARNY NPN:        REZYSTOR:         KONDENSATOR:
                                 
    B ─────                      ──┬┬──            ──┬│├──
           │                          │                ││
    C ──────>                                       (może być równolegle)
           │
    E ─────

CEWKA:                          MASA:              ZASILANIE:
    ═══┬────                     ─┬─                  ┬
        │                        │                    ▲
```

## 🔍 Typowy schemat: Wspólny Emiter

```
                +Ucc (zasilanie)
                 │
                 │ Rc (rezystor kolektora/obciążenia)
                 │
          Ca ──┬┤│├─┬─ u_wy
              │ │   │
          Cs ─┼─┤ B │─(tranzystor Q)
          ┌───┘ │ C │
          │     │   │
        ┌─┴─┐   │   Ry (obciążenie wyjścia)
        │ Rb│   │   │
        └─┬─┘   │   │
          │     │   │
        Rb2     │ E │
          │   │─┘   │
          │   │      │
        ─┬─  Re   Ce─┼─
         │   │   │   │
        GND  ───┴───GND

LEGENDA:
  Ucc = zasilanie (np. 12V)
  Rc = rezystor kolektora
  Rb = rezystor polaryzacji bazy (może być R1+R2 dzielnik)
  Re = rezystor emitera
  Ce = kondensator obejścia emitera
  Ca = kondensator sprzęgujący wejście
  Cs = kondensator sprzęgujący wyjście
  Ry = rezystor obciążenia
```

## 📋 Procedura: Czytanie Schematu

### Etap 1: Zidentyfikuj tranzystor

```
Pytania do siebie:
✓ Gdzie jest tranzystor? (baza, kolektor, emiter)
✓ Jaki typ? (zwykle NPN na początku)
✓ Jakie h-parametry mi dano?
```

### Etap 2: Zidentyfikuj zasilanie i masę

```
Pytania:
✓ Gdzie jest +Ucc? (zwykle na górze)
✓ Gdzie jest GND? (masa, zwykle na dole)
✓ Jaka wartość Ucc?
```

### Etap 3: Zidentyfikuj rezystory

```
Dla każdego rezystora pytaj:
✓ Jaka jest jego nazwa? (Rc, Re, Rb, Ry)
✓ Jaka jest jego wartość?
✓ Między czym jest podłączony?
✓ Czy jest równolegle czy szeregowo z tranzystorem?
```

| Nazwa | Rola | Połączenie |
|-------|------|-----------|
| **Rc** | Obciążenie kolektora | Ucc ─ Rc ─ C(Q) |
| **Re** | Rezystor emitera (stabilizacja) | E(Q) ─ Re ─ GND |
| **Rb** | Polaryzacja bazy | Ucc ─ Rb ─ B(Q) ─ GND |
| **Ry** | Obciążenie wyjścia | u_wy ─ Ry ─ GND |

### Etap 4: Zidentyfikuj kondensatory

```
Dla każdego kondensatora pytaj:
✓ Jaka jest jego nazwa? (Ca, Ce, Cs)
✓ Jaka jest jego pojemność?
✓ Gdzie jest podłączony?
✓ Jaki ma wpływ dla AC?
```

| Nazwa | Rola | Połączenie | Wpływ AC |
|-------|------|-----------|----------|
| **Ca** | Sprzęg wejściowy | źródło ─ Ca ─ B(Q) | Zwiera - przepuści AC |
| **Ce** | Obejście emitera | E(Q) ─ Ce ─ GND | Zwiera Re dla AC |
| **Cs** | Sprzęg wyjściowy | C(Q) ─ Cs ─ u_wy | Zwiera - przepuści AC |

### Etap 5: Zidentyfikuj źródło i obciążenie

```
Pytania:
✓ Gdzie jest sygnał wejściowy? (zwykle przy Ca)
✓ Jaka jest impedancja źródła? (Rs)
✓ Gdzie jest wyjście? (zwykle przy Cs)
✓ Jakie jest obciążenie? (Ry)
```

## 🎓 Praktyka: Przeanalizuj Ten Schemat

```
          +12V
            │
           10k (Rc)
            │
        ┌───┤C
    ┌─┬─┤100nF (Ca)
    │ │B│
   1k │ │ Q2N2222
    │ │E│
    │ ││100Ω (Re)
    │ ├┴─┴───1µF (Ce)
    │ │     │
   Źródło  GND
   1V AC
   1k (Rs)
    │
   GND
```

### Twoja analiza:

1. **Tranzystor:** Q2N2222 (NPN), h₂₁ = 200, h₁₁ = 1kΩ
2. **Zasilanie:** Ucc = 12V
3. **Rezystory:**
   - Rc = 10 kΩ (kolektora)
   - Re = 100 Ω (emitera)
   - Rs = 1 kΩ (źródła)
4. **Kondensatory:**
   - Ca = 100 nF (sprzęg wejścia)
   - Ce = 1 µF (obejście emitera)
5. **Źródło:** 1V amplitudy, 1 kΩ
6. **Obciążenie:** Brak podane (nieskończoność)

## 🎯 Co Patrzysz w Każdym Schemacie?

### Zanim przystąpisz do analizy, zawsze:

```
CHECKLIST:

☑ Tranzystor: typ i h-parametry
☑ Zasilanie: wartość Ucc
☑ Rezystor kolektora: Rc = ?
☑ Rezystor emitera: Re = ?
☑ Rezystor polaryzacji: Rb = ?
☑ Kondensator wejścia: Ca = ?
☑ Kondensator wyjścia: Cs = ?
☑ Kondensator emitera: Ce = ?
☑ Rezystor źródła: Rs = ?
☑ Rezystor obciążenia: Ry = ?
```

## 💡 Część Nie Pokazana Zawsze

Czasami na schemacie rzeczywistym brakuje:
- **Ce** może nie być (wtedy Re nie jest obejęty dla AC)
- **Cs** może nie być (wtedy sygnał nie wychodzi na wyjście)
- **Ry** może nie być (wtedy przyjmujemy nieskończoną impedancję obciążenia)

**Ważne:** Zawsze pytaj prowadzącego co jest, jeśli nie widzisz!

## 🔬 Konwencje Napięć

Pamiętaj, że na schemacie:
- **Ucc** = +12V (lub inna wartość) - zasilanie
- **GND** = 0V - masa (punkt odniesienia)
- **u_BE** = napięcie między bazą a emiterem (~0.6V-0.7V dla bipolara w pracy)
- **u_CE** = napięcie między kolektorem a emiterem (zmienia się z punktem pracy)
- **u_wy** = napięcie wyjściowe AC (zmienne)

## 🚀 Następny Krok

Teraz znasz już strukturę schematów. Nauczmy się **analizować konkretną konfigurację: wspólny emiter**.

→ Przejdź do **04_Wspólny_Emiter.md**
