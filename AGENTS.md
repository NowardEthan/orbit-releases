# Diretrizes do orbit-releases — leia antes de mexer

> Para qualquer agente de IA ou pessoa. Escreva tudo em **pt-BR** (nunca pt-PT). **O guia completo
> do ecossistema Orbit está em `orbit-mobile/AGENTS.md`** — leia-o; aqui ficam só as regras deste
> repo de distribuição.

## O que é
Este repo **distribui** o app Orbit. Ele não tem código do app — só os manifestos de atualização e
os APKs servidos pelos **GitHub Releases**:

- **`updates.json`** — canal **estável**. O app estável compara o `latestVersionCode` daqui.
- **`updates-beta.json`** — canal **beta** (o «Orbit β», app separado).
- O app baixa o APK dos **Releases**, não do repositório.

## Sucessor: Orbit Compose (OrbitLab)

O APK publicado nos canais **estável/beta** **vai passar a ser** o build Compose
(`OrbitLab/` / [`orbit-lab`](https://github.com/NowardEthan/orbit-lab)), não o Expo.
Mesmo `orbit.apk`, mesmos `applicationId` e assinatura. Até lá, continua o APK do
`orbit-mobile`. Ver `OrbitLab/RELEASING.md`.

### Canal só do lab (teste)

**`updates-lab.json`** — package `com.ethan.orbitlab`, tag de release **`lab`**.
Serve para o Ethan testar o auto-update Compose→Compose **sem** tocar no Orbit
instalado. Não é o canal de produção. Passos: `OrbitLab/TESTE-UPDATE.md`.

## 🛑 Regras que evitam estrago

1. **`orbit.apk` é gitignored — de propósito.** O APK vai pelo **asset do Release**, nunca pelo
   git. Commite **só** os `updates*.json`. (Fluxo: copia o APK certo pra `orbit.apk` local →
   `gh release upload …`.)

2. **`versionCode` só sobe.** Nunca repita nem diminua — o app compara por `versionCode`; um número
   igual/menor não é oferecido como atualização.

3. **Estável ≠ beta.** Não misture:
   - **Estável:** atualize `updates.json` e crie o release `v<X.Y.Z>` (`gh release create`). O app
     baixa de `releases/latest/download/orbit.apk` — então o release `v…` **não pode** ser
     pre-release.
   - **Beta:** atualize `updates-beta.json` e suba o APK no tag fixo **`beta`** (que É pre-release):
     `gh release upload beta ./orbit.apk --clobber`.
   - Nunca publique um build de teste/beta como release estável.
   - **`updates-lab.json`** é só para o package do lab Compose (teste). Não mistures
     com estável/beta do Expo.

4. **Verifique pelo raw, não pela API.** Confira os manifestos em
   `raw.githubusercontent.com/NowardEthan/orbit-releases/main/updates.json` (e `…-beta.json`). A
   API do GitHub tem rate-limit de 60/h por IP (o celular e o PC dividem o IP no Wi-Fi).

5. **Cadência (regra do Ethan).** Lançar release tem **critério**: batele um capítulo coerente,
   **não** 1 release por micro-mudança. Uma entrada de `news` consolidada, não uma enxurrada.

## O mural (`news`)
Cada `updates*.json` tem um array `news` (as novidades que o app mostra). Ao publicar, prepende
**uma** entrada clara do capítulo (id único, date, version, tag, title, body em pt-BR) — não várias
por micro-mudança.

_Na dúvida sobre canais ou releases: pergunte antes. O guia completo está em
`orbit-mobile/AGENTS.md`._
