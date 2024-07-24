# Get started

## Prerequisites

- PHP >=8.1
- ext-json
- ext-curl

## Set up your project

This section walks you through preparing a project to work with the Azure Storage SDK for PHP.

From your project directory, install packages for the Azure Storage SDK.

Install the library using [composer](https://getcomposer.org/)

```shell
composer require azure-oss/storage
```

## Authorize access

@TODO SAS vs Token

## Build your application

The following guides show you how to work with data resources and perform specific actions using the Azure Storage SDK.

| Guide                              | Description                                                                             |
| ---------------------------------- | --------------------------------------------------------------------------------------- |
| Create a container                 | Create containers.                                                                      |
| Delete and restore containers      | Delete containers, and if soft-delete is enabled, restore deleted containers.           |
| List containers                    | List containers in an account and the various options available to customize a listing. |
| Manage properties and metadata     | Get and set properties and metadata for containers.                                     |
| Create and manage container leases | Establish and manage a lock on a container.                                             |
| Create and manage blob leases      | Establish and manage a lock on a blob.                                                  |
| Append data to blobs               | Learn how to create an append blob and then append data to that blob.                   |
| Upload blobs                       | Learn how to upload blobs by using strings, streams, file paths, and other methods.     |
| Download blobs                     | Download blobs by using strings, streams, and file paths.                               |
| Copy blobs                         | Copy a blob from one location to another.                                               |
| List blobs                         | List blobs in different ways.                                                           |
| Delete and restore                 | Delete blobs, and if soft-delete is enabled, restore deleted blobs.                     |
| Find blobs using tags              | Set and retrieve tags, and use tags to find blobs.                                      |
| Manage properties and metadata     | Get and set properties and metadata for blobs.                                          |
| Set or change a blob's access tier | Set or change the access tier for a block blob.                                         |
