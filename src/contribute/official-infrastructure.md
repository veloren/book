# Official Infrastructure

This page documents the official veloren infrastructure for developers and users.
Everybody is free to host their own servers as they wish, when they are sponsored for the public veloren project, they are listed here.
The following 2 tables show a quick comparision of all our hosts and the servers we run on them.
Additional information regarding single hosts/servers can be listed below them in detail

## hosts

| Name               | FQDN (or IP)    | Owner (Discord) | Cores | Memory(GB) | Storage(GB) | Network(Mbit/s) | Cost | UptimeAprox | Static IP | Public IPv4 | OfflineSince |
|--------------------|-----------------|-----------------|------:|-----------:|------------:|----------------:|-----:|------------:|:---------:|:-----------:|-------------:|
| hetzner-1          |                 | @xMAC94x        |     1 |          2 |          20 |     (1000/1000) | 3€   |     99,90 % |           |           Y | 2019-08-26   |
| mac94-1            | mac94.de        | @xMAC94x        |     3 |          6 |          80 |        (400/40) | -    |     99,00 % | N         |           Y | -            |
| mac94-2            | pftclan.de      | @xMAC94x        |     3 |          6 |          80 |        (200/12) | -    |     90,00 % | N         |           Y | -            |
| gm8-hosting        | eu-01.gm8.app   | @notgne2        |     8 |         16 |          50 |           (?/?) | -    |     99,90 % |           |           Y | -            |
| juli-1             | -               | @Juli199696     |       |            |             |           (?/?) | -    |     90,00 % |           |             | -            |
| angelonfire-server | -               | @AngelOnFira    |       |            |             |           (?/?) | -    |     90,00 % |           |             | -            |
| angelonfire-laptop | -               | @AngelOnFira    |       |            |             |           (?/?) | -    |     90,00 % |           |             | -            |

## servers

| Name              | Host               | type          | FQDN               | Ports | Maintainer (Discord) |
|-------------------|--------------------|---------------|--------------------|-------|----------------------|
| gameserver        | mac94-1            | gameserver    | veloren.mac94.de   | 14004 | @xMAC94x             |
| gameserver-backup | mac94-2            | gameserver    | -                  | -     | @xMAC94x             |
| gameserver        | gm8-hosting        | gameserver    | -                  | -     | @xMAC94x             |
| runner            | mac94-1            | gitlab-runner | -                  | -     | @xMAC94x             |
| runner            | mac94-2            | gitlab-runner | -                  | -     | @xMAC94x             |
| runner            | juli-1             | gitlab-runner | -                  | -     | @Juli199696          |
| runner            | angelonfire-server | gitlab-runner | -                  | -     | @AngelOnFira         |
| runner            | angelonfire-laptop | gitlab-runner | -                  | -     | @AngelOnFira         |
| torvus            | mac94-1            | torvus        | -                  | -     | @xMAC94x             |

## details
### hosts
### servers