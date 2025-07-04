# A imagem 'python:3.13.5-alpine3.22' não existe.
# É recomendado usar uma versão estável do Python, como a 3.11.
# A imagem 'slim' é uma ótima opção, pois é leve e mais compatível que a 'alpine'.
FROM python:3.11-slim

# Define o diretório de trabalho dentro do contêiner
WORKDIR /app

# Cria um usuário não-root para rodar a aplicação por segurança
RUN useradd --create-home appuser

# Copia o arquivo de dependências primeiro para aproveitar o cache do Docker
COPY requirements.txt .

# Instala as dependências
RUN pip install --no-cache-dir -r requirements.txt

# Copia o restante do código e define as permissões para o novo usuário
COPY . .
RUN chown -R appuser:appuser /app

# Muda para o usuário não-root
USER appuser

# Expõe a porta que a aplicação irá rodar
EXPOSE 8000

# Comando para iniciar a aplicação em modo de produção (sem --reload)
# Para desenvolvimento, você pode sobrescrever este comando no docker-compose.yml
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]