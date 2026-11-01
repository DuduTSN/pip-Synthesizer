# pip!Synthesizer

**[Português](#português)** · **[English](#english)**

> Criado por / Created by **Dudu** (UniverStars; BETWEEN WORLDS) · v0.5

---

# Português

Um sintetizador de voz cantada criado com Python, para Windows: várias faixas, piano roll, edição de pitch e voicebanks UTAU ou DiffSinger (experimental). Os projetos usam a extensão `.chrproject` e os voicebanks podem ser pastas ou ficheiros encriptados `.chrvoice`.

## Funcionalidades

- **Várias faixas**, cada uma com o seu cantor, mute/solo, volume e pan; mistura estéreo.
- **Piano roll** com ferramentas pincel e selecionar, copiar/colar (também entre faixas) e atalhos de teclado.
- **Edição de pitch**: barra «Pitch» por baixo do piano roll para desenhar a curva de afinação.
- **Voicebanks UTAU** em pasta (`oto.ini`), com o motor PSOLA próprio ou um resampler externo.
- **Voicebanks DiffSinger (experimental)**: modelos ONNX no formato do OpenUtau, com vocoder NSF-HiFiGAN, phonemizer japonês e modelos de variância.
- **Voicebanks encriptados** (`.chrvoice`).
- **Importar `.mid` e `.ust`**, e converter projetos do OpenUtau (`.ustx`).
- **Render incremental com cache**, também em segundo plano: só volta a sintetizar o que mudou.
- **Temas** (Noite, Claro, Sakura, Ciano, Clássico), janela «O que há de novo» e janela «Sobre».

## Requisitos

- Windows.
- **Por precaução, é preciso ter o Python instalado** (https://www.python.org/downloads/).
- Erros inesperados ficam em `%USERPROFILE%\.pip_synth\crash.log` e aparecem numa caixa de diálogo.

## Primeiros passos

*Cantores* → importar a pasta do voicebank → *Definir como cantor padrão* → *Novo projeto* → clicar/arrastar na grelha para criar notas → duplo-clique numa nota para escrever a letra → Espaço para ouvir.

## Interface

- **Splash** animada ao iniciar (pode ser desligada em Definições).
- **Menu principal** (Ctrl+M volta a ele): *Início* (novo, abrir, continuar, recentes), *Projetos*, *Cantores* (importar pasta de voicebank UTAU ou DiffSinger / `.chrvoice`, encriptar, cantor padrão) e *Definições* (tema, splash, animações).
- **Editor**: barra de transporte com visor LCD (tempo, compasso, BPM, fórmula, snap) e retrato do cantor; faixas à esquerda (duplo-clique ou botão direito para propriedades: cor,
