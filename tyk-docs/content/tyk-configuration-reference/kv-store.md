---
title: Key Value Secrets Storage for Configuration in Tyk
description: Learn how to configure Tyk Gateway to retrieve values from external key-value stores such as Consul, Vault, local storage, or environment variables.
tags: ["Vault", "Consul", "key-value", "secret kv store"]
menu:
  main:
    parent: Tyk Gateway
weight: 13
aliases:
  - /tyk-stack/tyk-gateway/kv-store/
---
Tyk Gateway, as of v3.0, supports storing secrets in Key-Value (KV) systems such as [Vault](https://vaultproject.io), [Consul](https://consul.io), local storage, and environment variables. By referencing these values from the KV store in your `tyk.conf`, API definitions, middleware, and environment variables, you can:

- Easily manage and update secrets across multiple environments (e.g., development, staging, production) without modifying the configuration files.
- Securely store sensitive information like API keys, passwords, and certificates in a centralized location.
- Choose the most suitable configuration method for your deployment, whether it's using configuration files (`tyk.conf`) or environment variables (e.g., in Kubernetes).

## Supported KV Store Systems

Tyk Gateway supports the following KV store systems:

- **Consul**: Consul is a distributed, highly available, and data center aware solution to connect and configure applications across dynamic, distributed infrastructure. It can be used to store and retrieve Tyk Gateway secrets across multiple data centers.

- **Vault**: Vault is a tool for securely accessing secrets. It provides a unified interface to any secret while providing tight access control and recording a detailed audit log. Tyk Gateway can use Vault to manage and retrieve sensitive secrets such as API keys, passwords, and certificates.

- **Local secrets section inside `tyk.conf`**: The local secrets section in the `tyk.conf` file allows you to store secrets specific to a single Tyk Gateway instance. This is useful for storing instance-specific secrets or if you prefer using configuration files.

- **Environment variables**: Environment variables can be used to store secrets and can be accessed by Tyk Gateway. This is a simple and straightforward way to manage secrets, especially in containerized environments like Docker or Kubernetes.

## Referencing KV Store Values

You can reference values from KV stores in the following places:

1. Configuration file (`tyk.conf`)
2. API definitions
3. Middleware (request body transform, response body transform, URL rewrite, request header injection, response header injection)

### 1. Configuration File (`tyk.conf`)

In the `tyk.conf` file, you can reference values from KV stores for the following fields:

- `secret`
- `node_secret`
- `storage.password`
- `cache_storage.password`
- `security.private_certificate_encoding_secret`
- `db_app_conf_options.connection_string`
- `policies.policy_connection_string`

To reference a value from a KV store, use the following notation:

- Consul: `consul://path/to/value`
- Vault: `vault://path/to/secret`
- Local secrets: `secrets://key`
- Environment variables: `env://key`

These variables are replaced on gateway start when loading the `tyk.conf` file.

### 2. API Definitions

From Tyk Gateway v5.3 onwards, you can store any string field from the API definition in KV stores. Previously, only the `proxy.target_url` and `proxy.listen_path` fields were supported.

To reference a value from a KV store in an API definition field, use the same notation as in the `tyk.conf` file:

- Consul: `consul://path/to/value`
- Vault: `vault://path/to/secret`
- Local secrets: `secrets://key`
- Environment variables: `env://key`

Secrets in API definitions are replaced on API load. If a secret changes, you will need to reload the API for the changes to take effect.

Example API definition:

```json
{
  "name": "My API",
  "proxy": {
    "listen_path": "env://MY_LISTEN_PATH",
    "target_url": "consul://my-api/target-url"
  }
}
```

### 3. Middleware

In the following middleware, you can reference values from KV stores using the prefixes below:

- Request Body Transform
- Response Body Transform
- URL Rewrite
- Request Header Injection
- Response Header Injection

Prefixes for referencing KV store values in middleware:

- Consul: `$secret_consul.`
- Vault: `$secret_vault.`
- Local secrets: `$secret_conf.`
- Environment variables: `$secret_env.`

Secrets in middleware are evaluated dynamically on each request.

Example request body transform:

```json
{
  "body": "{\n  \"user\": \"$secret_vault.user\",\n  \"password\": \"$secret_env.PASSWORD\"\n}"
}
```

Example URL rewrite:

```json
{
  "path": "/api/v1/users/$secret_consul.user_id"
}
```

## Configuring KV Stores

To connect Tyk Gateway to KV stores, configure the respective settings in the `tyk.conf` file or using environment variables.

### Configuring KV Stores in `tyk.conf`

Here's an example of how to configure multiple KV stores in `tyk.conf`:

```json
{
  "kv": {
    "consul": {
      "address": "localhost:8025",
      "scheme": "http",
      "datacenter": "dc-1",
      "timeout": 30,
      "http_auth": {
        "username": "username",
        "password": "password"
      },
      "wait_time": 10,
      "token": "Token if available",
      "tls_config": {
        "address": "",
        "ca_path": "",
        "ca_file": "",
        "cert_file": "",
        "key_file": "",
        "insecure_skip_verify": false
      }
    },
    "vault": {
      "address": "http://localhost:1023",
      "agent_adress": "input if available",
      "max_retries": 3,
      "timeout": 30,
      "token": "token if available",
      "kv_version": 2
    }
  },
  "secrets": {
    "gateway": "secret"
  }
}
```

### Configuring KV Stores using Environment Variables

Alternatively, you can configure KV stores using environment variables. For example, to configure Vault, use the following environment variables:

```env
TYK_GW_KV_VAULT_ADDRESS=http://VAULT_CONNECTION_STRING:VAULT_CONNECTION_PORT
TYK_GW_KV_VAULT_MAXRETRIES=3
TYK_GW_KV_VAULT_TIMEOUT=30s
TYK_GW_KV_VAULT_TOKEN=VAULT_TOKEN
TYK_GW_KV_VAULT_KVVERSION=2
```

You can also define environment variables with the prefix `TYK_SECRET_` followed by a custom name (e.g., `TYK_SECRET_FOO`, `TYK_SECRET_BAR`). These environment variables can be referenced in the API definition using the format `env://foo` or `env://bar` for fields like `listen_path` or `target_url`.

If you want to set the local "secrets" section as an environment variable, use the following notation:
`TYK_GW_SECRETS=key:value,key2:value2`

For detailed information on configuring each KV store, refer to the [Configuration Reference]({{< ref "tyk-oss-gateway/configuration#a-namekva-key-value-store" >}}).

#### Retrieving Secrets from Vault

When retrieving secrets from Vault, you can use the dot notation to access specific values within a secret. For example, if you have a secret named `tyk` with a key `gw` and value `123` stored in Vault, you can retrieve the value using `vault://secret/tyk.gw`.

To retrieve the secret from within Vault:

```curl
curl \
  --header "X-Vault-Token: <your_vault_token>" \
  --request GET \
  https://vault-server.example.com/v1/secret/tyk?lease=true
```

The response will be similar to:

```yaml
{
   "request_id": "0c7e44e1-b71d-2102-5349-b5c60c13fb02",
   "lease_id": "",
   "lease_duration": 0,
   "renewable": false,
   "data": {
      "gw": "123"
      "excited": "yes",
      "foo": "world",
   },
   "metadata":{
      "created_time": "2019-08-28T14:18:44.477126Z",
      "deletion_time": "",
      "destroyed": false,
      "version": 1
   },
   "auth": ...
}
```

Note that there is no need to append `/data` to the secret path.

## Considerations

- If Tyk Gateway cannot communicate with the KV store, it will log an error but still load the APIs.
- Ensure that the necessary configuration and connection details are properly set up for each KV store being used.
- All fields in the classic and OAS API definitions support referencing values from KV stores.
- Fields can use values from different KV stores simultaneously.

For more information and examples, refer to the [KV Store Configuration Documentation]({{< ref "tyk-oss-gateway/configuration#a-namekva-key-value-store" >}}).
