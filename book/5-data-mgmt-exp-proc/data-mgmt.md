# What Kinds of Data Management Solutions Are There, And Which One is Suitable for My Project?

Data comes from various sources, but it is up to us to manage it 
effectively on our side. So it is imperative for us to understand the 
different types of data management solutions and its suitability for 
different datatypes. These solutions include:

- Flat files (CSVs, Excels, SQLite, JSONs, etc.)
- Object storage (S3, minIO, GCS, etc.)
- Relational database (SQL and its variants, Microsoft Access, etc.)
- Non-relational database (Redis, MongoDB, Cassandra, etc.) 
  + This can also be divided into sub-types such as:
    * Key-value store
    * Wide-column store ("two-dimensional key-value store")
    * Document store
    * Graph database

## Flat Files

Flat files are the simplest form of a data management solution, and it 
is usually the data type used in ML/DL tutorials. This includes CSVs,
Excel files, JSONs and SQLite. This form of data is recommended if the 
dataset is small (< 10GB) and/or needs to be portable.

The use of CSVs, while still prevalent in many tutorials and projects,
is highly discouraged. CSVs doesn't store data types and would need to 
be implicitly inferred, which may cause problems when ingesting data 
into your model(s).

## Object Storage

Object storage is a data management solution that relies connecting 
with an API, whether local or remote, and stores data as blobs. This 
is especially suitable for image, audio and video files. This type can
also accomodate flat file storage, suitable for incoming data that come
in multiple files. This type of data management solution is usually 
provided directly by cloud providers (S3 from AWS, GCS from GCP, etc.),
or being provisioned by your organisation's administrators using 
self-hosted solutions like MinIO.

## Relational Database

This should be another familiar form of a data management solution. 
This includes various flavours of SQL servers (MySQL, PostgreSQL, 
MariaDB, etc.). SQLite is also deemed to be a relational database type.
This is highly recommended for data that can be kept in tabular form
as well as fairly large sizes (excluding SQLite) since they are 
designed to run under heavy load from multiple clients querying from 
the servers. This also makes having the data being up-to-date easier 
for users since all the querying is done from a single source of data.

## Non-relational Database

This type of data management solution is for the types of data that is
difficult to store in a structured form like within a SQL database. 
There are many forms of non-relational databases (key-value store, 
document store, wide-column store, graph, etc.), so this is the most 
sophisticated form. This is highly recommended if you need to build a 
data lake that requires high throughput of data into the database 
before processing it into a data warehouse

## Data Lakes vs Data Warehouses

These terms might be thrown around whenever you read about articles 
pertaining to data management, or ML/DL/AI in general. For the sake of 
brevity, you could define data lake as a location to store raw data, 
while a data warehouse can be defined as a location to store processed
data. Usually a data lake uses a non-relational database to store since
it is usually built for high-throughput, while you have different forms
of data management solutions for data warehouses depending on the needs
of the organisations or your clients.
