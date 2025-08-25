Progetto: Audio Player Protetto con Modalità Pro
================================================

Obiettivo
---------

Creare un dispositivo dedicato (basato su Raspberry Pi Zero 2 W) in grado di riprodurre file audio cifrati, impedendo la copia non autorizzata e con possibilità di sbloccare una **Modalità Pro** tramite abbonamento a pagamento.

* * *

Requisiti Funzionali
--------------------

1.  **Riproduzione Audio**
    
    *   File audio cifrati, decrittati solo in RAM.
        
    *   Nessuna possibilità di copia o accesso diretto ai file.
        
2.  **Controllo Utente**
    
    *   Controllo tramite **Bluetooth** (app mobile) con comandi play/pause/volume.
        
    *   **USB Gadget** per manutenzione e accesso SSH solo da sviluppatore.
        
3.  **Modalità Pro (Abbonamento)**
    
    *   Modalità Standard → funzioni base.
        
    *   Modalità Pro → funzioni aggiuntive e contenuti premium.
        
    *   Sblocco tramite **token JWT** generato da server remoto, validato dal dispositivo.
        
4.  **Gestione Tempo e Licenze**
    
    *   **RTC hardware** (es. DS3231) per mantenere data/ora anche senza alimentazione.
        
    *   **Aggiornamento periodico dell’orario via Bluetooth** come ridondanza.
        
    *   Validazione della scadenza (`exp`) inclusa nel token JWT.
        

* * *

Architettura Tecnica
--------------------

### Hardware

*   Raspberry Pi Zero 2 W
    
*   Modulo RTC (DS3231) con batteria tampone
    
*   Uscita audio (jack 3.5mm o digitale)
    
*   PCB e storage resinati per protezione fisica
    

### Software

*   OS minimale (Raspberry Pi OS Lite o Buildroot)
    
*   Player custom (Python/C++)
    
*   File cifrati (AES-256)
    
*   Server Flask per controllo via BT
    
*   Validazione JWT tramite chiave pubblica integrata
    

### Sicurezza

*   Nessun servizio SSH attivo su Wi-Fi/BT
    
*   Accesso manutenzione solo via **USB Gadget (Ethernet over USB)** o UART
    
*   Storage resinato e bloccato fisicamente
    

* * *

Gestione Licenze
----------------

1.  **Server Remoto**
    
    *   Gestione utenti e pagamenti (Stripe/PayPal)
        
    *   Generazione token JWT con scadenza (`exp`)
        
    *   Invio token al cliente (via app o file)
        
2.  **Cliente (App Mobile/PC)**
    
    *   Riceve token JWT
        
    *   Trasmette token al device via Bluetooth o USB
        
    *   Trasmette anche data/ora corrente per sincronizzazione
        
3.  **Device (Raspberry Player)**
    
    *   Verifica validità token con chiave pubblica
        
    *   Confronta `exp` con orologio RTC
        
    *   Abilita o disabilita modalità Pro
        

* * *

Flusso d'Uso
------------

1.  Cliente acquista abbonamento.
    
2.  Server genera token JWT valido (es. 30 giorni).
    
3.  Cliente riceve token e lo invia al dispositivo via BT.
    
4.  Dispositivo valida token, aggiorna RTC se necessario, abilita modalità Pro.
    
5.  Alla scadenza, il token non è più valido → ritorno automatico a modalità Standard.
    

* * *

Schema Mermaid
--------------
``` mermaid

    flowchart TD
        subgraph Server[Server Remoto]
            P[Gestione Pagamenti]
            U[Gestione Utenti]
            L[Generazione Licenze JWT con exp]
            P --> L
            U --> L
        end
    
        subgraph Client[App Mobile / PC Cliente]
            T[Token JWT ricevuto]
            D[Data/Ora Corrente]
        end
    
        subgraph Device[Raspberry Player + RTC]
            R[RTC Hardware con batteria]
            V[Chiave pubblica integrata]
            C[Verifica Token + Scadenza]
            A[Audio Cifrato]
            Pm[Player Standard]
            Pro[Player Pro]
        end
    
        L -->|Invio Token| T
        T -->|Bluetooth / USB Gadget| C
        D -->|Bluetooth Sync| R
        R -->|Orario attuale| C
        V --> C
        C -->|Token valido e non scaduto| Pro
        C -->|Token non valido/scaduto| Pm
        A --> Pm
        A --> Pro
```

* * *

Conclusione
-----------

Il sistema combina **protezione fisica**, **cripto a livello software**, e **gestione licenze basata su token**.  
L’RTC hardware garantisce affidabilità del controllo scadenze, mentre l’aggiornamento via Bluetooth assicura ridondanza.  
Il risultato è un dispositivo blindato, sicuro e flessibile, adatto a un modello di business basato su abbonamenti.