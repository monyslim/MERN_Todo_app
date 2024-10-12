# Use the official Node.js image as the base
FROM node:18-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to install dependencies
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code into the container
COPY . .

# Expose the port your app runs on (this should match the port in your app)
EXPOSE 3500

# Define environment variables to be used by the container
ENV PORT=3500
# You can set other environment variables like MongoDB URL here
# ENV DB_URL=mongodb+srv://username:password@cluster.mongodb.net/dbname?retryWrites=true&w=majority

# Run the application
CMD ["npm", "run", "start"]