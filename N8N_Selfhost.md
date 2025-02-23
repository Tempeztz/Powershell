# n8n Self-Hosting with Ngrok

## Introduction

[n8n](https://n8n.io/) is a powerful workflow automation tool that allows you to connect various services and automate tasks. This guide provides step-by-step instructions on how to expose an existing n8n self-hosted instance to the internet securely with Ngrok.

## Prerequisites

Before getting started, ensure you have the following installed on your system:

- [Ngrok](https://ngrok.com/download)
- An existing n8n self-hosted instance running via Docker

## Step 1: Expose n8n to the Internet Using Ngrok

1. Start Ngrok and expose port 5678:
   ```sh
   ngrok http 5678
   ```
2. Ngrok will provide a forwarding URL (e.g., `https://randomsub.ngrok.io`). Copy this URL.
3. Stop the running n8n container:
   ```sh
   docker-compose down
   ```
4. Update your n8n environment variables to include the Ngrok URL:
   ```sh
   export WEBHOOK_TUNNEL_URL=https://randomsub.ngrok.io
   ```
5. Restart n8n with the updated configuration:
   ```sh
   docker-compose up -d
   ```

## Step 2: Access n8n

1. Open your browser and visit `http://localhost:5678`
2. Log in with your existing credentials.
3. To use webhooks in workflows, ensure that external services send requests to the Ngrok URL (`https://randomsub.ngrok.io`).

## Troubleshooting

- If n8n doesn’t start correctly, check the logs:
  ```sh
  docker-compose logs -f
  ```
- Ensure your Ngrok session is running; otherwise, restart it and update the `WEBHOOK_TUNNEL_URL`.

## Conclusion

You have successfully exposed your self-hosted n8n instance to the internet securely using Ngrok. This setup enables you to develop and test workflows that require external webhook connections.

For more details, visit the [n8n documentation](https://docs.n8n.io/).
