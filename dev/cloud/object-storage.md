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

This whole process is abstracted with some kind of interface, realised through a software daemon, that can be containerised and scaled. [Ceph][ceph], for example, uses a daemon with an Amazon S3 HTTP interface, and a backing database.

### Security

Without going too deep on this topic here, each provider has their own approach and there is no one way. Digital Ocean follows the Amazon S3 approach closely, but Google has their own approach. When the time comes, study the chosen platform closely, and model the authentication process.

Examples:

**IBM** uses an [API key and a token][ibm-curl].

[**Digital Ocean**][digital-ocean-authentication] aims to be compatible with Amazon S3 for all API requests -- including authentication. It uses a combination of an HTTP Authorisation header and [Amazon's Signature v4][amz-sig-v4]. It also makes use of a basic ACL, with roles for users and the public.

**Google** uses [IAM][google-iam] policy which defines roles and access -- to authenticated, and public users alike. They also allow conditional, role-based access based on object metadata -- like timestamp, type etc. [Signed URLs][google-signatures] can also be used to provide time-gated access to resources, along with a number of other approaches that provide a greater degree of security. [Cookie authentication][google-cookie-auth] is used where having a Google account is a requirement to access resources.

### Alternatives

**Block level storage** (raw file system blocks), and **file storage** are alternatives to storing binary data. Neither of these solutions are as scalable as object storage, but block level storage provides more performance and space efficiency.

### Solutions

Ceph, Minio, Openio.io, SwiftStack/OpenStack Swift -- all of which use the Amazon S3 protocol.

### Pricing

Pricing is usually volume based -- e.g. you pay per unit storage per month.

## Glossary

* [**IAM**](iam-cso): A general term that refers to a framework, or suite of technologies, that provides **identity and access management**.

## Sources

* [Authentication | Digital Ocean][digital-ocean-authentication]
* [Ceph | Wikipedia][ceph]
* [IAM | Google][google-iam]
* [IAM | SCO Online][iam-cso]
* [Curl Authentication | IBM][ibm-curl]
* [Choose the Right Data Store | Microsoft](https://docs.microsoft.com/en-us/azure/architecture/guide/technology-choices/data-store-overview)
* [Cookie Authentication | Google][google-cookie-auth]
* [Object Storage | IBM](https://www.ibm.com/cloud/learn/object-storage)
* [Signatures | Google][google-signatures]
* [Signature v4 | Amazon][amz-sig-v4]
* [What is Object Storage | Alibaba](https://www.alibabacloud.com/knowledge/what-is-object-storage)


[google-iam]: https://cloud.google.com/storage/docs/access-control/iam
[google-signatures]: https://cloud.google.com/storage/docs/authentication/signatures
[google-cookie-auth]: https://cloud.google.com/storage/docs/access-control/cookie-based-authentication
[ceph]: https://en.wikipedia.org/wiki/Ceph_(software)
[iam-cso]: https://www.csoonline.com/article/2120384/what-is-iam-identity-and-access-management-explained.html
[ibm-curl]: https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-curl#curl-token
[digital-ocean-authentication]: https://developers.digitalocean.com/documentation/spaces/#authentication
[amz-sig-v4]: https://docs.aws.amazon.com/general/latest/gr/signature-version-4.html
