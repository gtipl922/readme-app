# README Generator Web App

This is a self-hosted web application that allows you and your team to generate README files for your private GitHub repositories.

## Features

- Secure login with your GitHub account (via OAuth).
- Fetches and displays a list of your private repositories.
- Generates a placeholder README file for a selected repository.
- Fully containerized with Docker for easy deployment.

## Prerequisites

- [Docker](https://www.docker.com/get-started) and [Docker Compose](https://docs.docker.com/compose/install/) must be installed on your server or local machine.

## Setup and Configuration

### 1. Create a GitHub OAuth App

Before you can run the application, you need to create a GitHub OAuth App to get a Client ID and Secret.

1.  Go to your GitHub **Settings**.
2.  Navigate to **Developer settings** > **OAuth Apps**.
3.  Click **New OAuth App**.
4.  Fill in the form with the following details:
    *   **Application name:** You can name it anything, e.g., `My README Generator`.
    *   **Homepage URL:** `http://localhost:3000`
    *   **Authorization callback URL:** `http://localhost:3001/auth/github/callback`
5.  Click **Register application**.
6.  On the next page, you will see your **Client ID**. Click **Generate a new client secret** and copy both the Client ID and the new Client Secret.

### 2. Configure Environment Variables

In the root of the project (`gemini-readme-app`), you will find a file named `.env.example`. 

1.  Create a copy of this file and name it `.env`.
2.  Open the `.env` file and replace the placeholder values with the credentials you obtained from your GitHub OAuth App:

```
GITHUB_CLIENT_ID=paste_your_client_id_here
GITHUB_CLIENT_SECRET=paste_your_client_secret_here
SESSION_SECRET=replace_this_with_a_long_random_string
```

**Important:** The `SESSION_SECRET` should be a long, random, and private string. You can generate one easily online.

## Running the Application

Once you have configured your `.env` file, you can build and run the entire application with a single command.

1.  Open a terminal or command prompt in the root of the project (`gemini-readme-app`).
2.  Run the following command:

```bash
docker-compose up --build
```

This command will:
- Build the Docker images for both the frontend client and the backend server.
- Start the containers for both services.

It may take a few minutes the first time you run it as it needs to download the base images and install all dependencies.

## Accessing the Application

Once the containers are running, you can access the web application by navigating to the following URL in your web browser:

[http://localhost:3000](http://localhost:3000)

You will be prompted to log in with your GitHub account. After authorizing the app, you will be redirected to the dashboard where you can see your repositories and generate README files.

## Stopping the Application

To stop the application, press `Ctrl + C` in the terminal where `docker-compose` is running. To remove the containers, you can run:

```bash
docker-compose down
```
