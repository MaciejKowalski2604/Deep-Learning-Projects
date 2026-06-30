# Odtwarzanie Obrazów (Image Inpainting): U-Net vs cGAN (Pix2Pix) 🎨

Projekt z dziedziny Computer Vision (Deep Learning) mający na celu rekonstrukcję usuniętych (zakrytych maską) fragmentów obrazów. Rozwiązanie opiera się na zbiorze danych STL-10 i porównuje klasyczne podejście z architekturami generatywnymi.

## 🛠️ Wykorzystane Architektury
- **Klasyczny U-Net:** Model z enkoderem i dekoderem, uczony z wykorzystaniem błędu średniokwadratowego (MSE Loss).
- **Generacyjna Sieć Przeciwstawna (cGAN):** Architektura inspirowana modelem Pix2Pix. Składa się z:
  - **Generatora (U-Net):** Odpowiedzialnego za generowanie realistycznych łat na uszkodzonym obrazie.
  - **Dyskryminatora (PatchGAN):** Oceniającego, czy przedstawiony obraz jest autentyczny, czy wygenerowany sztucznie. Wykorzystano `BCEWithLogitsLoss` oraz `L1Loss` do stabilizacji treningu.

## 📊 Ewaluacja i Metryki
Do obiektywnej oceny jakości rekonstrukcji wykorzystano miary z biblioteki `torchmetrics`:
- **PSNR** (Peak Signal-to-Noise Ratio)
- **SSIM** (Structural Similarity Index Measure)

## 📂 Struktura plików
- `image_inpainting_pix2pix.ipynb` - kompletny notatnik zawierający preprocessing danych (aplikowanie losowych masek na obrazy), definicje architektur, pętle uczące oraz wizualizację wyników.
- `requirements.txt` - lista wymaganych bibliotek.

## 🚀 Kluczowe wnioski
1. **Różnice w wynikach:** Klasyczny U-Net dąży do minimalizacji błędu matematycznego (MSE), co skutkuje wyższymi wartościami PSNR/SSIM, ale generuje nienaturalne, "rozmyte" łaty.
2. **Przewaga GAN:** Wprowadzenie dyskryminatora wymusza na generatorze tworzenie ostrych, fotorealistycznych tekstur. Mimo że w suchych metrykach matematycznych cGAN może wypadać nieco słabiej, wizualnie generuje znacznie lepsze i bardziej spójne z kontekstem rezultaty.