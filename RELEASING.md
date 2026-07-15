# Como lançar o Orbit

Dois canais, dois manifestos. O **estável** (`updates.json`) é o mural oficial — só o
validado. O **beta** (`updates-beta.json`) é o pré-release, pro Ethan testar no celular pelo
auto-update sem sujar o oficial. O app escolhe o canal pelo interruptor «Canal de testes» nos
ajustes; compara por `latestVersionCode`.

## Princípio (ver memória `release-cadence-criterio`)

Commits são frequentes; **releases são bateladas** num capítulo coerente. Nada de uma release
por micro-mudança. `patch` = lote de correções; `minor` = feature/lote temático.

## Fluxo de um capítulo

1. **Trabalhar no `dev`** (orbit-mobile). Commitar à vontade.
2. **Pré-release (beta)** quando o capítulo fecha:
   - Bump `app.json`+`package.json` para `X.Y.Z` e `versionCode` (o code SEMPRE sobe).
   - `npm run android:apk` no `dev`.
   - Publicar o APK no release fixo **`beta`** (recriar pra atualizar o asset):
     `gh release delete beta -y; gh release create beta ./dist/orbit-mobile-X.Y.Z.apk --prerelease --title "beta X.Y.Z" --notes "…"`
   - Em `orbit-releases`: `updates-beta.json` → `latestVersion`, `latestVersionCode`,
     `apkUrl = .../releases/download/beta/orbit.apk`, e as notas do rc. Commit+push.
   - O Ethan (com beta ligado) auto-atualiza. Validar com ele.
3. **Oficial**, quando validado:
   - `git checkout master && git merge dev` (fast-forward).
   - `npm run android:apk` no `master` (ou reaproveitar o APK validado).
   - `gh release create vX.Y.Z ./dist/orbit-mobile-X.Y.Z.apk` (asset `orbit.apk`).
   - `updates.json` → nova versão + **uma** entrada de mural (tema + bullets). Commit+push.
   - `updates-beta.json` volta a espelhar o estável (`apkUrl` = `releases/latest/download/orbit.apk`),
     mesma versão — pra ninguém no beta ficar «atrás».

## Core (luna-core)

`main` auto-deploya no Railway (produção). Não há APK: o «pré-release» é a bateria de testes
empíricos (P16/P18/P19…) + typecheck rodando no `dev`. Só `merge dev→main` quando passa —
o merge é que faz o deploy. Verificar sempre pelo `commit` no `/health`, nunca por `ok:true`.
