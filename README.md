# Avaliacoes-M7-Inteli

Avaliação do Módulo 7 - Henrique Lemos Freire Matias

# 💻 Como executar

Para executar esse projeto, clone esse repositório git e na `root` do projeto rode o seguinte comando no terminal:

```bash
docker compose up
```

Pronto! Agora você pode acessar os seguintes serviços nos seguintes endereços:

- Frontend -> http://localhost:3000/
- Backend -> http://localhost:8000

# 🐳 Construção do Dockerfile

Para a elaboração da resolução da questão prática da prova foram contruídos os seguintes `Dockerfile` para os seguintes serviços:

- backend
- frontend

## 📊 Dockerfile backend

Na primeira linha já podemos encontrar um comando responsável por identificar a "imagem base" que será utilizada, nesse caso utilizamos a imagem já existente do python com a versão do python em 3.11.2.  
Com isso, essa imagem já terá as funções básicas do python 3.11.2. Após isso, expecificamos em que pasta a imagem colocará os arquivos e em qual lugar os comandos subsequêntes serão executados, nesse caso expecificamos que a pasta se chame `backend`.  
Agora, precisamos instalar todas as bibliotecas necessárias para a nossa aplicação rodar. Para isso utilizamos o comando de `copy` e `run` para que seja copiado o arquivo `requirements.txt` para dentro da imagem na root da pasta `backend` e em seguida execute o comando `pip` referente a instalação das bibliotecas expecificadas no arquivo `.txt` (utilizamos do argumento `--no-cache-dir` para não atrapalhar o sistema de cache nativo do docker).  
Agora, preciso de copiar todos os arquivos do serviço que se encontra no computador do host para dentro da imagem, para isso que é utilizado o comando `copy . .`.  
Por fim, exponho a porta `8000`, a qual a aplicação precisa ter acesso, e defino o comando para o ponto de entrada do container, que no caso é o comando para rodar o servidor:

```bash
python3 main.py
```

## 📺 Dockerfile frontend

Na primeira linha já podemos encontrar um comando responsável por identificar a "imagem base" que será utilizada, nesse caso utilizamos a imagem já existente do node com a versão do node em 20.  
Com isso, essa imagem já terá as funções básicas do node20. Após isso, expecificamos em que pasta a imagem colocará os arquivos e em qual lugar os comandos subsequêntes serão executados, nesse caso expecificamos que a pasta se chame `frontend`.  
Agora, precisamos instalar todas as bibliotecas necessárias para a nossa aplicação rodar. Para isso utilizamos o comando de `copy` e `run` para que seja copiado o arquivo `package.json` para dentro da imagem na root da pasta `frontend` e em seguida execute o comando `npm` referente a instalação das bibliotecas expecificadas no arquivo `package.json` (perceba que nesse caso, há um arquivo .dockerignore no frontend para que não seja enviado para o container a pasta `node_modules`, para que não misture as versões da maquina em que esse repositório git se encontrará e com o container).  
Agora, preciso de copiar todos os arquivos do serviço que se encontra no computador do host para dentro da imagem, para isso que é utilizado o comando `copy . .`.  
Por fim, exponho a porta `3000`, a qual a aplicação precisa ter acesso, e defino o comando para o ponto de entrada do container, que no caso é o comando para rodar o frontend:

```bash
node server.js
```

# 🐙 Construção do docker-compose

Foi construído um docker-compose que é responsável por gerir os containers de cada serviço.  
Na primeira linha, já podemos encontrar a versão utilizada do docker-compose, a qual é a "3".  
Após isso, definimos os serviços que esse "docker-compose" irá gerir, ou seja, os containers que ele irá gerir. Nesse caso, colocamos como nome de: "backend" e "frontend". Dentro de cada serviço expecificamos o nome da imagem que ele deve puxar do `docker hub` para aquele serviço respectivamente.  
Por fim, realizamos o "link" das portas do containers e do computador do "host", para que o conteúdo de cada container possa ser acessado.  
**Obs1.: Note que foi utilizado `depends_on` no serviço do frontend, para que ele apenas seja iniciado após o inicio do container do backend**  
**Obs2.: Note que foi utilizado `restart: always` em ambos os serviços para que o conteúdo de ambos os containers sejam reiniciados toda vez que o container é "desligado" e "ligado"**
