# 02 - Budowanie Modelu Małosygnałowego

## 🎯 Cel tej części

Po przeczytaniu będziesz wiedzieć:
1. Jak **rozdzielić DC od AC** w schemacie
2. Jak **zastąpić tranzystor** jego modelem h-parametrów
3. Jak **upraszczać** schema przy analityce małosygnałowej

## 📐 Dwie domeny analizy

Każdy układ pracuje jednocześnie w dwóch domenach:

### 1️⃣ Dziedzina DC (statyka)

**Cel:** Znaleźć punkt pracy tranzystora (Q-point)
- Jakie są prądy i napięcia bez sygnału?
- Icc = ? Uce = ?

**Reguły:**
- Kondensatory są **otwarte** (rozerwane)
- Cewki są **zwarte** (przewodniki)
- Tranzystor to element nieliniowy, ale używamy jego linii roboczej

```
Schemat DC: Usuwamy wszystkie kondensatory!
```

### 2️⃣ Dziedzina AC (dynamika)

**Cel:** Jak układ reaguje na małe zmiany sygnału?
- Jaka jest impedancja wejściowa?
- Jakie jest wzmocnienie?

**Reguły:**
- Kondensatory są **zwarte** (przewodniki dla AC)
- Cewki są **otwarte** (przeszkody dla AC)
- Zasilanie jest **zwarte** (źródło napięcia ma Ro ≈ 0)
- Tranzystor zastępujemy **modelem linearnym** z h-parametrami

```
Schemat AC: Usuwamy kondensatory i cewki jako otwarte,
            zastępujemy zasilanie masą, zastępujemy tranzystor
```

## 🔄 Krok po kroku: Budowanie Modelu Małosygnałowego

### Krok 1: Analiza DC - punkt pracy

Rysujemy schemat **bez kondensatorów i cewek**:

```
Przykład: Prosty wzmacniacz wspólnego emitera

SCHEMAT RZECZYWISTY:
        +Ucc
         │
         Rc
         │
    ┌────┤ Transistor (Q)
    │B   │C
    │    │
   Rbe   Re (ze zwarciem AC)
    │    │
    ├────┴───
    │       ├─ Ue (wyjście AC)
    │       │
   Rs      Ce (zwarto dla AC)
    │      ├─
    Ue     │
    │      ├─ Masa
    
SCHEMAT DC (bez Ca, Ce, Cs):
        +Ucc
         │
         Rc
         │
    ┌────┤
    │    │C
    │    │
   Rbe  Re
    │    │
    ├────┴─── masa
    │
   Źródło Ue
```

Z tego wyznaczamy: **Ic, Ube, Uce** - punkt pracy tranzystora.

### Krok 2: Przygotowanie schematu AC

Transformujemy schemat rzeczywisty:

**Zasady zamiany:**

| Element | Co się dzieje dla AC? |
|---------|----------------------|
| Kondensator serii | Zwiera sygnał AC (staje się przewodnikiem) |
| Kondensator równolegle | Zwiera do masy sygnały AC |
| Cewka serii | Rozrywa sygnał AC (otwarta) |
| Cewka równolegle | Zwiera sygnał AC |
| Zasilanie (+Ucc) | Staje się masą (Vpn = 0 dla AC) |
| Rezystor | Pozostaje bez zmian (dla DC i AC) |
| Tranzystor | ZASTĘP MODELEM! |

### Krok 3: Rysowanie modelu małosygnałowego

**Zastępujemy tranzystor jego ekwiwalentem:**

```
Model tranzystora z h-parametrami (dla wspólnego emitera):

Wejście (baza-emiter):
     ┌─ R_BE = h₁₁ ─┐
     │              ├─── u_BE
     ├─ h₁₂·u_CE ───┘
     │
    i_B

Wyjście (kolektor-emiter):
                 ┌─── i_C = h₂₁·i_B + h₂₂·u_CE

u_CE ─────┬─────┤ 1/h₂₂ (bardzo wysoka)
          │
       h₂₁·i_B (źródło prądu)
```

## 🎭 Praktyczny Przykład: Wspólny Emiter

### Schemat rzeczywisty:

```
          +Ucc
           │
          Rc
           │
      ┌────┤C (kolektor)
  Cs  │ B │ 
  ─┬─ Rb  │ Q (tranzystor)
   │  │   │
   ├──┘   E (emiter)
   │      │
  sig    Re  Ce
   │      ├──┴──
   │      │    
  Źródło  Masa  Wyjście
```

### Schemat DC (wyznaczanie Q-point):

```
          +Ucc
           │
          Rc
           │
      ┌────┤
      │    │
      Rb   │
      │    │
      ├────┤
      │    │
      ├─── Re (bez Ce!)
      │    │
    Sig   Masa
```

### Schemat AC (model małosygnałowy):

```
           Rc (równolegle do sygnału AC)
            │
   sig──┬───┤  i_B ──→ [h₂₁·i_B] ──→
        │   │                  │
        │  (h₁₁)              [1/h₂₂]
        │   │                  │
        ├───┘            u_CE ─┴─ u_wy
        │
       Rs
        │
      Źródło AC

Wejście widziane przez źródło: Rs + (h₁₁ równolegle z Rb)
Wyjście: Rc równlegle z (1/h₂₂)
Wzmocnienie: -h₂₁ · Rc / h₁₁
```

## 📝 Checklist: Czy dobrze zbudowałem model?

- [ ] Usunąłem wszystkie kondensatory (stały się zwartami)
- [ ] Usunąłem wszystkie cewki (stały się otwartami)
- [ ] Zasilanie +Ucc połączyłem z masą (dla AC)
- [ ] Zastąpiłem tranzystor modelem z h-parametrami
- [ ] Pozostawiłem wszystkie rezystory
- [ ] Źródło sygnału wciąż jest w schemacie

## 🚀 Co daje nam taki model?

Teraz możemy:
1. **Obliczyć impedancję wejściową** (Z_in) - jak źródło "widzi" układ
2. **Obliczyć impedancję wyjściową** (Z_out) - co układ "prezentuje" obciążeniu
3. **Obliczyć wzmocnienie napięciowe** (ku) - ile razy amplitudzie wzrastają
4. **Analizować fraktycję** kondensatorów sprzęgujących

## 💡 Intuicja

Model małosygnałowy to **linearyzacja** tranzystora wokół punktu pracy. Pozwala nam:
- Zamiast rozwiązywać nieliniowe równania Ebersa-Molla
- Pracować z prostymi schematami liniowymi
- Używać narzędzi analizy obwodów (Kirchhoff, dzielniki, itp.)

## 🎬 Następny krok

Teraz nauczymy się **czytać schematy rzeczywiste** i identyfikować elementy.

→ Przejdź do **03_Czytanie_schematu.md**
