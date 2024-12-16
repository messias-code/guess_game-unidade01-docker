# Imagem oficial do Python como base
FROM python:3.10

# Atualiza e instala dependências do sistema
RUN apt-get update && apt-get install -y build-essential

# Defini o diretório de trabalho dentro do container
WORKDIR /app  

# Copia o código do repositório para dentro do container
COPY . /app  

# Instala as dependências Python definidas no arquivo 'requirements.txt'
RUN pip install -r requirements.txt

# Variáveis de ambiente para a configuração do Flask
ENV FLASK_APP=run.py
ENV FLASK_DB_TYPE=postgres
ENV FLASK_DB_USER=postgres
ENV FLASK_DB_PASSWORD=secretpass  
ENV FLASK_DB_HOST=postgres
ENV FLASK_DB_PORT=5432  
ENV FLASK_DB_NAME=postgres  

# Roda o Flask app
CMD ["flask", "run", "--host=0.0.0.0", "--port=5000"]
