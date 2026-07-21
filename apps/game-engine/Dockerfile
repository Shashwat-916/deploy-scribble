FROM oven/bun:1

WORKDIR /app

# Copy dependency files first
COPY package.json bun.lockb ./
RUN bun install

# Copy source code
COPY . .

EXPOSE 8080

# You can use the start script from your package.json
CMD [ "bun", "run", "start" ]