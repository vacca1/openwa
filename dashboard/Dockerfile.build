# Debian (glibc) base — avoids Alpine/musl issues with rollup & esbuild
# optional native binaries that break `npm ci` on node:*-alpine.
FROM node:22-bookworm-slim AS builder

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies — `npm install` (not `npm ci`) so the correct
# platform-specific optional deps (rollup/esbuild linux binaries) are
# resolved even though the committed lockfile was generated on macOS.
RUN npm install --no-audit --no-fund

# Copy source code
COPY . .

# Build the app
RUN npm run build

# Production stage with nginx
FROM nginx:alpine

# Copy built files
COPY --from=builder /app/dist /usr/share/nginx/html

# Copy nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
