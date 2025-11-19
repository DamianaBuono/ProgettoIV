# Zombie Shooting – Reinforcement Learning
## Descrizione
Questo progetto ricrea una versione semplificata del classico gioco di **eliminazione degli zombie**, con l’obiettivo di addestrare un agente tramite algoritmi di **Reinforcement Learning (RL)**.
L’agente impara progressivamente a muoversi, rilevare i nemici e colpirli, affrontando livelli con difficoltà crescente.
Il comportamento è guidato da un sistema di **reward shaping** che incentiva azioni corrette e penalizza errori o inefficienze.

Il modello utilizza il sensore percettivo **RayPerceptionSensor3D** per rilevare la presenza degli zombie e una struttura di osservazioni che evolve nei vari livelli, aumentando il livello di complessità del task.

## Caratteristiche principali

* Movimenti su assi X (sinistra/destra) e Y (rotazione)

* Rilevamento degli zombie tramite **RayPerceptionSensor3D**

* Tre livelli di complessità crescente (statici → in movimento → numerosi con munizioni limitate)

* Sistema di reward progettato per massimizzare colpi a segno e minimizzare collisioni e sprechi

* Addestramento monitorato tramite metriche come episode length, cumulative reward e loss curves

# Meccaniche dell'agente
## Movimenti

* **X**→ sinistra/destra

* **Y** → rotazione

## Osservazioni

* **Space size 1** → Livello 1 e 2

* **Space size 2** → Livello 3

## Spazio delle azioni

* 4 azioni disponibili in ogni livello

# Reward
| Azione                 | Descrizione                               | Reward  |
|------------------------|---------------------------------------------|---------|
| Colpisce lo zombie     | L’agente colpisce correttamente un nemico  | **+6**  |
| Non colpisce lo zombie | Spara e manca il bersaglio                 | **–0.40** |
| Collisione con zombie  | L’agente viene colpito o troppo vicino     | **–1.5** |
| Collisione con muri    | Movimento scorretto                        | **–1.5** |
| Finisce i proiettili   | Utilizzo inefficiente delle risorse        | **–1.5** |

# Training
## Primo livello – Zombie statici

Gli zombie sono fermi ma generati in posizioni casuali.
L’agente impara a individuarli e colpirli.
Max Steps: **2.0M**

## Andamento del training

* Reward in crescita iniziale e stabilizzazione finale

* Diminuzione delle pertes (losses) dopo stabilizzazione

# Secondo livello – Zombie in movimento

Gli zombie si muovono verso l’agente.
Numero variabile tra **3 e 9 zombie**.
Max Steps: **1.5M**

## Andamento del training

* Reward in crescita e stabilizzazione

* Episodi più lunghi, segno di una maggiore sopravvivenza

* Losses in diminuzione nel tempo

# Terzo livello – Munizioni limitate

Gli zombie aumentano e le munizioni sono limitate.
Numero nemici: **6–12**, con munizioni assegnate di conseguenza + **5 proiettili bonus**.
Max Steps: **1.5M**

## Andamento del training

* Reward cumulativa in crescita

* Episodi più lunghi

* Variabilità elevata → possibile instabilità della politica

# Conclusioni

Il progetto dimostra come un agente possa apprendere a superare progressivamente sfide più complesse in un ambiente dinamico attraverso il **Reinforcement Learning**.
L’evoluzione dei tre livelli evidenzia un miglioramento significativo nelle capacità dell’agente, sia nel rilevamento degli zombie sia nella gestione delle risorse.

# Sviluppi futuri

* Introduzione di ostacoli nella stanza per limitare la visuale dell’agente

* Implementazione di tipologie diverse di zombie, con reward differenti

* Potenziamento dell’ambiente con obiettivi complessi o power-up
