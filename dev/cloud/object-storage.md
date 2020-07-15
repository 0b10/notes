# Object Storage

## Notes

Object storage is a **cost-effective** storage solution for large amounts of **static** (unchanging) **unstructured** (uncategorised) **binary data**. This solution works well because it's scalable without limits (partly due to its flat hierarchy), can be distributed, and has disaster recovery options.

**Metadata** can be used to attach almost anything you need to data objects, and often have data related to analytics, retention policies, disaster recovery strategy data, content authenticity, or some other business related data attached to them.

Some problematic issues are that files cannot be edited and must be reuploaded, and that it is slower than block storage.

### Portability

**Portability** is possible because the de facto standard that most implementations adhere to is the Amazon S3 protocol. The is also the OpenStack Swift API that a number of implementations support.

### Use Cases

It is very commonly used within cloud based apps.

* media;
* web assets;
* archived data (very common);
* backups (very common);
* big data;
* analytics;

### How It Works

Objects are stored in an object database that has two tables -- the object directory table; the object storage table.  The object storage table is responsible for storing the data. The object directory table is responsible for storing the metadata, and is used to do lookups -- with the collection id, object id being a necessary columns. There are three indices that are optimised for lookups:

* the creation timestamp;
* collection id + pending action data [sic] + creation timestamp;
* object id + collection id;

For instance, you can do a lookup with the object and collection ids.

### Solutions

Ceph, Minio, Openio.io, SwiftStack/OpenStack Swift -- all of which use the Amazon S3 protocol.

### Pricing

**Pricing** is usually volume based -- e.g. you pay per unit storage per month.

## Sources

[Object Storage | IBM](https://www.ibm.com/cloud/learn/object-storage)
[Choose the Right Data Store | Microsoft](https://docs.microsoft.com/en-us/azure/architecture/guide/technology-choices/data-store-overview)
[What is Object Storage | Alibaba](https://www.alibabacloud.com/knowledge/what-is-object-storage)
