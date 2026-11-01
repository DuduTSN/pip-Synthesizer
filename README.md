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
- **Temas** (Noite, Claro, Sakura, Ciano, Clássico), interface em **português e inglês**, janela «O que há de novo» e janela «Sobre».

## Instalar e correr

Requer Windows e Python (recomendado 3.10 ou superior).

```
python -m pip install -r requirements.txt
python tools/make_demo_voicebank.py demo_voicebank   # opcional:
