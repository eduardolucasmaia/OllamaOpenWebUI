# Ollama com Open WebUI e modelo DeepSeek-R1

Este repositório contém a configuração necessária para executar o Ollama com a interface Open WebUI, configurado para utilizar o modelo DeepSeek-R1.

## Conteúdo

- [Requisitos](#requisitos)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Instalação](#instalação)
- [Configuração](#configuração)
- [Uso](#uso)
- [Modelo DeepSeek-R1](#modelo-deepseek-r1)
- [Solução de Problemas](#solução-de-problemas)
- [Recursos Adicionais](#recursos-adicionais)

## Requisitos

- Docker (versão 20.10.0 ou superior)
- Docker Compose (versão 2.0.0 ou superior)
- Mínimo de 8GB de RAM
- Para aceleração GPU (opcional):
  - NVIDIA GPU com drivers instalados
  - NVIDIA Container Toolkit (nvidia-docker2)

## Estrutura do Projeto

```
.
└── docker-compose.yml   # Arquivo de configuração do Docker Compose
```

## Instalação

1. Clone este repositório ou copie o arquivo `docker-compose.yml` para sua máquina local.

2. Navegue até o diretório onde o arquivo `docker-compose.yml` está localizado.

3. Execute o seguinte comando para iniciar os serviços:

```bash
docker-compose up -d
```

Este comando iniciará dois contêineres:
- `ollama`: Servidor Ollama que gerencia os modelos de IA
- `open-webui`: Interface web para interagir com os modelos do Ollama

## Configuração

### Configuração Básica

O arquivo `docker-compose.yml` já está configurado com as configurações padrão para executar o Ollama e o Open WebUI. Não são necessárias configurações adicionais para começar.

### Configuração de GPU (Opcional)

Para habilitar a aceleração de GPU, descomente as seguintes linhas no arquivo `docker-compose.yml`:

```yaml
# deploy:
#   resources:
#     reservations:
#       devices:
#         - driver: nvidia
#           count: 1 # Ou 'all'
#           capabilities: [gpu]
```

### Configurações Avançadas

Para configurações adicionais do Open WebUI, você pode adicionar variáveis de ambiente na seção `environment` do serviço `open-webui`. Por exemplo:

```yaml
environment:
  - OLLAMA_BASE_URL=http://ollama:11434
  - WEBUI_SECRET_KEY=sua_chave_secreta
  # Outras configurações...
```

## Uso

1. Após iniciar os serviços, acesse a interface web em:
   
   [http://localhost:8080](http://localhost:8080)

2. Na primeira execução, você precisará criar uma conta de usuário na interface do Open WebUI.

3. Configure a conexão com o Ollama (geralmente já estará configurada automaticamente como `http://ollama:11434`).

4. Você pode então baixar e usar o modelo DeepSeek-R1 através da interface.

## Modelo DeepSeek-R1

O DeepSeek-R1 é um modelo de linguagem avançado desenvolvido pela DeepSeek. Para utilizá-lo:

### Baixando o Modelo

Você pode baixar o modelo DeepSeek-R1 de duas maneiras:

1. **Através da interface Open WebUI**:
   - Acesse a seção "Models" ou "Gallery"
   - Procure por "deepseek-r1"
   - Clique em "Download" ou "Pull"

2. **Através da linha de comando**:
   ```bash
   docker exec -it ollama ollama pull deepseek-r1
   ```

### Variantes do Modelo

O DeepSeek-R1 está disponível em diferentes variantes:
- `deepseek-r1` - Versão padrão
- `deepseek-r1:7b` - Versão com 7 bilhões de parâmetros
- `deepseek-r1:34b` - Versão com 34 bilhões de parâmetros (requer mais recursos)

Para baixar uma variante específica, adicione o sufixo ao nome do modelo:
```bash
docker exec -it ollama ollama pull deepseek-r1:7b
```

## Solução de Problemas

### Problemas Comuns

1. **Erro de conexão com o Ollama**:
   - Verifique se ambos os contêineres estão em execução: `docker ps`
   - Verifique os logs do Ollama: `docker logs ollama`
   - Certifique-se de que a rede `ollama_net` foi criada corretamente

2. **Problemas de memória ao carregar modelos grandes**:
   - Aumente a memória disponível para o Docker
   - Use uma variante menor do modelo (como `deepseek-r1:7b` em vez de `deepseek-r1:34b`)

3. **Problemas com GPU**:
   - Verifique se o NVIDIA Container Toolkit está instalado corretamente
   - Verifique se os drivers NVIDIA estão atualizados
   - Execute `nvidia-smi` para confirmar que a GPU está sendo detectada

### Verificando Logs

Para verificar os logs dos serviços:

```bash
# Logs do Ollama
docker logs ollama

# Logs do Open WebUI
docker logs open-webui
```

## Recursos Adicionais

- [Documentação oficial do Ollama](https://github.com/ollama/ollama)
- [Documentação do Open WebUI](https://github.com/open-webui/open-webui)
- [Informações sobre o modelo DeepSeek-R1](https://github.com/deepseek-ai/deepseek-LLM)

---

Este projeto utiliza software de código aberto. Todos os direitos reservados aos respectivos proprietários.
