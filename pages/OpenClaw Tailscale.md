# OpenClaw Tailscale integration

OpenClaw can integrate with [Tailscale](https://tailscale.com/) to expose the OpenClaw Gateway dashboard and WebSocket endpoint over a tailnet (or, optionally, to the public internet) while keeping the Gateway bound to loopback on the host.

According to the OpenClaw documentation, OpenClaw can automate **Tailscale Serve** (tailnet-only) or **Tailscale Funnel** (public) for the Gateway’s Control UI and WebSocket port. This approach allows the Gateway to remain bound to `127.0.0.1` while Tailscale provides HTTPS, routing, and (for Serve) identity headers.

## Modes

OpenClaw documents three Tailscale modes for the Gateway:

- **serve**: Tailnet-only exposure via `tailscale serve`, with the Gateway staying on `127.0.0.1`.
- **funnel**: Public HTTPS exposure via `tailscale funnel`; OpenClaw requires a shared password in this mode.
- **off**: No Tailscale automation (default).

## Authentication

OpenClaw’s Gateway authentication can be configured with `gateway.auth.mode`:

- **token**: Uses a token (noted as the default when `OPENCLAW_GATEWAY_TOKEN` is set).
- **password**: Uses a shared password (via `OPENCLAW_GATEWAY_PASSWORD` or configuration).

When `tailscale.mode` is `"serve"` and `gateway.auth.allowTailscale` is enabled, the Control UI and WebSocket can authenticate using Tailscale identity headers (such as `tailscale-user-login`) without supplying a token or password. The documentation describes verifying this identity by resolving the request’s `x-forwarded-for` address via the local Tailscale daemon (using `tailscale whois`) and matching it to the header.

The documentation also notes that this tokenless flow assumes the Gateway host is trusted; if untrusted local code may run on the same host, it recommends disabling `gateway.auth.allowTailscale` and requiring token/password authentication.

## Configuration examples

### Tailnet-only (Serve)

```json
{
  "gateway": {
    "bind": "loopback",
    "tailscale": { "mode": "serve" }
  }
}
```

### Tailnet-only (bind to Tailnet IP)

The documentation describes a `gateway.bind: "tailnet"` mode that binds the Gateway directly to the Tailnet IP address (without Serve/Funnel).

```json
{
  "gateway": {
    "bind": "tailnet",
    "auth": { "mode": "token", "token": "your-token" }
  }
}
```

### Public internet (Funnel + shared password)

```json
{
  "gateway": {
    "bind": "loopback",
    "tailscale": { "mode": "funnel" },
    "auth": { "mode": "password", "password": "replace-me" }
  }
}
```

The OpenClaw documentation recommends preferring the `OPENCLAW_GATEWAY_PASSWORD` environment variable over committing a password to disk.

## CLI examples

The documentation includes CLI flags for enabling Tailscale automation when starting the Gateway, such as:

- `openclaw gateway --tailscale serve`
- `openclaw gateway --tailscale funnel --auth password`

## References

1. OpenClaw documentation: “Tailscale (Gateway dashboard)”. https://docs.openclaw.ai/gateway/tailscale
2. Tailscale documentation: “Serve overview”. https://tailscale.com/kb/1312/serve
3. Tailscale documentation: “Funnel overview”. https://tailscale.com/kb/1223/tailscale-funnel
