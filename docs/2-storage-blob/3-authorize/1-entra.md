---
sidebar_position: 1
title: Microsoft Entra ID
---

Use Microsoft Entra ID when you do not want to use account keys.

This guide uses [`azure-oss/identity`](https://github.com/Azure-OSS/azure-identity-php) (repository: `azure-identity-php`) for token acquisition.

:::warning
This feature is not released yet.
:::

## Install

```shell
composer require azure-oss/identity
```

## Create Client

`DefaultAzureCredential` is the easiest default option.

```php
<?php

use AzureOss\Identity\DefaultAzureCredential;
use AzureOss\Storage\Blob\BlobServiceClient;
use GuzzleHttp\Psr7\Uri;

$credential = new DefaultAzureCredential();

$endpoint = new Uri('https://'.getenv('AZURE_STORAGE_ACCOUNT_NAME').'.blob.core.windows.net/');
$service = new BlobServiceClient($endpoint, $credential);
```

## Resolution Order

`DefaultAzureCredential` tries these sources in this order and uses the first one that can get a token:

1. Environment-based service principal settings:
   `AZURE_TENANT_ID`, `AZURE_CLIENT_ID`, and either
   `AZURE_CLIENT_SECRET` or `AZURE_CLIENT_CERTIFICATE_PATH`
   (optional: `AZURE_CLIENT_CERTIFICATE_PASSWORD`)
2. Workload identity
3. Managed identity

## Notes

- Token-based credentials cannot generate SAS URLs in this SDK (`canGenerateSasUri()` returns `false`).
- For SAS-based workflows, use access keys instead.

## Credential Options

| Credential | Use when | Required values |
| --- | --- | --- |
| `DefaultAzureCredential` | Best default for local and hosted workloads; tries multiple sources in order. | Depends on the source it resolves to. |
| `ClientSecretCredential` | Service principal with client secret. | `tenantId`, `clientId`, `clientSecret` constructor arguments. |
| `ClientCertificateCredential` | Service principal with certificate authentication. | `tenantId`, `clientId`, `clientCertificatePath` (+ optional password). |
| `ManagedIdentityCredential` | Workloads running in Azure with managed identity. | No secret values; identity is assigned on the Azure resource. |
| `WorkloadIdentityCredential` | Kubernetes/federated identity (OIDC) scenarios. | Federated workload identity configuration. |
