## Como rodar o site:

### Dependências

Esta aplicação utiliza o **Redis** como Message Broker e Result Backend para gerenciar as tarefas assíncronas do Celery.

**Linux (Ubuntu/Debian/WSL):**

```bash
sudo apt update
sudo apt install redis-server
sudo systemctl start redis
```

Instale as dependências Python:

```bash
pip install -r requirements.txt
```
### Comandos

Primeiramente, inicie o Redis:

```bash
sudo service redis-server start
```

Em um terminal, execute o worker do Celery:

```bash
celery -A app.celery worker --loglevel=info
```

Em seguida, em outro terminal, execute a aplicação Flask:

```bash
python3 main.py
```

Acesse o site pelo navegador:

```text
http://127.0.0.1:5000
```

## Dicas de depuração

- O terminal do Celery exibe os logs e possíveis erros durante o processamento.
- Certifique-se de que o Redis está ativo antes de iniciar o worker.
- Os gráficos são armazenados em `static/exports/`, separados por identificador de execução (UUID).
- Os arquivos .csv iniciais e os agregados são mantidos no ./arquivos_default
- Feito o download de um dia, o mesmo arquivo não é processado duas vezes, mas a construção de gráficos é sempre do 0.  
