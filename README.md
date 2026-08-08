<p align="center">
  <img src="orbit-icon.png" width="112" alt="Orbit" />
</p>

<h1 align="center">Orbit</h1>

<p align="center">
  <strong>Seu segundo cérebro no bolso.</strong><br/>
  O app da <em>Luna</em> — uma IA companheira com memória e personalidade próprias.
</p>

<p align="center">
  <a href="https://github.com/NowardEthan/orbit-lab-releases/releases">
    <img alt="Versão do Lab" src="https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fraw.githubusercontent.com%2FNowardEthan%2Forbit-releases%2Fmain%2Fupdates-lab.json&query=%24.latestVersion&label=Lab&color=7D3FD0">
  </a>
  <img alt="Android" src="https://img.shields.io/badge/Android-APK-3DDC84?logo=android&logoColor=white">
  <img alt="Status" src="https://img.shields.io/badge/status-beta-F5D047">
</p>

---

## O que é a Luna

A maioria dos apps de IA trata cada conversa como uma folha em branco. A **Luna** não: ela
tem **memória** e **personalidade próprias** — lembra de você, forma opiniões, e às vezes
discorda. A ideia é ser um **exocórtex**, um lugar pra despejar as mil ideias de uma mente
que pula entre assuntos e volta pra elas depois.

O **Orbit** é o app que leva a Luna pro seu bolso.

## Recursos

- 💬 **Conversa por texto e voz** — fale ou escreva; a fala é transcrita na hora.
- 🧠 **Memória persistente** — a Luna carrega o contexto de você entre as conversas.
- 📎 **Anexos** — mande imagens e documentos; ela lê e usa no papo.
- 🔀 **Ramifica conversas** — explore um caminho alternativo sem perder o original.
- 📤 **Exporta em Markdown** — leve suas conversas pro Obsidian, Notion ou Drive.
- 🔎 **Pesquisa na web** — quando o assunto pede, ela busca e cita fontes.
- 🗞️ **Atualização automática** — avisos de nova versão e um mural de novidades dentro do app.

## Baixar (Android)

> Este repo ficou como **ponte legado**. A produção atual do OrbitLab agora vive em
> [`orbit-lab-releases`](https://github.com/NowardEthan/orbit-lab-releases), e o debug em
> [`orbit-lab-debug-releases`](https://github.com/NowardEthan/orbit-lab-debug-releases).

1. **[Abra as releases de produção do Lab](https://github.com/NowardEthan/orbit-lab-releases/releases)**
2. Ao instalar, ative **"instalar apps de fontes desconhecidas"** (só na primeira vez).
3. Abra e converse. **As próximas atualizações chegam sozinhas**, direto no app.

> 📱 Android por enquanto. iOS no radar.

## Feito com

`Kotlin` · `Jetpack Compose` · `Firebase` · backend próprio (**Luna Core**, Node/TypeScript)
integrando LLMs. O app se auto-atualiza checando este repositório — sem loja de apps.

---

<details>
<summary><strong>Sobre este repositório</strong> (para quem tem curiosidade)</summary>

<br/>

Este é o **canal público de distribuição** do Orbit — o código-fonte é privado; aqui ficam só as
coisas que o app precisa baixar sem login:

- **[Produção atual](https://github.com/NowardEthan/orbit-lab-releases/releases)** — releases versionadas do OrbitLab.
- **[Debug](https://github.com/NowardEthan/orbit-lab-debug-releases/releases)** — releases versionadas de teste/debug.
- **`updates-lab.json` neste repo** — ponte de migração para apps antigos.
- **`updates.json`** — manifesto legado do Orbit mobile/Expo.

Esquema resumido do `updates.json`:

```jsonc
{
  "latestVersion": "2.1.1",     // versão mais recente (semver)
  "latestVersionCode": 3,        // versionCode Android
  "apkUrl": "…/releases/latest/download/orbit.apk",
  "news": [                      // itens do mural na aba Início
    { "id": "…", "date": "AAAA-MM-DD", "tag": "novidade", "title": "…", "body": "…" }
  ]
}
```

O app compara `latestVersion` com a própria versão instalada; se houver uma mais nova, mostra o
aviso e oferece baixar o `apkUrl`.

</details>

<p align="center"><sub>Feito com carinho por <a href="https://github.com/NowardEthan">Ethan</a>.</sub></p>
