# Storage

- [System Design - medium.com](https://medium.com/must-know-computer-science/system-desing-storage-d8ef4a8d952c)

The main types of storage that are used widely nowadays are File Storage, Block Storage, and Object Storage.

## File Storage

Store data as files and present it to its final users as a hierarchical directories structure. The main advantage is to
provide a user-friendly solution to store and retrieve files.

## Block Storage

Block storage chops data into blocks (chunks) and stores them as separate pieces.

Data is stored in blocks of uniform size, it is ideal for data that needs to be accessed and modified frequently as it
provides low-latency. However, it is expensive, complex, and less scalable compared with File Storage.

## Object storage

It was created in the cloud computing industry with the requirement of storing vast amounts of unstructured data.

Data is stored as objects with unique metadata and identifiers. Although, in general, this type of storage is less
expensive, but the objects can’t be modified — you have to write the object completely at once.
