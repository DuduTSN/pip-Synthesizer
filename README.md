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

---

# English

A singing voice synthesizer made with Python, for Windows: multi-track piano roll, pitch editing, and UTAU or (experimental) DiffSinger voicebanks. Projects use the `.chrproject` extension, and voicebanks can be plain folders or encrypted `.chrvoice` files.

## Features

- **Multiple tracks**, each with its own singer, mute/solo, volume and pan; stereo mix.
- **Piano roll** with brush and select tools, copy/paste (also between tracks) and keyboard shortcuts.
- **Pitch editing**: a “Pitch” bar below the piano roll to draw the pitch curve.
- **UTAU voicebanks** as folders (`oto.ini`), with the built-in PSOLA engine or an external resampler.
- **DiffSinger voicebanks (experimental)**: ONNX models in the OpenUtau format, with the NSF-HiFiGAN vocoder, a Japanese phonemizer and variance models.
- **Encrypted voicebanks** (`.chrvoice`).
- **Import `.mid` and `.ust`**, and convert OpenUtau projects (`.ustx`).
- **Incremental rendering with a cache**, also in the background: only what changed is synthesized again.
- **Themes** (Night, Light, Sakura, Cyan, Classic), a “What's new” window and an “About” window.

## Requirements

- Windows.
- **As a precaution, you need to have Python installed** (https://www.python.org/downloads/).
- Unexpected errors are saved to `%USERPROFILE%\.pip_synth\crash.log` and shown in a dialog.

## Getting started

*Singers* → import the voicebank folder → *Set as default singer* → *New project* → click/drag on the grid to create notes → double-click a note to type the lyric → press Space to listen.

## Interface

- Animated **splash** on start-up (can be turned off in Settings).
- **Main menu** (Ctrl+M returns to it): *Home* (new, open, resume, recent), *Projects*, *Singers* (import a UTAU or DiffSinger voicebank folder / `.chrvoice`, encrypt, default singer) and *Settings* (theme, splash, animations).
- **Editor**: transport bar with an LCD display (time, bar, BPM, time signature, snap) and the singer's portrait; tracks on the left (double-click or right-click for properties: colour, singer, volume, pan); piano roll below, with the other tracks shown as “ghosts”.
- **Open/import**: *File → Open…* (Ctrl+O) opens `.chrproject`, `.mid`/`.midi` and `.ust` as a new project; *Import MIDI / UST into this project…* (Ctrl+I) adds tracks; you can also drag the file onto the window. Each track is a single voice (chords keep the highest note, overlaps are trimmed), the percussion channel is ignored and karaoke MIDI lyrics are used.
- **What's new**: the “What's new in this update?” window opens by itself once per version and can be reopened from *Help → What's new*. For the next version, edit `releases()` in `ui/whatsnew.py` and `VERSION` in `ui/splash.py`.

**Shortcuts:** Space (play/stop), Ctrl+N/O/S, Ctrl+Shift+S, Ctrl+Shift+E (export WAV), Ctrl+T (new track), F2 (track properties), Ctrl+L (insert lyrics), Ctrl+E (engine), Ctrl+Z (undo), Ctrl+M (main menu), Ctrl+I (import MIDI/UST).

### Piano roll: tools and selection

- **Brush** (B): click creates a note, dragging stretches it. **Select** (V): click a note, or drag over an empty area to pick several.
- Ctrl/Shift+click adds or removes notes from the selection; dragging moves the group (start and pitch); dragging the right edge stretches them all. Esc clears the selection; Delete or right-click erases.
- Ctrl+A selects all; Ctrl+C / Ctrl+X / Ctrl+V copy, cut and paste (also from the *Edit* menu, and between tracks). Paste goes at the green start marker (click the ruler); if the same notes are already there, it pastes right after them.
- ↑ / ↓ move the selected notes up and down a semitone; with Shift, an octave.

### Pitch editing

The “Pitch” bar below the piano roll draws the current track's pitch curve (±300 cents, relative to the note): left button = brush, right button = eraser, “Clear” wipes it all, Ctrl+Z undoes. The curve is saved in the project. It works with the PSOLA engine (added to portamento and vibrato) and with the external resampler (sent as UTAU pitch bend).

## Synthesis engine (Ctrl+E)

Audio is generated in two steps that can be swapped at any time (they are saved in the `.chrproject`).

**Phonemizer**: turns each note's lyric into voicebank samples.
- *CV (romaji ↔ kana)*: one sample per note; accepts “ka”, “か”, “カ” and variants (shi/si, chi/ti…).
- *Direct*: alias = the lyric as typed.
- *VCV*: “a ka” (previous vowel + CV), “- ka” at the start of a phrase.
- *CVVC*: CV + a VC sample (“a k”) before the next consonant; “a R”/“a -” at the end.
- Alias prefix/suffix for multi-pitch banks (e.g. “ A3”).

**Resampler**: generates the audio. The default is **PSOLA by phrases** (built-in engine), still experimental and unstable.
- *PSOLA by phrases* (experimental): uses real periods from the recording (TD-PSOLA). Connected notes share the same pitch curve and marks, with continuous portamento, in-phase crossfade, optional vibrato and “humanization”. *Match volume between samples* (0–1, default 0.7) avoids level jumps between samples recorded at different intensities. Long vowels are stretched by sweeping forwards and backwards through the middle of the sample.
- *PSOLA note by note* (experimental): classic mode with audio crossfade.
- *External (UTAU-compatible)*: calls an `.exe` using the UTAU protocol for each note. **The program does not include one**: give the path to yours in *Synthesis engine*, or put a `resampler.exe` in the `resampler/` folder. It has no pitch curves (the program's portamento and vibrato do not apply). Windows only (uses “wine” on Linux/macOS).
- Old projects (WORLD engine) open normally and switch to the equivalent PSOLA mode.
- PSOLA gives the best result when the requested pitch is close to the pitch the sample was recorded at (up to about ±5 semitones); for very different pitches use multi-pitch samples (alias suffix).

To add your own phonemizer or resampler, create a class in `core/phonemizers.py` or `core/resamplers.py` and register it in `PHONEMIZERS` / `RESAMPLERS`: it appears automatically in the tab.

## UTAU voicebank (folder)

`wavs` + `config.ini` (or `oto.ini`). Lines in UTAU format:

```
file.wav=alias,offset,consonant,cutoff,preutterance,overlap
```

Optional metadata at the top:

```
[Voicebank]
name=Name
author=Author
description=Text
```

`character.txt` (`name=`) and `image.png` / `icon.png` (portrait) are also read. Accepted encodings: UTF-8, Shift-JIS, CP1252.

**Cutoff convention:** as in UTAU, `cutoff > 0` = distance (ms) from the **end** of the wav; `cutoff < 0` = **length** (ms) of the useful zone from the offset; `0` = until the end. With the external resampler, the consonant always uses the oto value and, when the previous note is short, the shortening is done through *velocity* (as in UTAU).

## DiffSinger (experimental)

Import a DiffSinger folder in the OpenUtau format (with `dsconfig.yaml`, `phonemes.txt/json`, `acoustic.onnx` and, optionally, `dsdict.yaml`) in *Singers → Import folder*. The program recognises it as “DiffSinger (ONNX)” and, on tracks with that singer, ignores the UTAU phonemizer and resampler. The pipeline is: lyrics → phonemes (**Japanese** phonemizer: dsdict, hiragana/katakana/romaji, ん, っ, ー = sustain, R = rest) → durations → f0 (note + portamento + vibrato + drawn pitch curve) → acoustic model → NSF-HiFiGAN vocoder (ONNX).

- **Vocoder:** it must have the **same name** the voicebank asks for in `dsconfig.yaml` (`vocoder:`); each voicebank only sounds right with the vocoder it was trained with. `nsf_hifigan` is used only when it is missing. It is searched in `<voicebank>/dsvocoder/<name>`, `<voicebank>/<name>`, the folder next to it, or `~/.pip_synth/vocoders/<name>` (needs a `vocoder.yaml` or `config.json` with sample_rate/hop_size).
- **GPU:** to speed it up, install `onnxruntime-directml` instead of `onnxruntime`.
- **Options** (`engine`, Engine tab): `ds_steps` (20) and `ds_speedup` (10).
- **Diagnostics:** `python tools/diagnose_diffsinger.py "folder" "lyric1" "lyric2"` shows the vocoder in use, the models' inputs and outputs, and how each phoneme is classified (C = consonant, V = vowel).

### Variance models (experimental)

If the voicebank has `dsdur/`, `dspitch/` and/or `dsvariance/` folders (each with `dsconfig.yaml`, `linguistic.onnx` and `dur.onnx` / `pitch.onnx` / `variance.onnx`), the app uses them before the acoustic model:

- **Duration** (`dsdur`): decides how long the leading consonants last and how the body of the syllable is split. The vowel still starts at the beginning of the note; consonants have a maximum length.
- **Pitch** (`dspitch`): replaces the base curve (note + portamento) with an expressive one; vibrato and the drawn curve are added on top.
- **Parameters** (`dsvariance`): predicts energy, breathiness, voicing and tension, which are passed to the acoustic model if it has those inputs.

The Engine tab has a master switch (`ds_variance`; off = behaviour without variance) and one per model (`ds_var_dur`, `ds_var_pitch`, `ds_var_params`), all on by default, plus pitch expressiveness (`ds_pitch_expr`, 100 %). Each model uses its own `phonemes` and speaker embeddings. If a model fails (missing phoneme, unknown input, wrong output size), synthesis carries on without it and the reason is logged to `~/.pip_synth/diffsinger.log`.

### Chunked and background rendering

- **By phrase:** DiffSinger renders one phrase at a time (split at rests ≥ 0.6 s; phrases longer than ~14 s are cut at the first short rest). Each phrase is cached as soon as it is ready, with a key that includes phonemes, durations, f0, parameters, models, steps/speedup, speaker and language. Only **changed** phrases are calculated again, and identical phrases (a repeated chorus) are calculated once.
- **Play from the middle:** when playing from a bar, phrases that end before that point are not rendered.
- **Automatic:** 1.5 s after you stop editing, the program fills the caches by itself, at low priority and starting with what is ahead of the cursor. If you edit again, outdated work is cancelled at the end of the current phrase/note. Progress shows in the status bar and background errors never open dialogs. It can be turned off in the Engine tab (“Render automatically in the background”); it needs the cache on.

## Cache and speed

Each phrase (DiffSinger) or note (external resampler) is stored in `~/.pip_synth/cache`, so on play only what changed is rendered. The key includes the engine, the source wav, pitch, duration, oto, flags and tempo. With the external resampler, notes render in parallel (one process per core, up to 8). Encrypted voicebanks (`.chrvoice`) never use the on-disk cache. 1 GB limit (least recently used is deleted). Under *Edit* and *Synthesis engine* there are “Open cache folder” and “Clear cache”.

## Formats

**`.chrvoice`**: folder → zip → AES-256-GCM (key via scrypt). The header (name/author/description) stays in clear text but authenticated; the content is decrypted in memory only (there is no option to decrypt to a folder). With a password it is secure; without one a built-in key is used (obfuscation only).

**`.chrproject`**: JSON with `tempo`, `beats_per_bar`, `singer_name`, `singer_path` and `notes` (`start`/`length` in beats, MIDI `pitch`, `lyric`), plus the engine options and the pitch curve.

## Tools

```
python tools/diagnose_voicebank.py "voicebank_folder"   # samples: voice/pitch detected per alias
python tools/diagnose_diffsinger.py "folder" "lyric"     # DiffSinger: vocoder, models, phonemes
python tools/selftest.py                                 # synthesizes a test voicebank and checks the pitch
python tools/ustx_to_chrproject.py project.ustx          # converts an OpenUtau project
python tools/make_demo_voicebank.py demo_voicebank       # test voicebank (a e i o u)
```

## Limitations

- **The interface's English language does not work yet.**
- **VOCALOID** voicebanks are not supported (they are proprietary and encrypted).
- DiffSinger currently has only a Japanese phonemizer and is experimental.
- The PSOLA engine is experimental and may be unstable.
- No voicebank or resampler is included: use your own and **respect each one's license**.

## Contributing

Issues and pull requests are welcome. Before opening a PR, run `python tools/selftest.py`.

## License

To be defined by the author.
