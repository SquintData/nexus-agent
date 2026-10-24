# Nexus Agent

Agente local de voz do Nexus para Windows. Conecta uma conta do painel Nexus ao microfone, à saída de áudio e às ações disponíveis no computador.

Este repositório contém o agente e seus scripts de instalação. A aplicação web e o backend estão no [nexus-project](https://github.com/SquintData/nexus-project).

## Como funciona

1. Detecta localmente a palavra de ativação com Vosk.
2. Captura o comando de voz.
3. Usa proxies autenticados do backend para transcrição, interpretação e síntese de voz.
4. Executa as ferramentas disponíveis e responde por áudio.

A detecção de ativação é local; as etapas de IA dependem de conexão com o backend e com os provedores.

## Requisitos

- Windows 10 ou superior.
- Python 3.11 ou 3.12 disponível no PATH.
- Microfone e saída de áudio.
- Conta Nexus com acesso ao recurso de pareamento.

## Instalação

Baixe ou clone o repositório e abra um terminal na raiz.

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m agent.setup_models
```

Também há um instalador interativo em `setup.bat`. Leia o script antes de executá-lo, especialmente se já existir um ambiente virtual na pasta.

## Pareamento e uso

1. No painel Nexus, entre na conta e abra **Parear agente**.
2. Gere um código e inicie o agente:

```powershell
.\.venv\Scripts\python.exe -m agent.main
```

3. Cole o código quando solicitado.
4. Diga **“Olá Nexus”** e faça o pedido.

O pareamento salva as credenciais de sessão em um `.env` local. Não envie esse arquivo para o GitHub.

## Estrutura

```text
agent/voice/       Captura, transcrição, síntese e detecção de voz
agent/llm/         Orquestração e definição das ferramentas
agent/tools/       Execução das ferramentas
agent/desktop/     Automação local
agent/db/          Comunicação com o backend
setup.bat          Instalação interativa
run.bat            Inicialização
```

## Configuração

[agent/config.py](agent/config.py) lê a configuração do `.env` na raiz. Os valores padrão apontam para o backend Nexus; para outro ambiente, configure `SUPABASE_URL` e `SUPABASE_ANON_KEY`.

As chaves dos provedores de IA ficam nas funções do backend. O agente usa a autenticação do usuário para acessar esses proxies.

A lista de aplicativos permitidos está em [agent/config.json](agent/config.json). Os caminhos precisam corresponder aos aplicativos instalados na máquina.

## Diagnóstico e validação

- **Python não encontrado:** confira o PATH e a instalação do Python.
- **Sem áudio:** confira os dispositivos padrão de entrada e saída do Windows.
- **Código inválido ou expirado:** gere outro código no painel.
- **Falha de autenticação:** repita o pareamento e confira a disponibilidade do backend.

Não há suíte automatizada de testes neste repositório. A instalação, o pareamento, a voz e a automação devem ser validados no Windows com o backend configurado.

O agente deste repositório e o diretório `agent/` do projeto principal têm diferenças; não presuma equivalência de versões.
