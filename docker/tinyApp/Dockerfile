# Specify a base image
FROM node:14-alpine

# Establish a work directory
WORKDIR /usr/app

# Copy necessary files into the container
# Not the best practive to move it to the root directory
COPY ./package.json ./

# Install some dependencies
RUN npm install

COPY ./ ./

# Set Up Defaul Command
CMD ["npm", "start"]