# Post LinkedIn — Sashimi público

Copiar el bloque de abajo. No publicar desde acá.

---

Abrí el repositorio de Sashimi.

Es un payment gateway crypto-fiat para LATAM: el comprador paga en pesos (o crypto) y el comercio liquida en USDT o USDC. El problema de diseño no es “aceptar cripto”. Es sostener dos rails detrás de una sola API, con estado de liquidación que no se contradiga entre banco y chain.

Cuatro decisiones que importan si vas a leer el código:

HD wallets. Cada orden deriva una deposit address propia en TRON y Solana. No hay una cuenta compartida que después haya que desambiguar a mano.

Dual rail. Cash-in: ARS/BRL por CVU o PIX, el merchant recibe USDT. Crypto: USDT/USDC on-chain, o off-ramp a fiat local. El merchant elige settlement_mode; el contrato del API es el mismo.

Webhooks HMAC-SHA256 e idempotencia. El merchant no adivina si pagaron. El evento llega firmado. Reintentar createOrder no duplica el cobro.

Un Docker Compose. Postgres, Redis, API con checkout estático, Prometheus y Grafana. `docker compose up -d --build`. Para integrar: REST, SDK o el widget.

Stack: Java 21, Spring Boot 3.3, Maven multi-módulo, PostgreSQL, Redis, Next.js, @sashimi/sdk y widget JS.

Repo: https://github.com/Matias-Sanmiguel/sashimi-public
Docs: https://matias-sanmiguel.github.io/sashimi-public/
