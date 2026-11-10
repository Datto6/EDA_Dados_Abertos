# Análise dos Dados de Bilhetagem Intermunicipal

Este projeto está sendo desenvolvido pelo LABORATÓRIO DE INTELIGÊNCIA ARTIFICIAL APLICADA (LIA<sup>2</sup>) da Universidade Estadual do Rio de Janeiro (UERJ).
<p></p>
A presente versão inicial realiza uma análise exploratória das bases de bilhetagem do Portal Dados Abertos do Governo do Estado do Rio de Janeiro [https://dadosabertos.rj.gov.br/].
<p></p>
O usuário define data início e data fim em uma interface WEB. Em seguida o projeto busca todos os arquivos disponíveis no Portal Dados Abertos, extrai os dados e realiza uma série de análises, as quais são apresentadas em diversos gráficos. 

### Equipe

- Desenvolvedores: Nilo Zeribinate e Rafael Osborne
- Coordenadores: Karla Figueiredo e Meyer Elias Nigri

## Pré Requisitos
Esse site foi testado nas versões Linux Ubuntu 22.04 e 24.04.
<p></p>
É Necessário ter acesso ao terminal permissão de executar comandos sudo.

Além disso, necessita:
- Python 3.12.3
- Porta 5000 disponível
- Redis
- bibliotecas nas respectivas versões definidas no arquivo requirements.txt

## Como instalar e executar o projeto:

Primeiro, abra um terminal. 

### Instalando arquivos

Vá para um diretório de sua escolha, onde serão feitos o download dos arquivos necessários.

```bash
git clone https://github.com/Datto6/EDA_Dados_Abertos.git 
cd EDA_Dados_Abertos
```
### Dependências

Em seguida, faça a instalação do redis.

```bash
sudo apt update
sudo apt install redis-server
```
Se necessário, habilte os serviços.
```bash
sudo systemctl enable redis
sudo systemctl enable redis-server
```

### Crie um ambiente Virtual

Recomendamos fortemente a criação de uma ambiente virtual Python, de modo que não surja conflito de versões entre bibliotecas.

```bash
python3.12 -m venv .venv 
source .venv/bin/activate
pip install -r requirements.txt
```

Atenção: Não use Versões anteriores ao Python 3.12. Por outro lado, esse projeto não foi testado em versões superiores a 3.12. 

### Comandos

Inicie o Redis, caso não tenah sido iniciado automaticamente:

```bash
sudo systemctl start redis
sudo systemctl start redis-server
```

Execute o worker do Celery:

```bash
celery -A main.celery worker --loglevel=info
```

Em seguida, abra outro terminal e execute a aplicação principal:

```bash
python3 main.py
```

Acesse o site pelo navegador:

```text
http://127.0.0.1:5000
```

No navegador, defina as datas de início e fim, clique "Iniciar Processamento" e aguarde o precessamento ser concluido - tipicamente em 15 minutos.

## Dicas de depuração

- O terminal do Celery exibe os logs e possíveis erros durante o processamento.
- Certifique-se de que o Redis esteja ativo antes de iniciar o worker.
- Os gráficos são armazenados em `static/exports/`, separados por identificador de execução (UUID).
- Os arquivos .csv iniciais e os agregados são mantidos no ./arquivos_default
- Feito o download de um determinado dia, os arquivos desse dia não são baixados novamente em futuros processamentos que incluam o mesmo dia. Ou seja, arquivos baixados permanecem no diretório. No entanto, a análise dos dados é sempre processada para os dias definidos pelo usuário.