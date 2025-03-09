FROM node:20.10.0-alpine3.18
# Definir o diretório de trabalho
WORKDIR /app
# Copiar os arquivos package.json e package-lock.json - O objetivo é aproveitar o cache do docker sempre que possivel
COPY package*.json .
# Instalar as dependências do npm
RUN npm install

# Instalar o pacote 'shadow' que inclui comandos para manipulação de usuários
#Criando o usuario e apos removendo o pacote
RUN apk update && apk add --no-cache findutils && \
    apk add --no-cache shadow && \
    useradd -ms /bin/ash kubenews && \
    apk del shadow

# Copiar os arquivos do diretório atual para o contêiner e ajustar permissões
COPY --chown=kubenews:kubenews . .

#Ajustando as permissoes dos diretorios e arquivos
RUN apk add --no-cache findutils && \
    find . -type f -exec chmod 755 {} \; && \
    find . -type d -exec chmod 755 {} \; && \
    apk del findutils

# Definir 'kubenews' como o usuário padrão
USER kubenews

# Expor a porta 8080
EXPOSE 8080

# Definir o comando padrão para iniciar a aplicação
CMD ["node", "server.js"]

