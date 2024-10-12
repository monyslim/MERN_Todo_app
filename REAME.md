# **Todo App (Frontend & Backend)**

## **Overview**
This project is a Todo Application consisting of a React frontend and an Express backend that connects to a MongoDB Atlas database. The frontend is hosted on Amazon S3, while the backend is deployed using AWS Lambda and API Gateway. Both the frontend and backend use environment variables *(.env)* for configuration.

### Backend Adjustments for AWS Lambda
The Express backend was modified to work in a serverless environment like AWS Lambda. Below are the main changes made:

### Changes Made in the backend folder:
1. Removed **app.listen()**: Since Lambda manages the request/response lifecycle, the explicit app.listen() function was removed.

2. Installed *serverless-http*: To make the Express app compatible with AWS Lambda, serverless-http was used to wrap the Express app.

3. Environment Variables *(.env)*:
The MongoDB connection string (DB_URL) and other sensitive data were moved to a .env file.
AWS Lambda also allows environment variables to be set directly in its configuration panel.

## Steps to Deploy Backend on AWS Lambda
1. Prepare the Code:

Ensure all backend code, including the node_modules folder, is ready and compressed into a .zip file.

2. Set Up AWS Lambda:

Go to the AWS Lambda console, create a new function with Node.js as the runtime.
Upload the .zip file containing your backend code.

3. Set Environment Variables in Lambda:

In the Lambda function settings, add the environment variables used in the backend, such as DB_URL for MongoDB.

4. Set Up API Gateway:

Create a new API in AWS API Gateway.
Define routes in API Gateway that map to your backend endpoints (e.g., /todo, /todo/:id).
Integrate the API Gateway with your Lambda function so that API requests are forwarded to the backend.

5. Testing the API:

Once API Gateway is set up, you’ll get an Invoke URL that serves as the base URL for your backend. You can use tools like Postman to test the endpoints.

*Note: In AWS Lambda, you will set these variables in the function’s environment settings.*

## Frontend Adjustments for S3 Hosting
The React frontend is deployed as a static website hosted on an S3 bucket. Since the backend is on AWS Lambda (invoked via API Gateway), the React app needs to communicate with the backend through the API Gateway URL.

- Changes Made:
    - API Base URL:

The API base URL was changed to the Invoke URL of the API Gateway created in the backend setup.
This is done using environment variables *(REACT_APP_API_BASE_URL)* in a .env file.

-Environment Variables (.env):

    -A *.env *file is used to manage the API Gateway URL. React apps can read environment variables prefixed with REACT_APP_.


## Steps to Deploy Frontend on AWS S3
1. Set Up .env File:
    - In the root of your React project, create a .env file to store the API Gateway URL:
    '''bash
    REACT_APP_API_BASE_URL=https://your-api-gateway-url.amazonaws.com/production
    '''
2. Build the React App:
    - Run the following command to build the production-ready version of the app:
    '''bash
    npm run build
    '''
    This will generate a build folder with optimized static files for deployment.
3. Create an S3 Bucket:
- Go to the AWS S3 console and create a new bucket for hosting the frontend.
- Enable static website hosting in the bucket settings and set index.html as the entry point.

4. Upload Build Files:
    - Upload all files from the build/ folder to the S3 bucket.