# Evolution API Container

Este repositório contém a configuração de um container Docker para a Evolution API.

## Descrição

O container `evolution_api` utiliza a imagem `atendai/evolution-api:v2.1.1` e está configurado para rodar com suporte a banco de dados PostgreSQL e cache Redis.

## Configuração

O arquivo `docker-compose.yml` define o container com as seguintes configurações:
- **Imagem**: `atendai/evolution-api:v2.1.1`
- **Porta**: 8080
- **Variáveis de ambiente**: Carregadas do arquivo `.env`
- **Volumes**: `evolution_instances` para persistência de dados
- **Redes**:
  - `postgres_net` (banco de dados PostgreSQL)
  - `redis_net` (cache Redis)
- **Healthcheck**: Testa a API a cada 10 segundos usando `curl`

## Como Usar

### Subir o container
```sh
docker-compose up -d
```

### Parar o container
```sh
docker-compose down
```

### Verificar logs
```sh
docker logs evolution_api
```

### Testar se a API está rodando
```sh
curl http://localhost:8080/manager
```
Se a API estiver funcionando corretamente, ela deve responder com status HTTP 200.

## Persistência de Dados
Os dados da Evolution API são armazenados no volume `evolution_instances`, garantindo que informações importantes sejam mantidas entre reinícios do container.

## Monitoramento da Saúde
O healthcheck executa `wget http://localhost:8080/manager` a cada 10 segundos. Se a API falhar três vezes seguidas, o container será marcado como unhealthy.

## Licença
Este projeto é de uso interno e não possui licença definida.

