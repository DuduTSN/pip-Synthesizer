# pip!Synthesizer

**[English](#english)** · **[Português (PT-PT)](#português-pt-pt)**

> Created by **Dudu** (UniverStars; BETWEEN WORLDS) · v0.5

---

# English

A singing voice synthesizer built with Python for Windows.

## Features

- **Multi-track editing**: Dedicated tracks with individual singer assignment, mute/solo switches, volume, panning, and stereo mixing.
- **Piano roll**: Intuitive brush and selection tools, cross-track copy/paste, and configurable keyboard shortcuts.
- **Pitch curve editing**: Dedicated "Pitch" lane below the piano roll to draw precise pitch curves ($\pm300$ cents relative to notes).
- **UTAU voicebank support**: Full compatibility with UTAU folder structures (`oto.ini`), utilizing an internal PSOLA engine or custom external resamplers.
- **DiffSinger support (experimental)**: OpenUtau-formatted ONNX models featuring the NSF-HiFiGAN vocoder, Japanese phonemizers, and variance control models.
- **Encrypted voicebanks**: Support for encrypted `.chrvoice` packages decrypted securely in memory.
- **Import & conversion**: Native import for `.mid` and `.ust` files, with built-in converter utilities for OpenUtau (`.ustx`) project files.
- **Incremental background rendering**: Smart phrase-level caching that only re-renders modified segments.
- **Customization**: Multiple visual themes (Night, Light, Sakura, Cyan, Classic), update notifications, and full transport status readouts.

## Requirements

- **Operating System**: Windows (Linux/macOS supported via Wine for external resamplers).
- **Runtime**: [Python 3.10+](https://www.python.org/downloads/) installed and accessible via system path.
- **Diagnostics**: Error logs are generated automatically at `%USERPROFILE%\.pip_synth\crash.log`.

## Quick Start

1. Open **Singers** $\rightarrow$ Import your voicebank folder or `.chrvoice` file.
2. Click **Set as default singer**.
3. Create a **New Project** and use the **Brush tool** ($B$) to draw notes on the piano roll grid.
4. Double-click any note to enter lyrics (e.g., romaji or kana).
5. Press **Space** to trigger synthesis and playback.

## User Interface & Workflow

- **Main Menu (`Ctrl+M`)**: Access Home, Project Management, Singer Management, and Application Settings.
- **Editor & Transport**: LCD transport header displaying time, bar counts, BPM, time signature, snap grid settings, and active singer portrait.
- **File Management**:
  - `Ctrl+O`: Open project files (`.chrproject`), MIDI (`.mid`/`.midi`), or UTAU projects (`.ust`).
  - `Ctrl+I`: Import MIDI/UST tracks directly into the active session.
  - Drag-and-drop support for fast file loading.

### Shortcuts Reference

| Action | Shortcut |
| :--- | :--- |
| **Play / Stop** | `Space` |
| **New / Open / Save** | `Ctrl+N` / `Ctrl+O` / `Ctrl+S` |
| **Export Audio (WAV)** | `Ctrl+Shift+E` |
| **Add Track / Properties**| `Ctrl+T` / `F2` |
| **Engine Settings** | `Ctrl+E` |
| **Brush / Select Tool** | `B` / `V` |
| **Transpose Octave Up/Down** | `Shift+↑` / `Shift+↓` |

---

## Synthesis Engine (`Ctrl+E`)

The synthesis pipeline operates in two main stages:

1. **Phonemizer**: Converts note text into targeted voicebank acoustic samples.
   - **CV**: Standard consonant-vowel mappings (accepts romaji and kana).
   - **VCV / CVVC**: Advanced diphones/triphones for smooth transitions.
   - **Direct**: Uses exact sample aliases as written.
2. **Resampler**: Generates output waveform audio.
   - **PSOLA (Phrase Mode)**: Continuous pitch curves, automatic phase alignment, and intensity matching across samples.
   - **External Resampler**: Invokes external UTAU-compatible binaries (`resampler.exe`).

---

## DiffSinger Architecture (Experimental)

DiffSinger projects utilize ONNX acoustic models coupled with the **NSF-HiFiGAN** vocoder.

- **Variance Models**: Optional sub-models for explicit duration control (`dsdur`), expressive pitch generation (`dspitch`), and expressive parameter prediction (`dsvariance` for breathiness, energy, and tension).
- **Background Caching**: Phrases separated by pauses ($\ge 0.6\text{s}$) are processed in low-priority background threads to keep playback responsive.

---

# Português (PT-PT)

Um sintetizador de voz cantada desenvolvido em Python para Windows.

## Funcionalidades

- **Edição multipista**: Pistas dedicadas com atribuição individual de cantor, controlos de silenciamento (*mute*)/solo, volume, panorâmica e mistura estéreo.
- **Piano roll**: Ferramentas intuitivas de pincel e seleção, copiar/colar entre pistas e atalhos de teclado configuráveis.
- **Edição de curva de afinação**: Painel de afinação (*Pitch*) sob o *piano roll* para desenhar curvas de afinação personalizadas ($\pm300$ cêntimos em relação à nota).
- **Suporte a voicebanks UTAU**: Compatibilidade total com a estrutura de pastas UTAU (`oto.ini`), utilizando o motor PSOLA interno ou *resamplers* externos.
- **Suporte a DiffSinger (experimental)**: Modelos ONNX no formato OpenUtau com vocoder NSF-HiFiGAN, *phonemizers* de japonês e modelos de variação expressiva.
- **Voicebanks encriptados**: Suporte a pacotes `.chrvoice` encriptados, descodificados de forma segura diretamente na memória RAM.
- **Importação e conversão**: Importação nativa de ficheiros `.mid` e `.ust`, com utilitários de conversão integrados para projetos OpenUtau (`.ustx`).
- **Renderização incremental em segundo plano**: Sistema de *cache* inteligente ao nível da frase que apenas sintetiza os trechos modificados.
- **Personalização**: Diversos temas visuais (Noite, Claro, Sakura, Ciano, Clássico), janelas de atualizações e leitura completa do estado de transporte.

## Requisitos do Sistema

- **Sistema Operativo**: Windows (Linux/macOS suportados via Wine para a utilização de *resamplers* externos).
- **Ambiente de Execução**: [Python 3.10+](https://www.python.org/downloads/) instalado e configurado nas variáveis de ambiente.
- **Diagnósticos**: Os registos de erro são guardados automaticamente em `%USERPROFILE%\.pip_synth\crash.log`.

## Guia de Início Rápido

1. Aceda a **Cantores** $\rightarrow$ Importar pasta de *voicebank* ou ficheiro `.chrvoice`.
2. Clique em **Definir como cantor predefinido**.
3. Crie um **Novo Projeto** e utilize a ferramenta **Pincel** ($B$) para desenhar notas na grelha do *piano roll*.
4. Dê um duplo clique em qualquer nota para introduzir a letra da música (ex.: *romaji* ou *kana*).
5. Pressione a barra de **Espaço** para iniciar a síntese e reprodução de áudio.

## Interface e Fluxo de Trabalho

- **Menu Principal (`Ctrl+M`)**: Acesso rápido ao início, gestão de projetos, gestão de cantores e definições da aplicação.
- **Editor e Transporte**: Barra superior com mostrador LCD com tempo decorrido, contagem de compassos, BPM, fórmula de compasso, grelha de alinhamento e foto do cantor ativo.
- **Gestão de Ficheiros**:
  - `Ctrl+O`: Abrir ficheiros de projeto (`.chrproject`), MIDI (`.mid`/`.midi`) ou UTAU (`.ust`).
  - `Ctrl+I`: Importar pistas MIDI/UST diretamente para a sessão atual.
  - Suporte para arrastar e largar ficheiros diretamente na janela.

### Tabela de Atalhos

| Ação | Atalho |
| :--- | :--- |
| **Reproduzir / Parar** | `Espaço` |
| **Novo / Abrir / Guardar** | `Ctrl+N` / `Ctrl+O` / `Ctrl+S` |
| **Exportar Áudio (WAV)** | `Ctrl+Shift+E` |
| **Adicionar Pista / Propriedades**| `Ctrl+T` / `F2` |
| **Definições do Motor** | `Ctrl+E` |
| **Pincel / Ferramenta de Seleção** | `B` / `V` |
| **Transpor Oitava Acima/Abaixo** | `Shift+↑` / `Shift+↓` |

---

## Motor de Síntese (`Ctrl+E`)

O processo de síntese divide-se em duas etapas principais:

1. **Phonemizer**: Converte o texto das notas em amostras fonéticas do *voicebank*.
   - **CV**: Mapeamento básico consoante-vogal (aceita *romaji* e *kana*).
   - **VCV / CVVC**: Difones e trifones avançados para transições mais suaves.
   - **Direto**: Utiliza exatamente o nome dos *aliases* registados.
2. **Resampler**: Gera a forma de onda de áudio final.
   - **PSOLA (Modo Frase)**: Curvas de afinação contínuas, alinhamento automático de fase e equalização de intensidade entre amostras.
   - **Resampler Externo**: Executa binários externos compatíveis com UTAU (`resampler.exe`).

---

## Arquitetura DiffSinger (Experimental)

Os projetos DiffSinger empregam modelos acústicos ONNX juntamente com o vocoder **NSF-HiFiGAN**.

- **Modelos de Variação**: Submodelos opcionais para controlo explícito de duração (`dsdur`), geração de curvas de afinação expressivas (`dspitch`) e previsão de parâmetros dinâmicos (`dsvariance` para aspereza, energia e tensão vocal).
- **Cache em Segundo Plano**: As frases separadas por pausas ($\ge 0,6\text{s}$) são processadas em segundo plano com baixa prioridade para manter a interface fluida.


## License

This project's license is to be defined by the author.
