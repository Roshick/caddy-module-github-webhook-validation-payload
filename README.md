# Caddy GitHub Webhook Payload Validation Module

This Caddy handler module validates GitHub webhook payloads by using a shared secret. It ensures that the incoming webhooks are legitimate and come from GitHub, thereby enhancing security for your application.

## Directive

The directive for this module is `validate_github_webhook_payload`.

## Features

- Validates GitHub webhook payloads.
- Uses a shared secret to ensure the request integrity.
- Compatible with Caddy v2.

## Installation

To use this module, you will need to build Caddy with the module included. Here's how you can do it:

1. Install [xcaddy](https://github.com/caddyserver/xcaddy):

    ```bash
    $ go install github.com/caddyserver/xcaddy/cmd/xcaddy@latest
    ```

2. Build Caddy with the `validate_github_webhook_payload` module:

    ```bash
    $ xcaddy build --with github.com/Roshick/validate_github_webhook_payload
    ```

## Configuration

To configure the `validate_github_webhook_payload` directive in your Caddyfile, provide the secret that you will use to validate the webhook payload.

### Caddyfile Example

```caddyfile
{
    # Global options block
}

:80

validate_github_webhook_payload <your_secret_here>

route {
    # Your other directives
    reverse_proxy http://localhost:8080
}
```

Replace `<your_secret_here>` with the actual secret that you have configured in your GitHub webhook settings.

## Usage

1. **Generate a Secret**: Generate a secret, which will be used to sign the payload. You can use any method to generate a secure random string.

2. **Setup GitHub Webhook**: In your GitHub repository settings, add a new webhook and set the secret to the one you generated. The webhook URL should point to the endpoint managed by your Caddy server.

3. **Run Caddy**: Start Caddy with your configured Caddyfile. The server will now validate incoming webhook requests using the provided secret.

## Example

Given the following configuration:

- Webhook URL: `http://yourdomain.com/webhook`
- Secret: `my_super_secret`

The Caddyfile would be:

```caddyfile
{
    # Global options block
}

:80

validate_github_webhook_payload my_super_secret

route {
    handle_path /webhook {
        # Your webhook handler directives
        reverse_proxy http://localhost:8080
    }
}

```

In this example, Caddy will verify the incoming webhook payloads sent to `/webhook` using the secret `my_super_secret`.

## Contribution

Contributions are welcome! Please feel free to submit a pull request or open an issue.

## License

This project is licensed under the MIT License. See the `LICENSE` file for more details.