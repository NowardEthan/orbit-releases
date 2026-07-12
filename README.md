<p align="center">
  <img src="orbit-icon.png" width="112" alt="Orbit" />
</p>

<h1 align="center">Orbit</h1>

<p align="center">
  <strong>Seu segundo cérebro no bolso.</strong><br/>
  O app da <em>Luna</em> — uma IA companheira com memória e personalidade próprias.
</p>

<p align="center">
  <a href="https://github.com/NowardEthan/orbit-releases/releases/latest">
    <img alt="Última versão" src="https://img.shields.io/github/v/release/NowardEthan/orbit-releases?label=vers%C3%A3o&color=7D3FD0">
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

1. **[Baixe o APK mais recente](https://github.com/NowardEthan/orbit-releases/releases/latest)**
2. Ao instalar, ative **"instalar apps de fontes desconhecidas"** (só na primeira vez).
3. Abra e converse. **As próximas atualizações chegam sozinhas**, direto no app.

> 📱 Android por enquanto. iOS no radar.

## Feito com

`React Native` · `Expo` · `TypeScript` · `Firebase` · backend próprio (**Luna Core**, Node/TypeScript)
integrando LLMs. O app se auto-atualiza checando este repositório — sem loja de apps.

---

<details>
<summary><strong>Sobre este repositório</strong> (para quem tem curiosidade)</summary>

<br/>

Este é o **canal público de distribuição** do Orbit — o código-fonte é privado; aqui ficam só as
coisas que o app precisa baixar sem login:

- **[Releases](https://github.com/NowardEthan/orbit-releases/releases)** — os instaladores (APK).
- **`updates.json`** — o manifesto que o app lê pra saber se há versão nova e o que mostrar no mural.

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
