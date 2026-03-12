---
sidebar_position: 2
title: Shared access signature (SAS)
---

SAS (Shared Access Signature) lets you grant scoped, time-limited access without exposing your account key.


## Use A SAS URL

```php
use AzureOss\Storage\Blob\BlobClient;
use GuzzleHttp\Psr7\Uri;

$sasBlobClient = new BlobClient(new Uri((string) $blobSas));
$content = $sasBlobClient->downloadStreaming()->content->getContents();
```

## Generate A Blob SAS URL

```php
<?php

use AzureOss\Storage\Blob\BlobServiceClient;
use AzureOss\Storage\Blob\Sas\BlobSasBuilder;

$service = BlobServiceClient::fromConnectionString(getenv('AZURE_STORAGE_CONNECTION_STRING'));
$blob = $service->getContainerClient('quickstart')->getBlobClient('hello.txt');

$blobSas = $blob->generateSasUri(
    BlobSasBuilder::new()
        ->setPermissions('r')
        ->setExpiresOn(new \DateTimeImmutable('+15 minutes'))
);
```

## Generate A Container SAS URL

```php
use AzureOss\Storage\Blob\Sas\BlobSasBuilder;

$container = $service->getContainerClient('quickstart');

$containerSas = $container->generateSasUri(
    BlobSasBuilder::new()
        ->setPermissions('rl')
        ->setExpiresOn(new \DateTimeImmutable('+15 minutes'))
);
```

## Account SAS

```php
use AzureOss\Storage\Common\Sas\AccountSasBuilder;
use AzureOss\Storage\Common\Sas\AccountSasPermissions;
use AzureOss\Storage\Common\Sas\AccountSasResourceTypes;

$accountSas = $service->generateAccountSasUri(
    AccountSasBuilder::new()
        ->setPermissions(new AccountSasPermissions(list: true, read: true))
        ->setResourceTypes(new AccountSasResourceTypes(service: true, container: true, object: true))
        ->setExpiresOn(new \DateTimeImmutable('+15 minutes'))
);
```
