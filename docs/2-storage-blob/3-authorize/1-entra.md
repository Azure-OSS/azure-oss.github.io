---
sidebar_position: 1
title: Microsoft Entra ID
---

Use Microsoft Entra ID when you do not want to use account keys.

This SDK supports token-based authentication via `TokenCredential` implementations such as `DefaultAzureCredential`, `ClientSecretCredential`, `ClientCertificateCredential` and `WorkloadIdentityCredential`.

## Prerequisites

Your identity must have **Azure RBAC** permissions on the storage account (or narrower scope like a container). Common roles:

- `Storage Blob Data Contributor` (read/write blobs)
- `Storage Blob Data Reader` (read-only)

## Quickstart

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

## Credentials

### DefaultAzureCredential

`DefaultAzureCredential` tries these sources in this order and uses the first one that can get a token:

1. Environment-based service principal settings:
   `AZURE_TENANT_ID`, `AZURE_CLIENT_ID`, and either
   `AZURE_CLIENT_SECRET` or `AZURE_CLIENT_CERTIFICATE_PATH`
   (optional: `AZURE_CLIENT_CERTIFICATE_PASSWORD`)
2. Workload identity
3. Managed identity (experimental)

Example:

```php
<?php

use AzureOss\Identity\DefaultAzureCredential;
use AzureOss\Storage\Blob\BlobServiceClient;
use GuzzleHttp\Psr7\Uri;

$credential = new DefaultAzureCredential();

$endpoint = new Uri('https://'.getenv('AZURE_STORAGE_ACCOUNT_NAME').'.blob.core.windows.net/');
$service = new BlobServiceClient($endpoint, $credential);
```

### Service principal

If you set the environment variables listed above, `DefaultAzureCredential` automatically authenticates using them.

If you prefer to be explicit, use `ClientSecretCredential`:

```php
<?php

use AzureOss\Identity\ClientSecretCredential;
use AzureOss\Storage\Blob\BlobServiceClient;
use GuzzleHttp\Psr7\Uri;

$credential = new ClientSecretCredential(
    tenantId: getenv('AZURE_TENANT_ID'),
    clientId: getenv('AZURE_CLIENT_ID'),
    clientSecret: getenv('AZURE_CLIENT_SECRET'),
);

$endpoint = new Uri('https://'.getenv('AZURE_STORAGE_ACCOUNT_NAME').'.blob.core.windows.net/');
$service = new BlobServiceClient($endpoint, $credential);
```

If you use certificate authentication, use `ClientCertificateCredential`:

```php
<?php

use AzureOss\Identity\ClientCertificateCredential;
use AzureOss\Storage\Blob\BlobServiceClient;
use GuzzleHttp\Psr7\Uri;

$credential = new ClientCertificateCredential(
    tenantId: getenv('AZURE_TENANT_ID'),
    clientId: getenv('AZURE_CLIENT_ID'),
    clientCertificatePath: getenv('AZURE_CLIENT_CERTIFICATE_PATH'),
    clientCertificatePassword: getenv('AZURE_CLIENT_CERTIFICATE_PASSWORD') ?: null,
);

$endpoint = new Uri('https://'.getenv('AZURE_STORAGE_ACCOUNT_NAME').'.blob.core.windows.net/');
$service = new BlobServiceClient($endpoint, $credential);
```

### Workload identity (federated credentials)

For Kubernetes or other OIDC-based federation scenarios, use `WorkloadIdentityCredential`.

Typical configuration uses:

- `AZURE_TENANT_ID`
- `AZURE_CLIENT_ID`
- `AZURE_FEDERATED_TOKEN_FILE`

Example:

```php
<?php

use AzureOss\Identity\WorkloadIdentityCredential;
use AzureOss\Storage\Blob\BlobServiceClient;
use GuzzleHttp\Psr7\Uri;

$credential = new WorkloadIdentityCredential();

$endpoint = new Uri('https://'.getenv('AZURE_STORAGE_ACCOUNT_NAME').'.blob.core.windows.net/');
$service = new BlobServiceClient($endpoint, $credential);
```

### Managed identity (experimental)

:::caution Experimental
`ManagedIdentityCredential` is experimental. This credential can be difficult to test reliably because most managed identity endpoints are only available from within the corresponding Azure runtime (IMDS, App Service/Functions, Arc, etc.). If you try this in a real environment and it works (or fails), please let us know which environment you used and any relevant HTTP status/error details.
:::

Example:

```php
<?php

use AzureOss\Identity\ManagedIdentityCredential;
use AzureOss\Storage\Blob\BlobServiceClient;
use GuzzleHttp\Psr7\Uri;

$credential = new ManagedIdentityCredential();

$endpoint = new Uri('https://'.getenv('AZURE_STORAGE_ACCOUNT_NAME').'.blob.core.windows.net/');
$service = new BlobServiceClient($endpoint, $credential);
```

## Notes

- Token-based credentials cannot generate SAS URLs in this SDK (`canGenerateSasUri()` returns `false`).
- For SAS-based workflows, use access keys instead.
