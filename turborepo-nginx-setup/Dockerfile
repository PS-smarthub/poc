# Etapa 1: Construir o projeto usando uma imagem Node.js
FROM node:18-alpine AS builder
WORKDIR /app

# Copie apenas os arquivos de configuração e o package.json para instalar as dependências
COPY turbo.json ./
COPY apps/web/package.json ./apps/web/
COPY packages/*/package.json ./packages/
COPY package.json ./

COPY . .

RUN npm install --legacy-peer-deps

RUN npx turbo run build --filter=web...

# Etapa 2: Configurar o Nginx para servir o conteúdo estático
FROM nginx:alpine
COPY --from=builder /app/apps/web/.next /usr/share/nginx/html

# Copiar o arquivo de configuração do Nginx
COPY nginx.conf /etc/nginx/nginx.conf

# Expor a porta 80 para o servidor web
EXPOSE 80

# Comando de inicialização do Nginx
CMD ["nginx", "-g", "daemon off;"]
