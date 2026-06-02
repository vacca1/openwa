# Prebuilt dashboard — serves the committed ./dist with nginx.
# The Vite build is done locally (npm run build) and the result is
# committed, so the VPS does NOT run npm (avoids build-env issues).
# To rebuild: `cd dashboard && npm install && npm run build`, then commit dist/.
# (The full source build lives in Dockerfile.build.)
FROM nginx:alpine

COPY dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
