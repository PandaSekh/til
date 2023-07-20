# Docker Image Layers - Caching

When building a Docker Image, the Dockerfile specifies the sequence of commands to create each layer. These layers are based on the content they contain and are identified by unique cryptographic hashes. Such an approach enables caching, making subsequent builds faster and more efficient.

![Docker Image Layers](image_layers.png)

To create highly optimized Docker Images, developers can employ various strategies. One key approach is to structure the Dockerfile so that each layer remains as small as possible. By doing this, unchanged layers can be cached, reducing build times and resource consumption.

Consider this example Dockerfile for a Node.js application:

```dockerfile
FROM node:16-alpine
WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY /src .
RUN npm run build

EXPOSE 3000

CMD [ "npx", "serve", "build" ]
```

In this case, by copying the package.json and installing dependencies separately, Docker can cache this layer. Subsequent builds that do not introduce new dependencies will skip this step, resulting in faster and more efficient image builds.