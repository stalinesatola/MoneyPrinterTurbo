<div align="center">

# MoneyPrinterTurbo 💸

### Gerador de vídeos curtos com IA, tudo-em-um

Dá um **tema** ou uma **palavra-chave** e o MoneyPrinterTurbo gera o guião, escolhe as imagens/clips,
cria as legendas e a música de fundo, e produz um vídeo curto em HD.

[Português](README.md) | [English](README-en.md) | [简体中文](README-zh.md) | [日本語](README-ja.md) | [Releases](https://github.com/harry0703/MoneyPrinterTurbo/releases) | [Issues](https://github.com/harry0703/MoneyPrinterTurbo/issues)

</div>

> Tradução para português da documentação do projeto original
> [`harry0703/MoneyPrinterTurbo`](https://github.com/harry0703/MoneyPrinterTurbo).
> Este repositório é um fork. Para descarregar os pacotes e as *releases* oficiais usa sempre o repositório original.

---

## Capturas de ecrã 🖥️

<h4 align="center">WebUI</h4>

![](docs/webui-en.jpg)

<h4 align="center">API</h4>

![](docs/api.jpg)

---

## O que faz 🎯

### Fluxos de criação

- Cria vídeos por **Agente de IA, WebUI, API ou CLI** — para experimentação rápida ou produção automatizada
- Do tema ao guião, locução, imagens, legendas, música e montagem de forma automática, mantendo o controlo de cada etapa
- Geração de várias variantes em lote, histórico de tarefas, e importação/exportação das definições e chaves de API

### Guiões e modelos de IA

- Gera ou reescreve **guiões multilingues** com IA, ou fornece um guião completo à mão
- Suporta os principais fornecedores: Kimi / Moonshot, OpenAI, Anthropic Claude, Google Gemini, DeepSeek,
  Alibaba Qwen, Azure OpenAI, ByteDance VolcEngine Ark, xAI Grok, MiniMax, Xiaomi MiMo
- Liga-se também através de *gateways* compatíveis com OpenAI: OpenRouter, Ollama (local), OneAPI,
  LiteLLM, Groq, Cloudflare AI Gateway, ModelScope, entre outros

### Imagens e clips de vídeo

- Carrega **imagens e vídeos locais**, ou usa banco de imagens HD grátis do
  [Pexels](https://www.pexels.com/api/), [Pixabay](https://pixabay.com/api/docs/) e [Coverr](https://coverr.co/developers)
- Geração de clips por IA (texto→vídeo): Metaso MiniMax H3 (`768P`/`2K`), VolcEngine Ark Seedance,
  OFox, WaveSpeed AI, ou serviços de texto→imagem compatíveis com OpenAI convertidos em clips animados
- Ajuste da duração de cada clip, modo de enquadramento (`cover`/`contain`) e ordem dos materiais

### Locução, legendas e música

- Locução automática, áudio carregado por ti, ou sem locução
- TTS: **Edge TTS (grátis, sem chave de API)**, Azure Speech, SiliconFlow, Google Gemini,
  Xiaomi MiMo, MiniMax, ElevenLabs, Chatterbox (self-hosted), Fish Audio
- Legendas por *timestamps* do TTS (`edge`) ou por transcrição local `faster-whisper` (`whisper`),
  com controlo de tipo de letra, posição, cor, tamanho, contorno e fundo
- Música de fundo aleatória, local ou gerada por IA, com volume independente

### Saída e publicação

- Formatos: vertical `9:16 (1080×1920)`, horizontal `16:9 (1920×1080)`, quadrado `1:1 (1080×1080)`
- Publicação direta para **TikTok, Instagram e YouTube Shorts**

---

## Requisitos de sistema 📦

- Plataformas recomendadas: Windows 10+, macOS 11+, ou uma distribuição Linux mainstream
- Instalação local requer **Python 3.11 ou superior** (3.11 recomendado)
- GPU não é obrigatória, mas ajuda em transcrição local, processamento de vídeo e geração em lote

| Item | Mínimo        | Recomendado   | Ótimo       |
| ---- | ------------- | ------------- | ----------- |
| CPU  | 4 núcleos     | 6 a 8 núcleos | 8+ núcleos  |
| RAM  | 4 GB          | 8 GB          | 16+ GB      |
| GPU  | Não requerida | 4+ GB VRAM    | 8+ GB VRAM  |

Se dependes sobretudo de LLM/TTS na *cloud* e bancos de imagem online, CPU e RAM pesam mais que a GPU.
Se usas `faster-whisper` ou geração em lote, a GPU melhora bastante o débito.

---

## Começar rápido 🚀

### Caminhos recomendados

- Não queres instalar nada: gera vídeos com um **Agente de IA** (ver abaixo)
- **Windows**: usa o pacote *one-click* das *releases* para o teste local mais rápido
- **macOS / Linux**: usa `uv` como caminho principal de instalação local
- Ambiente isolado: usa **Docker**

### Gerar vídeos com um Agente de IA

Se o teu agente consegue ler *Skills* e usar um terminal local, envia-lhe:

```text
Usa esta Skill: https://raw.githubusercontent.com/harry0703/MoneyPrinterTurbo/main/docs/skill/SKILL.md
Cria um vídeo com o tema "Como a IA está a mudar o dia a dia".
```

O agente instala, configura, gera o vídeo e devolve o caminho do ficheiro. Só pede as chaves de API em falta.

### Google Colab

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/harry0703/MoneyPrinterTurbo/blob/main/docs/MoneyPrinterTurbo.ipynb)

### Windows (pacote one-click)

Descarrega o pacote mais recente das
[Releases](https://github.com/harry0703/MoneyPrinterTurbo/releases/latest) e extrai-o.
Executa primeiro `update.bat` (atualiza o código) e depois `start.bat`. O browser abre sozinho
(usa Chrome ou Edge se abrir em branco).

---

## Instalação e execução 📥

> No Windows, evita caminhos com acentos, carateres especiais ou espaços.

### 1. Clonar o projeto

```bash
git clone https://github.com/stalinesatola/MoneyPrinterTurbo.git
cd MoneyPrinterTurbo
```

Na primeira execução, o `config.toml` é criado a partir de `config.example.toml` — não precisas de o criar à mão.
As chaves de API para LLM na *cloud*, imagens online e vídeo por IA adicionam-se nas definições da WebUI.

### 2a. Ambiente Python com `uv` (recomendado)

```bash
uv python install 3.11
uv sync --frozen
```

### 2b. Ou com `venv` + `pip`

```bash
python3.11 -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

- `pyproject.toml` é o manifesto principal de dependências; `uv.lock` fixa as versões resolvidas.
- `requirements.txt` mantém-se apenas para a instalação legada com `pip`.

### 3. Arrancar a WebUI 🌐

Executa a partir da **raiz** do projeto:

```bash
# Windows
.\webui.bat

# macOS / Linux
sh webui.sh
```

Para permitir acesso de outros dispositivos na rede local, define `MPT_WEBUI_HOST=0.0.0.0` antes de arrancar.
Depois de arrancar o browser abre automaticamente (por omissão em http://127.0.0.1:8501).

### 4. Arrancar o serviço de API 🚀

```bash
uv run python main.py     # ou: python main.py
```

- Documentação da API: http://127.0.0.1:8080/docs ou http://127.0.0.1:8080/redoc
- CORS: o acesso do browser da mesma origem está ativo por omissão. Define `CORS_ALLOWED_ORIGINS`
  (ex. `http://localhost:3000,https://frontend.example.com`) só se um frontend web separado precisar
  de chamar a API a partir de outra origem. Não afeta curl, Postman, n8n ou clientes server-side.
- Autenticação: define `app.api_key` no `config.toml` para proteger `/api/v1` e `/tasks`.

### 5. Modo CLI puro (sem browser) ⌨️

```bash
uv run python cli.py --video-subject "Como a IA está a mudar o dia a dia"
uv run python cli.py --help      # referência completa de parâmetros
```

Estilo de legenda e opções de locução resolvem-se por esta ordem:
**opção explícita no CLI > valor `[ui]` guardado no `config.toml` > valor por omissão**.

Execução de várias tarefas em sequência (array JSON UTF-8 ou manifesto JSONL, máx. 100 tarefas / 1 MiB):

```json
[
  { "video_subject": "Como funcionam os painéis solares" },
  { "video_subject": "Como funcionam as turbinas eólicas", "video_aspect": "16:9" }
]
```

```bash
uv run python cli.py --batch-file ./tasks.json --stop-at video
```

Todas as entradas são validadas antes de a primeira tarefa arrancar; a execução continua após falha
individual; no fim é impresso um resumo JSON (`total`, `succeeded`, `failed`, `tasks`).

### Docker 🐳

```bash
cd MoneyPrinterTurbo
cp config.example.toml config.toml     # necessário antes do primeiro arranque
docker compose -f docker-compose.release.yml up
```

- WebUI: http://127.0.0.1:8501 · API: http://127.0.0.1:8080/docs
- `docker-compose.release.yml` puxa a imagem pré-construída de `ghcr.io/harry0703/moneyprinterturbo:latest`.
  Para construir localmente, usa `docker compose up`.

---

## Locução, legendas e música 🎙️

### Síntese de voz

O **Azure TTS V1** na WebUI usa o **Edge TTS** — grátis e sem chave de API. Suporta ainda Azure TTS V2,
SiliconFlow, Google Gemini TTS, Xiaomi MiMo TTS, ElevenLabs, Chatterbox (self-hosted), Fish Audio, e modo sem voz.
Lista de vozes Edge TTS em [`docs/voice-list.txt`](./docs/voice-list.txt).

### Legendas

- **`edge`** (por omissão): usa os *timestamps* do TTS, rápido, sem GPU.
- **`whisper`**: transcrição local `faster-whisper` quando precisas de maior precisão. O modelo é descarregado no primeiro uso.

```toml
[app]
subtitle_provider = "whisper"

[whisper]
model_size = "large-v3-turbo"   # ~1.6 GB, mais rápido que o large-v3 (~3 GB)
```

Se o download automático do Hugging Face falhar, descarrega o
[`whisper-large-v3`](https://huggingface.co/Systran/faster-whisper-large-v3) manualmente e coloca a pasta
em `./MoneyPrinterTurbo/models/whisper-large-v3`.

### Música e tipos de letra

- Música de fundo em `resource/songs`
- Tipos de letra das legendas em `resource/fonts` (podes adicionar os teus)

---

## Perguntas frequentes 🤔

<details>
<summary>RuntimeError: No ffmpeg exe could be found</summary>

Normalmente o ffmpeg é descarregado e detetado automaticamente. Se o ambiente impedir o download,
descarrega o FFmpeg de [gyan.dev](https://www.gyan.dev/ffmpeg/builds/) e define no `config.toml`:

```toml
[app]
# separadores de caminho no Windows são \\
ffmpeg_path = "C:\\Users\\utilizador\\Downloads\\ffmpeg.exe"
```

</details>

<details>
<summary>OSError: [Errno 24] Too many open files</summary>

Limite do sistema para ficheiros abertos. Verifica com `ulimit -n` e aumenta, ex. `ulimit -n 10240`.

</details>

<details>
<summary>Falha no download do modelo Whisper</summary>

Descarrega o modelo manualmente do Hugging Face (ver secção **Legendas** acima).

</details>

---

## Arquitetura do código 🧱

```
MoneyPrinterTurbo/
├── main.py                  # Arranque do serviço de API (uvicorn → app.asgi:app)
├── cli.py                   # Interface de linha de comandos (tarefa única + lote)
├── webui/Main.py            # Interface Streamlit (i18n em webui/i18n/*.json, inclui pt.json)
├── config.example.toml      # Modelo de configuração; copiado para config.toml no 1.º arranque
│
├── app/
│   ├── asgi.py              # App FastAPI: CORS, handlers de exceção, lifespan
│   ├── router.py            # Agregação das rotas v1
│   ├── config/config.py     # Carregamento/gravação de config com lock partilhado (WebUI vs. tarefas)
│   ├── models/
│   │   ├── schema.py        # VideoParams e enums (VideoAspect, ConcatMode, TransitionMode, ...)
│   │   └── const.py         # Estados de tarefa e de publicação
│   ├── controllers/
│   │   ├── v1/video.py      # /videos /subtitle /audio /tasks, upload de BGM/materiais, stream/download
│   │   ├── v1/llm.py        # Endpoints de guião/termos
│   │   └── manager/         # Filas de tarefas: em memória ou Redis
│   ├── services/
│   │   ├── task.py          # Orquestrador do pipeline (_run_pipeline) — partilhado por API/CLI/WebUI
│   │   ├── llm.py           # Geração de guião e de termos de pesquisa (litellm/openai/gemini)
│   │   ├── voice.py         # TTS (Edge, Azure, SiliconFlow, Gemini, MiMo, MiniMax, ElevenLabs, ...)
│   │   ├── subtitle.py      # Legendas via edge / faster-whisper
│   │   ├── material.py      # Pesquisa/descarga de imagens (Pexels, Pixabay, Coverr, openai_image)
│   │   ├── video.py         # Montagem final com moviepy (concat, transições, legendas, BGM)
│   │   ├── bgm.py           # Seleção de música de fundo
│   │   ├── sonilo.py / elevenlabs_music.py   # Música por IA
│   │   ├── metaso_minimax.py / ofox.py / volcengine_seedance.py   # Vídeo por IA (texto→vídeo)
│   │   ├── upload_post.py   # Publicação em TikTok / Instagram / YouTube
│   │   ├── state.py         # Estado das tarefas (memória / Redis)
│   │   └── material_cache.py / cache_manager.py   # Cache em disco dos materiais online
│   └── utils/
│       ├── utils.py             # Helpers gerais + verificação do FFmpeg
│       └── file_security.py     # Leitura/escrita segura dentro do diretório da tarefa
│
├── resource/{songs,fonts}   # Música e tipos de letra incluídos
├── test/services/           # Testes (pytest) — cobrem serviços, controllers, CLI e WebUI
└── docs/skill/SKILL.md      # Skill para agentes de IA
```

### O pipeline de geração (`app/services/task.py::_run_pipeline`)

1. **Preflight** — valida chaves de API do fornecedor de vídeo/música escolhido e a disponibilidade do FFmpeg
   (o mesmo ponto de entrada é usado por API, CLI e WebUI, para comportamento consistente).
2. **Guião** (`generate_script`) — LLM redige o guião a partir do tema (ou usa o guião fornecido).
3. **Termos** (`generate_terms`) — LLM extrai palavras-chave de pesquisa (ignorado se `video_source = local`).
4. **Áudio** (`generate_audio`) — TTS gera a locução; ou usa o áudio carregado; ou nenhum.
5. **Legendas** (`generate_subtitle`) — `edge` (timestamps do TTS) ou `whisper` (transcrição local).
6. **Materiais** (`get_video_materials`) — descarrega/gera os clips e imagens.
7. **Vídeo** (`generate_final_videos`) — moviepy junta tudo: montagem, transições, legendas, música.
8. **Publicação** (opcional) — `upload_post` envia para as redes sociais (num *thread pool* dedicado).

`--stop-at {script,terms,audio,subtitle,materials,video}` permite parar o pipeline num estágio intermédio.

### Configuração (`config.toml`)

Secções: `[app]` (chaves LLM, provedores, FFmpeg, autenticação da API, proxies), `[whisper]`,
`[proxy]`, `[azure]`, `[siliconflow]`, `[minimax_tts]`, `[elevenlabs]`, `[chatterbox]`, `[fish_audio]`, `[ui]`
(valores memorizados da WebUI). A WebUI e as tarefas partilham um *lock* de escrita para não trocar de
fornecedor/chave a meio de uma geração.

### Stack

Python 3.11+ · FastAPI + Uvicorn (API) · Streamlit (WebUI) · moviepy 2.x (vídeo) · edge-tts · faster-whisper ·
litellm / openai / google-genai (LLM) · Redis (fila de tarefas, opcional) · pytest + ruff (dev).

---

## Sugestões e problemas 📢

Abre um [issue](https://github.com/harry0703/MoneyPrinterTurbo/issues) ou um
[pull request](https://github.com/harry0703/MoneyPrinterTurbo/pulls) no projeto original.

## Licença 📝

Ver o ficheiro [`LICENSE`](LICENSE) (MIT).
