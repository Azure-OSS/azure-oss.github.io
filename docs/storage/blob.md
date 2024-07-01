# Blob

## Container

### createContainer

Create a new container inside the storage account

[https://learn.microsoft.com/en-us/rest/api/storageservices/create-container](https://learn.microsoft.com/en-us/rest/api/storageservices/create-container)

```php
public function createContainer(string $container, ?CreateContainerOptions $options = null): CreateContainerResponse;
```

### getContainerProperties

Get the container metadata by its container name

[https://learn.microsoft.com/en-us/rest/api/storageservices/get-container-properties](https://learn.microsoft.com/en-us/rest/api/storageservices/get-container-properties)

```php
public function getContainerProperties(string $container, ?GetContainerPropertiesOptions $options = null): GetContainerPropertiesResponse;
```

### deleteContainer

Remove a container by name

[https://learn.microsoft.com/en-us/rest/api/storageservices/delete-container](https://learn.microsoft.com/en-us/rest/api/storageservices/delete-container)

```php
public function deleteContainer(string $container, ?DeleteContainerOptions $options = null): DeleteContainerResponse;
```

### containerExists

Verify if a container exists

```php
public function containerExists(string $container): bool;
```

## Blob

### listBlobs

List all blobs from a storage container

[https://learn.microsoft.com/en-us/rest/api/storageservices/list-blobs](https://learn.microsoft.com/en-us/rest/api/storageservices/list-blobs)

```php
public function listBlobs(string $container, ?ListBlobsOptions $options = null): ListBlobsResponse;
```

| Syntax     | Description | Optional |
|------------|-------------|----------|
| prefix     | string      | yes      |
| marker     | string      | yes      |
| maxResults | integer     | yes      |
| delimiter  | string      | yes      |

### putBlob

https://learn.microsoft.com/en-us/rest/api/storageservices/put-blob

### blobExists

### getBlob

https://learn.microsoft.com/en-us/rest/api/storageservices/get-blob

### deleteBlob

https://learn.microsoft.com/en-us/rest/api/storageservices/delete-blob

### getBlobProperties

https://learn.microsoft.com/en-us/rest/api/storageservices/get-blob-properties

### copyBlob

https://learn.microsoft.com/en-us/rest/api/storageservices/copy-blob

## Block

### putBlock

https://learn.microsoft.com/en-us/rest/api/storageservices/put-block

### uploadBlockBlob

### putBlockList

https://learn.microsoft.com/en-us/rest/api/storageservices/put-block-list
