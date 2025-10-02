# use a snall base image
FROM node:18-alpine AS base
WORKDIR /app

# install dependencies separately for caching
COPY package.json package-lock.json* ./
RUN npm ci --omit=dev

# copy app source
COPY . .

# run as non-root (alpine node image includes user 'node')
USER node
EXPOSE 3000
ENV NODE_ENV=production
CMD ["npm", "start"]