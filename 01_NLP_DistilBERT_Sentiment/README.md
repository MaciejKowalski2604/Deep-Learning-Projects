# Analiza Sentymentu (IMDB): LSTM vs Fine-tuning DistilBERT 🎬

Projekt z dziedziny Przetwarzania Języka Naturalnego (NLP) polegający na budowie i porównaniu modeli głębokich do binarnej klasyfikacji recenzji filmowych (zbior danych IMDB). 

## 🛠️ Architektura i Wykorzystane Techniki
- **Klasyfikator Baseline (LSTM):** Ręczna implementacja sieci rekurencyjnej z warstwą osadzeń (Embedding), komórką LSTM i w pełni połączoną głową klasyfikacyjną.
- **Transfer Learning (DistilBERT):** Wykorzystanie pretrenowanego modelu z biblioteki Hugging Face. Zaimplementowano dwa warianty optymalizacji:
  - Zamrożenie całego "kręgosłupa" (backbone) i trenowanie wyłącznie nowej głowy klasyfikacyjnej.
  - Odmrożenie ostatniej warstwy transformera w celu lepszej specjalizacji do zadania (Fine-tuning).
- **Proces uczenia:** Własna pętla treningowa w PyTorch, optymalizator AdamW, minimalizacja błędu entropii krzyżowej ($\mathcal{L} = -\sum_{i=1}^{C} y_i \log(\hat{y}_i)$).

## 📂 Struktura plików
- `imdb_sentiment_classifier.ipynb` - pełny kod eksperymentów: od preprocessingu i tokenizacji, przez budowę klas (dziedziczących po `nn.Module`), aż po walidację i wizualizację wyników.
- `requirements.txt` - zależności projektowe (PyTorch, Transformers, Datasets).

## 🚀 Kluczowe wnioski z eksperymentu
1. **Dokładność vs Czas:** Całkowicie zamrożony DistilBERT osiąga skuteczność porównywalną do prostej sieci LSTM, jednak LSTM trenuje się niemal 4-krotnie szybciej.
2. **Siła Fine-tuningu:** Odmrożenie zaledwie jednej (ostatniej) warstwy transformera zwiększa dokładność modelu o około 10 punktów procentowych przy zachowaniu akceptowalnego czasu treningu.
3. **Złoty środek:** Dla zadań wymagających maksymalizacji dokładności, krótki trening DistilBERTa z częściowo odmrożonymi warstwami jest optymalny. Dla projektów z rygorystycznymi limitami czasowymi, proste architektury rekurencyjne (LSTM) pozostają wysoce konkurencyjne.