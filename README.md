# Docker Dev Environment

Questo progetto fornisce un ambiente di sviluppo completo basato su Docker, con supporto per:

- Apache + PHP (versione configurabile)
- Node.js
- Python
- MariaDB + phpMyAdmin
- Redis
- Mailhog

## Struttura delle cartelle

```
.
├── app/                          # Codice del progetto PHP (Laravel, WordPress, ecc.)
├── config/
│   └── docker-web/               # Dockerfile personalizzato
│        └── apache/
│            ├── base.conf        # Configurazione Apache sempre caricata
│            ├── laravel.conf     # Configurazione per Laravel
│            └── wordpress.conf   # (facoltativa) Altri preset
│        └── php/                 # File php.ini personalizzati
├── data/
│   └── db/                       # Dati persistenti del database
├── .env                          # Variabili d'ambiente (copiato da .env.example)
├── .env.example                  # Esempio di file env
├── .gitignore
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

## Configurazioni Apache

Nel file `.env` puoi specificare quale preset Apache usare (oltre alla configurazione base sempre caricata):

```env
APACHE_PRESET=laravel
```

Il sistema caricherà `base.conf` + `laravel.conf` da `config/docker-web/apache/`.

### Esempi:

- `APACHE_PRESET=none`: solo `base.conf` (default generico)
- `APACHE_PRESET=laravel`: aggiunge configurazione per Laravel (DocumentRoot in `/public`)

## Aggiungere un progetto

### ✅ Progetto generico PHP

Inserisci il codice PHP in `app/`, assicurati che il tuo file di ingresso sia visibile direttamente (es. `index.php`).

### ✅ Progetto Laravel

1. Installa Laravel nella cartella `app/`:

```bash
docker-compose exec web bash
composer create-project laravel/laravel .
```

2. Imposta `APACHE_PRESET=laravel` nel `.env`.

3. Riavvia il container:

```bash
docker-compose up -d --build
```

Visita [http://localhost:8080](http://localhost:8080)

## Licenza

Questo progetto è distribuito sotto la licenza [MIT](LICENSE).