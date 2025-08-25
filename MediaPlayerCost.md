# Analisi Costi e Tempi – Audio Player Protetto

## 1. Costi di Componenti (per singola unità)

### Hardware

* **Raspberry Pi Zero 2 W** → \~25 € in retail Italia, \~15–18 € all’ingrosso.
* **Modulo RTC (DS3231)** → 5 € retail, \~2 € in bulk.
* **Resinatura / protezione fisica** → \~5 € DIY, in batch sostituibile con case plastico stampato.
* **Altri componenti** (alimentatore, microSD, batteria RTC, cablaggi) → \~10 €.

### Stima costo prototipo singolo

| Componente                   | Costo stimato |
| ---------------------------- | ------------- |
| Raspberry Pi Zero 2 W        | 25 €          |
| DS3231 RTC                   | 5 €           |
| Resinatura/protezione        | 5 €           |
| Altri componenti             | 10 €          |
| **Totale stimato per unità** | **\~45 €**    |

---

## 2. Costi per Batch / Produzione in scala

### Small batch (100–1000 unità)

* Raspberry Pi Zero 2 W: \~18 € cad.
* RTC moduli: \~2 € cad.
* Case plastico stampato a iniezione: \~3 € cad. (dopo costo stampo).
* Altri componenti (microSD, alimentazione): \~8 € cad.
* Assemblaggio/PCB: 5–10 € cad.

### Stima costo per unità (produzione industriale)

| Componente                   | Costo stimato |
| ---------------------------- | ------------- |
| Raspberry Pi Zero 2 W        | 18 €          |
| DS3231 RTC                   | 2 €           |
| Case plastica stampata       | 3 €           |
| Altri componenti             | 8 €           |
| Assemblaggio/PCB             | 5–10 €        |
| **Totale stimato per unità** | **\~36–41 €** |

Nota: se lo stampo costa \~8.000 € per 5.000 unità, incide per \~1,6 € a pezzo.

---

## 3. Tempo di sviluppo (lavorando da solo)

| Fase di lavoro                          | Tempo stimato             |
| --------------------------------------- | ------------------------- |
| Prototipo hardware + resinatura         | 5–7 gg                    |
| Software base (player cifrato, BT, RTC) | 10–15 gg                  |
| Integrazione USB gadget e SSH           | 3–5 gg                    |
| Gestione licenze (JWT, server + token)  | 5–7 gg                    |
| Testing e stabilizzazione               | 7–10 gg                   |
| **Totale stimato**                      | **30–40 gg** ≈ 1,5–2 mesi |

---

## 4. Riepilogo

* **Costo unitario prototipo singolo**: \~45 €.
* **Costo unitario in batch**: \~36–41 €.
* **Tempi sviluppo (1 persona)**: \~1,5–2 mesi lavorativi.

Questa stima copre solo hardware + sviluppo software + gestione licenze. Non include costi server, packaging, distribuzione o supporto post‑vendita.
