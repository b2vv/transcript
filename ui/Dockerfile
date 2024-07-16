# First stage: build
FROM node:lts-alpine AS builder

# Create and change to the app directory
WORKDIR /app

# Copy application dependency manifests to the container image.
COPY ./audio-transcript-ui/package*.json .

# Install dependencies
RUN npm install

## Copy local code to the container image.
COPY ./audio-transcript-ui .

RUN npm run build

# Second stage: runtime
FROM nginx:latest

WORKDIR /usr/share/nginx/html

COPY --from=builder /app/dist .

COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
