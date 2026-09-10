# Analiza Małosygnałowa Tranzystorów Bipolarnych

Komprehensywny materiał edukacyjny do nauki analizy małosygnałowej z **Elektroniki i Miernictwa** na pierwszym roku.

## 📚 Struktura materiałów

```
📁 Analiza_Malosynalowa_Tranzystory/
├── 01_Podstawy_teoretyczne.md          # Teoria h-parametrów i modelowania
├── 02_Model_malosynalowy.md            # Jak budować model małosygnałowy
├── 03_Czytanie_schematu.md             # Praktyczny przewodnik do odczytywania
├── 04_Wspólny_Emiter.md                # Najważniejsza konfiguracja
├── 05_Przykład_1_Prosty_WE.md          # Przykład - wzmacniacz wspólnego emitera
├── 06_Przykład_2_Kondensator_Wej.md    # Przykład - ze sprzęgiem wejściowym
├── 07_Przykład_3_Kondensator_Wyj.md    # Przykład - ze sprzęgiem wyjściowym
├── 08_Przykład_4_Rezystor_Emitera.md   # Przykład - rezystor degradacji emitera
├── 09_Schemat_Pracy.md                 # Schemat logiczny wszystkich kroków
└── 10_Szablon_Analizy.md               # Szablon do samodzielnej analizy
```

## 🎯 Cel materiałów

Nauczysz się:
- ✅ Identyfikować tranzystor w schemacie i określać jego punkt pracy
- ✅ Budować model małosygnałowy na podstawie h-parametrów
- ✅ Obliczać impedancję wejściową (uWE)
- ✅ Obliczać impedancję wyjściową (uWY)
- ✅ Wyznaczać wzmocnienie napięciowe (ku)
- ✅ Analizować wpływ kondensatorów na charakterystykę

## 🔧 Parametry, które będziesz używać

| Parametr | Znaczenie | Wartość typowa |
|----------|-----------|----------------|
| **h₁₁** | Impedancja wejściowa | kilka kΩ |
| **h₂₁** | Wzmocnienie prądowe | 50-300 |
| **h₁₂** | Ujemne sprzężenie zwrotne (małe) | ≈ 0 |
| **h₂₂** | Admitancja wyjściowa | ≈ 0 (wysokie Ro) |

## 📝 Jak pracować z tym materiałem

1. **Zacznij od** `01_Podstawy_teoretyczne.md` - zrozumiesz modelowanie
2. **Przejdź do** `02_Model_malosynalowy.md` - nauczysz się budować modele
3. **Praktyka z** `04_Wspólny_Emiter.md` - zrozumiesz konfigurację
4. **Przeanalizuj** przykłady 1-4 - każdy dodaje nową złożoność
5. **Używaj** szablonu do samodzielnej analizy nowych układów

## 💡 Kluczowa metodyka

Każdy przykład pokazuje:
1. **Schemat schematyczny** (ASCII art)
2. **Model DC** (punkt pracy)
3. **Model małosygnałowy** (zamiennik h-parametrami)
4. **Analiza impedancji** (uWE, uWY)
5. **Obliczenie wzmocnienia** (ku)
6. **Wnioski praktyczne**

---

**Autor:** Materiały edukacyjne  
**Poziom:** I rok Elektroniki i Miernictwa  
**Język:** Polski
