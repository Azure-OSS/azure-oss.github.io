# Flysystem

To easily integrate within your application we suggest using [Flysystem](https://flysystem.thephpleague.com/). This
library has a native adapter available to integrate with the Azure-OSS Storage SDK.

## Installation

```shell
composer require league/flysystem-azure-oss:^1.0
```

## Usage

Below is a simple example how to start using the Flysystem adapter. More information can be found on the `Flysystem`
documentation page

```php
<?php

require('vendor/autoload.php');

use AzureOss\FlysystemAzureBlobStorage\AzureBlobStorageAdapter;
use AzureOss\Storage\Blob\BlobServiceClient;
use League\Flysystem\Filesystem;

include __DIR__ . '/vendor/autoload.php';

$client = BlobServiceClient::fromConnectionString(
    # Replace below DSN
    'DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;BlobEndpoint=http://azurite:10000/devstoreaccount1;QueueEndpoint=http://azurite:10001/devstoreaccount1;TableEndpoint=http://azurite:10002/devstoreaccount1;'
)->getContainerClient('your-container-name');

$adapter = new AzureBlobStorageAdapter(
    $client,
);
$filesystem = new Filesystem($adapter);

$filesystem->write('./your-demo-file', 'your-demo-content');
```
