# Docker Dev Environment

Questo progetto fornisce un ambiente di sviluppo completo basato su Docker, con supporto per:

- Apache + PHP
- Node.js
- Python
- MariaDB + phpMyAdmin
- Redis
- Mailhog

## Struttura delle cartelle

```
.
├── app/         # Codice PHP
├── config/
│   └── apache/  # Configurazioni personalizzate di Apache
│   └── php/     # Configurazioni personalizzate di PHP
│   └── docker-web/ # Dockerfile personalizzato
├── data/
│   └── db/      # Dati persistenti del database
├── .env         # Variabili d'ambiente (crealo da .env.example)
├── .env.example # Esempio di file env
├── .gitignore   # File di esclusione per Git
└── docker-compose.yml
```

## Come si usa

1. Copia `.env.example` in `.env` e personalizza le variabili.
2. Avvia l’ambiente con:

```bash
docker-compose up --build -d
```

3. Accedi a:
   - App PHP: http://localhost:8080
   - phpMyAdmin: http://localhost:8081
   - Mailhog: http://localhost:8025

## Variabili configurabili

Guarda il file `.env.example` per l’elenco completo delle variabili configurabili.

## Licenza

Questo progetto è distribuito sotto la licenza [MIT](LICENSE).