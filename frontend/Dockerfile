# Imagem base para build do React
FROM node:18 as build  

# Define o diretório de trabalho dentro do container para /app. Todas as operações subsequentes (COPY, RUN, etc.) serão executadas neste diretório.
WORKDIR /app  

# Copia e instala dependências
COPY package*.json ./  

# Habilita o Corepack (gerenciador de pacotes) e instala todas as dependências listadas no package.json.
RUN corepack enable && npm install  

# Defini variável de ambiente para o backend
ENV REACT_APP_BACKEND_URL=http://localhost:5000  

# Copia o restante do código para buildar o aplicativo
COPY . ./  
# Executa o script `build` do React, gerando os arquivos estáticos prontos para produção na pasta `build`.
RUN npm run build  

# Imagem base para servir o React
FROM nginx:latest  

# Remove a configuração padrão do NGINX
RUN rm -rf /usr/share/nginx/html/*  

# Copia os arquivos estáticos do React para a pasta do NGINX
COPY --from=build /app/build /usr/share/nginx/html  

# Expõe a porta 80
EXPOSE 80  

# Inicia o servidor NGINX
CMD ["nginx", "-g", "daemon off;"]