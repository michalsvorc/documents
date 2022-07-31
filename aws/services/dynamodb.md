# DynamoDB

- [Low-Level API Reference](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/CurrentAPI.html)
- [Reserved Words in DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/ReservedWords.html)
- [Limits and Quotas](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Limits.html)
- [Best Practices](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html)

## Resources

- [Docker image - dynamodb-local](https://hub.docker.com/r/amazon/dynamodb-local)

## SDK for JavaScript v3

- [client-dynamodb](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-dynamodb/index.html)
- [client-dynamodb-streams](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-dynamodb-streams/index.html)
- [lib-dynamodb](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/modules/_aws_sdk_lib_dynamodb.html)
- [util-dynamodb](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/modules/_aws_sdk_util_dynamodb.html)

## Articles

- [(Video) Data modeling with Amazon DynamoDB (CMY304)](https://www.youtube.com/watch?v=DIQVJqiSUkE)
- [(Video) Advanced design patterns (DAT403-R1)](https://www.youtube.com/watch?v=6yqfmXiZTlM)

## Conditions

- [Condition API](https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_Condition.html)
- [Condition Expressions](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ConditionExpressions.html)
- [Comparison Operator and Function Reference](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.OperatorsAndFunctions.html)

## Remember

- `ADD` - Update expression for Updating Numbers and Sets. In general, we recommend using SET rather than ADD.
- Data shape: Instead of reshaping data when a query is processed (as an RDBMS system does), a NoSQL database organizes
  data so that its shape in the database corresponds with what will be queried.

## Local instance

```console
$ docker run --rm -p 4000:8000 --name dynamodb-local amazon/dynamodb-local
```

## Capacity units

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/ProvisionedThroughput.html)

DynamoDB calculates the number of read capacity units consumed based on item size, not on the amount of data that is
returned to an application. For this reason, the number of capacity units consumed is the same whether you request all
of the attributes (the default behavior) or just some of them (using a projection expression). The number is also the
same whether or not you use a filter expression.

## Partitions

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.Partitions.html)

Partition key defines primary index. Build filtering into your Primary key. For items with a given partition key value, DynamoDB stores these items close together, in sorted order by sort key value.

### Partition Key and Sort Key

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.Partitions.html#HowItWorks.Partitions.CompositeKey)

If the table has a composite primary key (partition key and sort key), DynamoDB calculates the hash value of the
partition key in the same way as described in Data Distribution: Partition Key. However, it stores all the items with
the same partition key value physically close together, ordered by sort key value.

Group objects that satisfy the primary access pattern together in partition. We decorate them with additional
attributes, which we're going to index for secondary access patterns.

## Secondary indexes

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/SecondaryIndexes.html)
- [Difference between local and global indexes in DynamoDB](https://stackoverflow.com/questions/21381744/difference-between-local-and-global-indexes-in-dynamodb)

A secondary index is a data structure that contains a subset of attributes from a table, along with an alternate key to
support Query operations. You can retrieve data from the index using a Query, in much the same way as you use a Query
with a table. A table can have multiple secondary indexes, which give your applications access to many different query
patterns.

Every write updates secondary indexes, so index only data you need.

### LocalSecondaryIndex (LSI)

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/LSI.html)

An index that has the same partition key as the base table, but a different sort key. A local secondary index is "local"
in the sense that every partition of a local secondary index is scoped to a base table partition that has the same
partition key value.

## GlobalSecondaryIndex (GSI)

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GSI.html)

An index with a partition key and a sort key that can be different from those on the base table. A global secondary
index is considered "global" because queries on the index can span all of the data in the base table, across all
partitions. A global secondary index is stored in its own partition space away from the base table and scales separately
from the base table.

GSIs are generally recommended unless you have a justified need to support strong consistency. Again, don’t build
indexes you don’t need – they will consume capacity.

In a DynamoDB table, each key value must be unique. However, the key values in a global secondary index do not need to
be unique.

Only the items with the specified key values appear in the response. Within that set of data, the items are in no
particular order.

