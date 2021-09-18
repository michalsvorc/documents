# MongoDB

Overview:

* [Documentation](https://docs.mongodb.com/)
* [Tutorial](https://www.tutorialspoint.com/mongodb/index.htm)

API:

* [Collection Methods](https://docs.mongodb.com/manual/reference/method/js-collection/)
* [MongoDB - Datatypes](https://www.tutorialspoint.com/mongodb/mongodb_datatype.htm)
* [Operators](https://docs.mongodb.com/manual/reference/operator/)
* [CRUD operations](https://docs.mongodb.com/manual/crud/)
* [Cursor methods](https://docs.mongodb.com/manual/reference/method/js-cursor/)

Topics:

* [Write Concern - MongoDB Manual](https://docs.mongodb.com/manual/reference/write-concern/)

## Concepts

Table => Collection
Row => JSON/BSON document
Column => Field

BSON is a binary serialization format used to store documents and make remote procedure calls in MongoDB. Max. size of
the BSON document is 16MB.

## Data types

* [Documentation](https://docs.mongodb.com/manual/reference/bson-types/)

* Double

  Double is more precise than float and can store 64 bits, double of the number of bits float can store.

* ObjectId

  In MongoDB, each document stored in a collection requires a unique
  [`_id`](https://docs.mongodb.com/manual/reference/glossary/#term-id) field that acts as a [primary
  key](https://docs.mongodb.com/manual/reference/glossary/#term-primary-key). If an inserted document omits the `_id`
  field, the MongoDB driver automatically generates an
  [ObjectId](https://docs.mongodb.com/manual/reference/bson-types/#objectid) for the `_id` field.

* Timestamps

  The BSON timestamp type is for internal MongoDB use. For most cases, in application development, you will want to use
  the BSON *Date* type.

* Date

  BSON Date is a 64-bit integer that represents the number of milliseconds since the Unix epoch (Jan 1, 1970).

* Numbers

  Double: `double`
  32-bit integer: `int`
  64-bit integer: `long`
  Decimal128 `decimal` (Use for precise calculations)

## Data models

* [Documentation](https://www.tutorialspoint.com/mongodb/mongodb_data_modeling.htm)

MongoDB provides two types of data models: 

- [embedded](https://docs.mongodb.com/manual/core/data-model-design/#data-modeling-embedding): embed all the related
  data in a *single document*
- [normalized](https://docs.mongodb.com/manual/core/data-model-design/#normalized-data-models): refer the sub documents
  in the original document, using references

Execute joins while writing, not on read. Implement complex aggregation in the schema.

## $set operator

* [Documentation](https://docs.mongodb.com/manual/reference/operator/update/set/)

The `$set` operator replaces the value of a field with the specified value. If the field does not exist, `$set` will add
a new field with the specified value, provided that the new field does not violate a type constraint.

## upsert

Mixes the functionality of update and insert.

When you execute an `update()` with upsert: true and the query matches no existing document, MongoDB will refuse to
insert a new document if the query specifies conditions on the `_id` field using [dot
notation](https://docs.mongodb.com/manual/core/document/#document-dot-notation).

