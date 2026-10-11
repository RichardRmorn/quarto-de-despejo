# Quarto de Despejo – projeto Android (APK)

O jogo (HTML5) roda dentro de um WebView em tela cheia, offline. Saves = localStorage do WebView.
Botão Voltar do Android = pausa o jogo.

## Como gerar o APK (escolha um)

**A) Sem instalar nada – GitHub Actions (mais fácil)**
1. Crie um repositório no GitHub e envie esta pasta inteira.
2. Aba *Actions* → *Build APK* → *Run workflow*.
3. Ao terminar, baixe o artefato `quarto-de-despejo-apk` (contém `app-debug.apk`).

**B) Android Studio**: *File → Open* nesta pasta → *Build → Build APK(s)*.

**C) Linha de comando** (JDK 17 + Android SDK, `ANDROID_HOME` definido): `./gradlew assembleDebug`
O APK sai em `app/build/outputs/apk/debug/app-debug.apk`.

## Instalar
Copie o APK para o celular, permita "instalar apps desconhecidos" e abra.

## Compatibilidade real (leia)
- O APK **instala** desde o Android 4.1 (minSdk 16) e roda em qualquer versão mais recente.
- O jogo usa tecnologias modernas (unidades CSS `cqw`, Web Audio, JavaScript ES6). Elas exigem WebView
  com Chromium 105+. Em Android 5.0+ o *Android System WebView* se atualiza pela Play Store, então
  funciona. Em Android 4.1–4.4 o WebView é do sistema e não atualiza: o jogo mostra um aviso
  explicando em vez de travar.
- Para rodar de verdade no 4.1–4.4 seria preciso reescrever o jogo (ES5, CSS sem cqw, áudio alternativo)
  ou embutir um motor de navegador próprio (Crosswalk) – conversa à parte.

## Publicar na Play Store (futuro)
Gere uma chave própria (`keytool -genkeypair ...`), guarde-a e as senhas em local seguro (se perder, não
há como atualizar o app) e use `QD_KEYSTORE`, `QD_STOREPASS`, `QD_KEYALIAS`, `QD_KEYPASS` com `./gradlew bundleRelease`.
A Play Store exige minSdk ≥ 21 para novos apps.
