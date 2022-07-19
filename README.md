# 🐾 Pounce

_pounce is a multi-client, TLS-only IRC bouncer. It maintains a persistent connection to an IRC server, acting as a proxy and buffer for a number of clients. When a client connects, any messages received since it last disconnected will be relayed to it. Unlike some other bouncers, pounce uses a single buffer for all IRC messages, which acts as a queue from which each client reads messages independently._

See https://git.causal.agency/pounce/about/ for more information.

## About This Image

This is a CRI / Docker-compliant image containing Pounce as well as the `pounce-palaver` and `pounce-notify` components. It's built using a multi-stage build to keep the resulting image as lean as possible (~12MiB).

## How To Use

### pounce
**Friendly reminder:** Pounce requires that TLS be configured for communication, even if you're using a reverse proxy - you cannot force it to start without a certificate!

The image runs `pounce /config/pounce.conf` by default, so mounting your config there (with `-v my_pounce_config:/config/pounce.conf`), as well as any necessary certificates (something like `-v cert.pem:/config/cert.pem -v cert.key:/config/cert.key`) should get you started.

You should run one instancce of the container per server connection.

See [pounce(1)](https://git.causal.agency/pounce/about/pounce.1) for more information.

### pounce-notify, pounce-palaver, etc

Run another instance of the container with the desired command & arguments, eg `pounce-palaver pounce-host`.

See [pounce-notify](https://git.causal.agency/pounce/about/pounce-notify.1) and [pounce-palaver](https://git.causal.agency/pounce/about/pounce-notify.1) for more information.
