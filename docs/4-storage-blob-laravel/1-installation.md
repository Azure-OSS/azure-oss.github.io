---
sidebar_position: 1
title: Installation
---

`azure-oss/storage-blob-laravel` integrates Azure Blob Storage with Laravel's filesystem.

## Requirements

- PHP 8.1+
- Laravel Filesystem (`illuminate/filesystem`) 10.x, 11.x, 12.x, or 13.x

## Install With Composer

```bash
composer require azure-oss/storage-blob-laravel
```

## Configure `config/filesystems.php`

Use either a connection string or token-based credentials.

Connection string:

```php
'azure' => [
    'driver' => 'azure-storage-blob',
    'connection_string' => env('AZURE_STORAGE_CONNECTION_STRING'),
    'container' => env('AZURE_STORAGE_CONTAINER'),
],
```

Token-based credentials (Microsoft Entra ID):

```php
'azure' => [
    'driver' => 'azure-storage-blob',
    'endpoint' => env('AZURE_STORAGE_ENDPOINT'),
    // or: 'account_name' => env('AZURE_STORAGE_ACCOUNT_NAME'),
    // optional with account_name: 'endpoint_suffix' => env('AZURE_STORAGE_ENDPOINT_SUFFIX', 'core.windows.net'),
    'tenant_id' => env('AZURE_STORAGE_TENANT_ID'),
    'client_id' => env('AZURE_STORAGE_CLIENT_ID'),
    'client_secret' => env('AZURE_STORAGE_CLIENT_SECRET'),
    'container' => env('AZURE_STORAGE_CONTAINER'),
],
```

## Next Step

Continue to [Quickstart](./quickstart) for common file operations with `Storage::disk('azure')`.
