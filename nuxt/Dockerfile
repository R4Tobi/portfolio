# Use the official Node.js image as the base image
FROM node:22-alpine

# Set the working directory
WORKDIR /app

COPY ./src/ .
RUN rm -R node_modules
RUN find . -type f -exec dos2unix {} \;
RUN find . -type f -exec sed -i 's/\r//g' {} +

# RUN rm -R node_modules

RUN npm install

# Build the Nuxt.js application
RUN npm run build

# Expose the port the app runs on
EXPOSE 80

# Start the application
CMD [ "node", ".output/server/index.mjs" ]