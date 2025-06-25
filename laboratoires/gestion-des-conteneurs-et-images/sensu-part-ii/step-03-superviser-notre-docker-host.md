# Step 03 - Superviser notre Docker Host

* Ajouter le plug-in permettant la surveillance

```bash
sensuctl.exe asset add sensu/monitoring-plugins:2.2.0-1
```

```
fetching bonsai asset: sensu/monitoring-plugins:2.2.0-1
added asset: sensu/monitoring-plugins:2.2.0-1

You have successfully added the Sensu asset resource, but the asset will not get downloaded until
it's invoked by another Sensu resource (ex. check). To add this runtime asset to the appropriate
resource, populate the "runtime_assets" field with ["sensu/monitoring-plugins"].
```

* Créer un "listener" spécifique pour le protocole NTP

```bash
sensuctl.exe check create ntp ^
  --runtime-assets "sensu/monitoring-plugins" ^
  --command "check_ntp_time -H time.nist.gov--warn 0.5 --critical 1.0" ^
  --output-metric-format nagios_perfdata ^
  --publish="true" ^
  --interval 30 ^
  --timeout 10 ^
  --subscriptions linux
```

```
Created
```

* Lister les "event listener" présents sur Sensu

```
sensuctl.exe event list
```

{% code fullWidth="true" %}
```
     Entity        Check                                              Output                                             Status   Silenced             Timestamp                              UUID
─────────────── ─────────── ─────────────────────────────────────────────────────────────────────────────────────────── ──────── ────────── ──────────────────────────────── ───────────────────────────────────────
  ccfb127bc70c   keepalive   Keepalive last sent from ccfb127bc70c at 2024-09-03 09:21:30 +0000 UTC                           0   false      2024-09-03 11:21:30 +0200 CEST   4a21cacd-54f5-4b3a-9704-91203f99898f
  ccfb127bc70c   ntp         check_ntp_time: Invalid hostname/address - time.nist.gov--warn                                   3   false      2024-09-03 11:21:24 +0200 CEST   3c384df9-8931-40c2-872b-640909325d1f
                             Usage:
                              check_ntp_time -H <host> [-4|-6] [-w <warn>] [-c <crit>] [-v verbose] [-o <time offset>]
```
{% endcode %}

* Observer l'état de la surveillance via la console web

<figure><img src="../../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>
