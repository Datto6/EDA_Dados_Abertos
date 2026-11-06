## Pré Requisitos
Esse site foi testado nas versões Linux Ubuntu 24.04 e 22.04.
Além disso, utiliza:
- Python 3.12.3
- Redis
- Dependências do requirements.txt

## Como rodar o site:
Primeiro, abra um terminal. 
### Instalando arquivos
Vá para um diretório de escola
Clonar o repositório com git clone. Abra o terminal e vá para um diretório de escolha. 
```bash
git clone https://github.com/Datto6/EDA_Dados_Abertos.git 
cd EDA_Dados_Abertos
```
### Dependências
Primeiro, fazer a instalação do redis, e habilitá-lo
```bash
sudo apt update
sudo apt install redis-server
sudo systemctl enable redis
sudo systemctl enable redis-server
```

Instale as dependências Python:
(Criando ambiente virtual e instalando módulos)
```bash
python3.12 -m venv .venv 
source .venv/bin/activate
pip install -r requirements.txt
```
### Comandos

Primeiramente, inicie o Redis:

```bash
sudo systemctl start redis
sudo systemctl start redis-server
```

Em um terminal, execute o worker do Celery:

```bash
celery -A main.celery worker --loglevel=info
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