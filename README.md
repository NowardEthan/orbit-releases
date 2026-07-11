# orbit-releases

Canal **público** de publicação do Orbit (o app mobile). O código-fonte fica no repo
**privado** `orbit-mobile`; aqui ficam só as coisas que o app precisa baixar **sem login**:

- **`updates.json`** — manifesto: versão mais recente + novidades do mural.
- **Releases do GitHub** — os APKs (o instalador Android).

> Por que separado? Repo privado exige login pra baixar arquivos/APK, e o celular do
> usuário não loga. Este repo público resolve isso sem expor o código.

---

## `updates.json` — schema

| Campo | Tipo | O quê |
|---|---|---|
| `manifestVersion` | number | Versão do formato deste arquivo (hoje `1`). |
| `latestVersion` | string | Última versão publicada (semver, ex.: `"2.1.0"`). O app compara com a própria. |
| `latestVersionCode` | number | `versionCode` Android da última versão (inteiro crescente). |
| `publishedAt` | string | Data da última versão (`YYYY-MM-DD`). |
| `apkUrl` | string | URL do APK. Usa o atalho `releases/latest/download/orbit.apk` (sempre aponta pro release mais novo). |
| `minSupportedVersion` | string | Abaixo disso, a atualização é tratada como obrigatória. |
| `mandatory` | boolean | Força a atualização mesmo acima do mínimo (ex.: bug crítico). |
| `news[]` | array | Itens do mural (ver abaixo). |

### Item de `news`

```json
{
  "id": "2026-07-11-mural",     // único e estável (usado pra "já vi isso")
  "date": "2026-07-11",          // YYYY-MM-DD
  "tag": "novidade",             // novidade | correcao | aviso
  "title": "Título curto",
  "body": "Texto do recado."
}
```

Tags: **`novidade`** (feature nova), **`correcao`** (bug corrigido), **`aviso`** (recado/anúncio).
Coloque os mais recentes **no topo** do array.

---

## Como publicar uma nova versão

1. No `orbit-mobile`, suba a versão em `app.json` (`expo.version`) e o `versionCode` Android.
2. Gere o APK (build local/EAS). Renomeie o arquivo para **`orbit.apk`**.
3. Crie um **Release** no GitHub deste repo:
   - Tag `vX.Y.Z` (ex.: `v2.1.0`), marcada como *latest*.
   - Anexe o `orbit.apk` como asset (o nome precisa ser exatamente `orbit.apk`).
4. Edite o `updates.json`: atualize `latestVersion`, `latestVersionCode`, `publishedAt` e
   **adicione um item em `news`** contando a novidade. Commit + push.

O app checa este `updates.json`, compara com a própria versão e, se houver uma mais nova,
mostra o aviso + badge e oferece baixar o `apkUrl`.

Via `gh` (exemplo):

```bash
gh release create v2.1.0 ./orbit.apk --repo NowardEthan/orbit-releases \
  --title "Orbit 2.1.0" --notes "Novidades desta versão…" --latest
```
