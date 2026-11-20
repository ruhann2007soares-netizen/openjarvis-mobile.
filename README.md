# OpenJarvis Mobile — primeira versão PWA

Interface Android instalável para conectar a um servidor OpenJarvis existente.

## O que já funciona nesta primeira entrega
- Interface responsiva em português, com navegação móvel.
- PWA instalável e cache básico para abrir a interface offline.
- Chat usando `POST /v1/chat/completions` do OpenJarvis.
- Configuração do endereço, token e modelo do servidor.
- Entrada de voz pelo reconhecimento de fala do navegador (quando suportado).
- Saída por voz pode ser usada pelo leitor/acessibilidade do Android; TTS integrado será uma próxima etapa.
- Histórico de conversa durante a sessão.
- Notas locais simples e anexação de TXT, MD, CSV, JSON e LOG ao próximo prompt.

## O que ainda depende de integração
- Memória nativa remota: endpoints `/v1/memory` e políticas do servidor.
- Agentes: endpoints `/v1/agents`, permissões e confirmação de ações.
- Pesquisa aprofundada: agente `deep_research` e ferramentas web habilitadas.
- Automações: scheduler do servidor, criação/listagem/pausa/cancelamento.
- PDFs e Office: extração de texto e envio para indexação.
- Streaming e eventos de agente por WebSocket.
- Login multiusuário e armazenamento seguro de credenciais.

## Requisitos do servidor
O OpenJarvis original oferece API compatível com OpenAI. Em um computador/servidor:
```bash
git clone https://github.com/open-jarvis/OpenJarvis.git
cd OpenJarvis
uv sync --extra server
uv run jarvis serve --host 0.0.0.0 --port 8000 --agent orchestrator
```
Configure autenticação (`OPENJARVIS_API_KEY` ou `[server.auth].api_key`) antes de expor o serviço. Para acesso remoto, use HTTPS/WSS e firewall. Não exponha Ollama diretamente à internet.

Atenção: `0.0.0.0` sem autenticação e HTTPS não é seguro. A documentação oficial recomenda configurar autenticação antes de permitir acesso pela rede.

## Testar
Abra `index.html` com um servidor estático local ou publique os arquivos em hospedagem HTTPS. Para instalação PWA, o site precisa estar em HTTPS (ou localhost).

No Android:
1. Abra o endereço publicado no Chrome.
2. Abra o menu ⋮.
3. Escolha **Instalar app** ou **Adicionar à tela inicial**.
4. Abra Configurações dentro do Jarvis e informe a URL HTTPS da API e a chave, se configurada.

## Limites conhecidos
A hospedagem estática serve apenas a interface. O motor OpenJarvis e os modelos precisam continuar rodando em um computador ou servidor compatível. O processamento local diretamente no Android não está implementado nesta versão.
