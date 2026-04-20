# WhisperX Transkriptor — Releases

Öffentliches Repo für die Sparkle-Update-Infrastruktur. Der Quellcode lebt im privaten Repo [WhisperX-Transkriptor](https://github.com/WELTENBERG/WhisperX-Transkriptor).

## Was hier liegt

- [`appcast.xml`](appcast.xml) — Sparkle-Feed, den die App regelmäßig abfragt
- [GitHub Releases](../../releases) — die fertigen `.dmg`-Installer, signiert und notarisiert

## Update-Flow

```
App lokal  →  appcast.xml (this repo)  →  DMG (GitHub Releases)
```

Der Download-Link in der App zeigt auf ein Release-Asset dieses Repos; die App verifiziert die EdDSA-Signatur, bevor der Download überhaupt entpackt wird.

## Wie neue Versionen released werden

Im privaten Repo gibt's `App/release.sh` (wird noch gebaut), das:

1. Baut die App (`build_app.sh`)
2. Notarisiert sie (`notarize.sh`)
3. Packt sie als `.dmg` per `create-dmg`
4. Signiert die DMG mit dem Sparkle-EdDSA-Key
5. Aktualisiert `appcast.xml` in diesem Repo
6. Erstellt ein GitHub-Release mit der DMG als Asset
