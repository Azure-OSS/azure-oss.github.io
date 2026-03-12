---
sidebar_position: 3
title: Access Key
---

Access key authentication is the default when you connect using a storage account connection string.

:::warning
This feature is not released yet.
:::

## Option 1: Connection String (Recommended)

```php
<?php

use AzureOss\Storage\Blob\BlobServiceClient;

$service = BlobServiceClient::fromConnectionString(
    getenv('AZURE_STORAGE_CONNECTION_STRING')
);
```

For local development with Azurite, you can use:

```env
AZURE_STORAGE_CONNECTION_STRING="UseDevelopmentStorage=true"
```

`UseDevelopmentStorage=true` tells the SDK to connect to the local Azurite emulator instead of Azure Storage.

## Option 2: Explicit Endpoint + Shared Key

```php
<?php

use AzureOss\Storage\Blob\BlobServiceClient;
use AzureOss\Storage\Common\Auth\StorageSharedKeyCredential;
use GuzzleHttp\Psr7\Uri;

$credential = new StorageSharedKeyCredential(
    getenv('AZURE_STORAGE_ACCOUNT_NAME'),
    getenv('AZURE_STORAGE_ACCOUNT_KEY')
);

$endpoint = new Uri('https://'.getenv('AZURE_STORAGE_ACCOUNT_NAME').'.blob.core.windows.net/');
$service = new BlobServiceClient($endpoint, $credential);
```

## Verify SAS Capability

With shared key credentials, SAS generation is available:

```php
$container = $service->getContainerClient('quickstart');

if ($container->canGenerateSasUri()) {
    // generate container/blob SAS tokens
}
```
