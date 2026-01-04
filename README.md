# 📄 Lysz210 CV - Microfrontend

Questo repository ospita il Microfrontend del Curriculum Vitae per il progetto **Lysz210**. Realizzato con **Nuxt 4**, il progetto utilizza un'architettura ibrida ottimizzata per la velocità e la gestione dinamica dei contenuti.

## 🚀 Architettura del Progetto

Il Microfrontend non contiene i dati del CV al suo interno, ma agisce come un guscio reattivo che si popola a runtime:

* **Dati Dinamici (Client-side):** Al caricamento della pagina, il browser effettua il fetching dei dati (esperienze, skill, progetti) direttamente dal repository [lysz210/profile](https://github.com/lysz210/profile). Questo garantisce che il CV sia sempre aggiornato all'ultimo commit del profilo senza necessità di una nuova build.
* **Gestione PDF (Server-side):** La logica di backend, ospitata su **AWS Lambda**, gestisce il recupero e la distribuzione del documento PDF del CV, anch'esso archiviato centralmente nel repository del profilo.
* **Distribuzione Asset:** S3 e CloudFront gestiscono la distribuzione dei file statici e del codice dell'applicazione, garantendo latenza minima a livello globale.

## 🛠️ Stack Tecnologico

* **Framework:** Nuxt 4 (Nitro Engine)
* **Infrastructure:** Terraform
* **Hosting:** * **Frontend:** AWS S3 + CloudFront (Static Assets)
* **Backend:** AWS Lambda


* **CI/CD:** GitHub Actions con autenticazione OIDC (OpenID Connect)

## 🔄 Workflow di Sviluppo e Deploy

1. **Sviluppo Locale:** L'app punta al repository del profilo tramite variabili d'ambiente.
2. **Push:** Ogni push su `main` avvia la GitHub Action.
3. **Deploy:**
* I file statici vengono sincronizzati su **S3**.
* Il server Nitro (per i PDF) viene aggiornato su **Lambda**.
* Viene eseguita l'invalidazione della cache su **CloudFront**.
