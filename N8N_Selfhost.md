# n8n Self-Hosting with Ngrok

## Introduction

[n8n](https://n8n.io/) is a powerful workflow automation tool that allows you to connect various services and automate tasks. This guide provides step-by-step instructions on how to expose an existing n8n self-hosted instance to the internet securely with Ngrok.

## What is ngrok?

Ngrok is a tool that creates secure tunnels to your localhost, allowing you to expose local web servers behind NATs and firewalls to the internet.


## Prerequisites

Before getting started, ensure you have the following installed on your system:

- [Ngrok](https://ngrok.com/download)
- An existing n8n self-hosted instance running via Docker

## Step 1: Expose n8n to the Internet Using Ngrok

1. Start Ngrok and expose port 5678:
   ```sh
   ngrok http http://localhost:5678
   ```
   ![image](https://github.com/user-attachments/assets/b91179f9-e747-46a8-b498-fa878b49d50c)

2. Ngrok will provide a forwarding URL (e.g., `https://randomsub.ngrok.io`). Copy this URL.
   
   ![image](https://github.com/user-attachments/assets/c1a4dd36-739b-4f43-8807-af44e20e5775)

4. Stop the running n8n container:
   ```sh
   docker-compose down
   ```
5. Update your n8n environment variables to include the Ngrok URL:
   ```sh
   WEBHOOK_URL=https://20b3-197-211-58-214.ngrok-free.app
   ```
6. Restart n8n with the updated configuration:
   ```sh
   docker-compose up -d
   ```

## Step 2: Access n8n

1. Open your browser and visit `http://localhost:5678`
2. Log in with your existing credentials.
3. To use webhooks in workflows, ensure that external services send requests to the Ngrok URL (`https://20b3-197-211-58-214.ngrok-free.app`).
   
   ![image](https://github.com/user-attachments/assets/c5e1a0c1-46b1-44e1-93df-ab1c3641fa4c)

## Step 3: Set Up a Static Domain (Free Plan)

Ngrok now allows the use of static domains even on the free plan. This provides a persistent URL that doesn't change every time you restart the tunnel.

## Steps to Get a Static Domain:

1. Go to your ngrok dashboard.
2. Navigate to the Deploy your app online section.
3. Under the Static Domain tab, copy the provided URL and command.
   ![image](https://github.com/user-attachments/assets/843975ef-62da-470f-8cff-111aab174aa2)
   
4. Replace the static url with the temporary url provided to you earlier in the environment variables
   ```sh
   WEBHOOK_URL=https://lark-striking-wholly.ngrok-free.app
   ```
6. Run the command in your terminal.
   ```sh
   ngrok http --url=lark-striking-wholly.ngrok-free.app 5678
   ```
Now, you have a permanent/static link that will remain the same as long as you use this command.

## Troubleshooting

- If n8n doesn’t start correctly, check the logs:
  ```sh
  docker-compose logs -f
  ```
- Ensure your Ngrok session is running; otherwise, restart it and update the `WEBHOOK_URL`.

## Conclusion

You have successfully exposed your self-hosted n8n instance to the internet securely using Ngrok. This setup enables you to develop and test workflows that require external webhook connections.

For more details, visit the [n8n documentation](https://docs.n8n.io/).
