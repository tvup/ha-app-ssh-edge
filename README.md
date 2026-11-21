# Terminal & SSH (OpenSSH edge)

Kopi af Home Assistants officielle [Terminal & SSH](https://github.com/home-assistant/app-ssh)-tilføjelse
(upstream commit `8f5da32`), hvor OpenSSH opgraderes til den nyeste version fra Alpine **edge**
(p.t. OpenSSH 10.6p2). Alt andet er uændret.

Tilføjelsen bygges lokalt på Home Assistant (intet færdigt image).

## Installation
Indstillinger → Tilføjelser → Butik → ⋮ → Repositories → tilføj `https://github.com/tvup/ha-app-ssh-edge`.

Kan ikke køre samtidig med den originale Terminal & SSH (begge bruger port 22).

## Opdatering
Når upstream eller Alpine edge har en ny OpenSSH: hæv `version` i `ssh_edge/config.yaml` og opdatér tilføjelsen i HA (den genbygges).

Licens: Apache 2.0 (som upstream).