A global secondary index only tracks data items where its key attributes actually exist.

### Attribute Projections

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GSI.html#GSI.Projections)

A projection is the set of attributes that is copied from a table into a secondary index. The partition key and sort key
of the table are always projected into the index.

## Access keys

Create new users in the IAM management dashboard with Programmatic access.

1. Attach existing policies directly > Create policy button
2. Service > DynamoDB
3. Actions > select actions
4. Resources > table > add table ARN

After user creation, you will see `Access key ID` and `Secret access key`

## Queries

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Query.html)

A filter expression cannot contain partition key or sort key attributes. You need to specify those attributes in the key
condition expression, not the filter expression.

A filter expression removes items from the Query result set. If possible, avoid using Query where you expect to retrieve
a large number of items but also need to discard most of those items.

If possible, avoid using Query where you expect to retrieve a large number of items but also need to discard most of
those items. If LastEvaluatedKey is present in the response and is non-null, you must paginate the result set.

### Paginating Table Query Results

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Query.Pagination.html)

To determine whether there are more results: if the result contains a **LastEvaluatedKey** element and it's non-null.

## Transactions

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/transactions.html)

## DAX

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DAX.html)

DAX is a DynamoDB-compatible caching service that enables you to benefit from fast in-memory performance for demanding
applications.

## Projection Expressions - Amazon DynamoDB

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ProjectionExpressions.html)

Amazon DynamoDB returns all the item attributes by default. To get only some, rather than all of the attributes, use a
projection expression.

### Expression Attribute Names in DynamoDB - Amazon DynamoDB

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ExpressionAttributeNames.html)

```console
--projection-expression "#c" \
--expression-attribute-names '{"#c":"Comment"}'
```

### Expression Attribute Values - Amazon DynamoDB

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ExpressionAttributeValues.html)

```console
--filter-expression "contains(Color, :c) and Price &lt;= :p" \
--expression-attribute-values file://values.json
```

values.json:

```json
{
  ":c": { "S": "Black" },
  ":p": { "N": "500" }
}
```

## Monitoring and Troubleshooting Best Practices

- Check the AWS error code returned from your operations and include in your application logs.
- Enable CloudTrail so that DynamoDB control operations (create table, update table, etc.) are available for later
  analysis.
- Use the CloudWatch metrics provided by DynamoDB to monitor table performance.
- Set alarms for pertinent metrics out of acceptable range.

## Expiring Items By Using DynamoDB Time to Live (TTL) - Amazon DynamoDB

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/TTL.html)

Amazon DynamoDB Time to Live (TTL) allows you to define a per-item timestamp to determine when an item is no longer
needed. Shortly after the date and time of the specified timestamp, DynamoDB deletes the item from your table without
consuming any write throughput.

## Items

- [Item Sizes and
  Formats](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/CapacityUnitCalculations.html)
- [Working with Items and Attributes - Amazon
  DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/WorkingWithItems.html)
- [Conditional
  Writes](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/WorkingWithItems.html#WorkingWithItems.ConditionalUpdate)

The maximum item size in DynamoDB is 400 KB, which includes both attribute name binary length (UTF-8 length) and
attribute value lengths (again binary length). The attribute name counts towards the size limit.

We recommend that you choose shorter attribute names rather than long ones. This helps you reduce the amount of storage
required, but also can lower the amount of RCU/WCUs you use.

## Optimistic Locking with Version Number

Use optimistic locking with a version number as described below to make sure that an item has not changed since the last
time you read it. This approach is also known as the read-modify-write design pattern or optimistic concurrency control.

Maintain a version number to check that the item has not been updated between the last read and update.

1. Read the item and remember the version number (versionNum = 0).
2. Make the state transition in memory after validating information (accountLocked = N if currentLoginTime >
lastFailedLoginTime + 24 hours).
3. Increment the version number (versionNum = 1).
4. Write the item with updated attributes (accountLocked = N and versionNum = 1). Use a conditional expression to
perform a write only if the item has not changed since it was last read.
5. If the condition fails, start over from step 1.
