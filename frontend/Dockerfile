FROM node:18-alpine

ENV HTTP_PROXY=http://127.0.0.1:8889
ENV HTTPS_PROXY=http://127.0.0.1:8889

# Install Python and essential build tools
RUN apk add --update --no-cache python3 make g++ && ln -sf python3 /usr/bin/python
RUN python3 -m ensurepip
RUN pip3 install --no-cache --upgrade pip setuptools

# Create the directory on the node image 
# where our Next.js app will live
RUN mkdir -p /app

# Set /app as the working directory
WORKDIR /app

# Copy package.json and yarn.lock
# to the /app working directory
COPY package*.json yarn.lock ./

# Install dependencies in /app
RUN yarn install

# Copy the rest of our Next.js folder into /app
COPY . .

# Build the Next.js application
RUN yarn build

# Ensure port 3000 is accessible to our system
EXPOSE 3000

ENV HTTP_PROXY ""
ENV HTTPS_PROXY ""

# Run yarn start, as we would via the command line 
CMD ["yarn", "start"]