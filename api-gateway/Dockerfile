# Stage 1: Builder
FROM node:20-alpine AS builder

WORKDIR /app

# Copy package.json and prisma folder
COPY package*.json ./

# Install app dependencies and build
RUN pnpm install

# Copy the rest of the app
COPY . .

# remove old build
RUN rm -rf dist

# Build the app
RUN pnpm run build

# Stage 2: Production Image
FROM node:20-alpine AS production

WORKDIR /app

# Copy only the production build and install production dependencies
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./
COPY --from=builder /app/.env ./

# Install only production dependencies
RUN pnpm install --prod


