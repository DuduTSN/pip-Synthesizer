# pip-Synthesizer
Singing voice synthesizer made with Python, for Windows: multi-track piano roll, pitch editing, UTAU support and experimental DiffSinger voicebanks integration.
# pip!Synthesizer

**PT** · Um sintetizador de voz cantada criado com Python, para Windows: várias faixas, piano roll, edição de pitch e voicebanks UTAU ou DiffSinger (experimental).
**EN** · A singing voice synthesizer made with Python, for Windows: multi-track piano roll, pitch editing, and UTAU or (experimental) DiffSinger voicebanks.

> Criado por **Dudu** (UniverStars; BETWEEN WORLDS)

## O que faz

- **Várias faixas** com piano roll, copiar/colar, seleção, ferramentas pincel e selecionar, mute/solo/volume/pan.
- **Edição de pitch**: barra «Pitch» por baixo do piano roll para desenhar a curva de afinação (pincel, borracha, Ctrl+Z).
- **Voicebanks UTAU** em pasta (`oto.ini`), com resampler externo ou motor **PSOLA** experimental.
- **Voicebanks DiffSinger** (experimental): modelos ONNX no formato do OpenUtau, vocoder NSF-HiFiGAN, phonemizer japonês, e modelos de variância (duração, pitch, energia/respiração/voicing/tensão) quando existem.
- **Voicebanks encriptados** (`.chrvoice`) e projetos `.chrproject`.
- **Importar `.mid` e `.ust`**; render incremental com cache (só volta a sintetizar o que mudou).
- Temas, interface em **português e inglês**, janela «O que há de novo».

## Instalar e correr

Requer Windows e Python (recomendado 3.10 ou superior).

```
python -m pip install -r requirements.txt
python tools/make_demo_voicebank.py demo_voicebank   # opcional: voicebank de teste (a e i o u)
python main.py
```

Para criar um `.exe`: execute `build_exe.bat`.

### Motor de síntese

Por omissão usa o motor próprio **PSOLA por frases** (experimental), que não precisa de mais nada. Também suporta um **resampler externo** compatível com UTAU (*Motor de síntese*, Ctrl+E): esse programa **não vem neste repositório**, por isso indique o caminho do seu ou ponha um `resampler.exe` em `resampler/`.

### Voicebanks

Nenhum voicebank vem incluído. Use os seus próprios e **respeite a licença de cada um**. Os bancos de voz VOCALOID não são suportados (são proprietários e encriptados).

## Documentação

- [Guia detalhado](docs/GUIA.md): interface, atalhos, motores, DiffSinger, cache.
- [Changelog](CHANGELOG.md)
- Traduções: `core/i18n_en.py` + `python tools/check_i18n.py`.

## Contribuir

Issues e pull requests são bem-vindos. Antes de abrir um PR, corra `python tools/check_i18n.py` e `python tools/selftest.py`.

## Licença

A definir pelo autor.

