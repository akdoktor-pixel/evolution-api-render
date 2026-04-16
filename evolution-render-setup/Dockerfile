FROM node:18-alpine

WORKDIR /app

# Evolution API'yi indir
RUN git clone https://github.com/EvolutionAPI/evolution-api.git .

# Bağımlılıkları yükle
RUN npm install

# Port açın
EXPOSE 8080

# Başlat
CMD ["npm", "start"]
