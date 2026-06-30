# Lądowanie na Księżycu (Reinforcement Learning): DQN vs PPO vs A2C 🚀

Projekt badawczy z dziedziny Uczenia ze Wzmocnieniem (Reinforcement Learning) wykorzystujący środowisko `LunarLander-v3` z biblioteki `Gymnasium`. Celem projektu jest wytrenowanie agenta AI do autonomicznego i bezpiecznego lądowania rakietą na księżycu, poprzez maksymalizację nagród.

## 🛠️ Architektury i Metody
Projekt opiera się na implementacjach z biblioteki `stable-baselines3` i porównuje trzy popularne algorytmy:
- **DQN (Deep Q-Network):** Uczenie oparte na wartości (Value-based), wykorzystujące sieć neuronową do estymacji Q-wartości nagród dla poszczególnych akcji.
- **PPO (Proximal Policy Optimization):** Algorytm z rodziny Policy Gradient, działający bezpośrednio na politykę agenta, charakteryzujący się bardzo wysoką stabilnością procesu uczenia.
- **A2C (Advantage Actor-Critic):** Podejście synchroniczne wykorzystujące dwie sieci (Aktora i Krytyka) do jednoczesnego aktualizowania polityki i oceny stanów.

## 📈 Optymalizacja i Ewaluacja (Fine-Tuning)
W ramach eksperymentów dla modelu DQN przeprowadzono rozbudowany Grid Search mający na celu znalezienie optymalnych hiperparametrów:
- `Learning Rate` oraz `Batch Size`
- Współczynnik dyskontowania `Gamma` oraz `Tau`
- Parametry eksploracji: `exploration_fraction` i `exploration_final_eps`

Wykorzystano `EvalCallback` oraz `Monitor` do bieżącego logowania wyników, śledzenia krzywych uczenia oraz analizy zależności między długością epizodów a zdobywaną nagrodą punktową.

## 📂 Pliki w projekcie
- `rl_lunar_lander_dqn_ppo_a2c.ipynb` - główny notatnik z kodem trenowania, strojenia hiperparametrów oraz generowania wizualizacji (wykresy i nagrania wideo).
- `requirements.txt` - lista wymaganych paczek.

## 🚀 Kluczowe wnioski
1. **DQN i Hiperparametry:** Algorytmy oparte na wartości są niezwykle czułe na dobór hiperparametrów. Odpowiednie zestrojenie współczynnika eksploracji oraz parametru dyskontowania (`Gamma`) jest krytyczne dla osiągnięcia progu sukcesu (+200 punktów).
2. **PPO i Stabilność:** PPO udowadnia swoją renomę jako algorytm typu "state-of-the-art" – już przy domyślnych/zbliżonych do domyślnych parametrach potrafi bardzo szybko i stabilnie rozwiązać zadanie Lądowania.
3. **Analiza A2C:** Analiza wariancji i długości epizodów wykazała, że im dłużej trwał proces lądowania w niedotrenowanym modelu A2C, tym większą sumaryczną karę zbierał agent za niestabilne manewry.