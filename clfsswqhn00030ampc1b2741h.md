---
title: "MongoDB time series collection in C#"
datePublished: Tue Mar 28 2023 21:59:50 GMT+0000 (Coordinated Universal Time)
cuid: clfsswqhn00030ampc1b2741h
slug: mongodb-time-series-collection-in-csharp
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/yD5rv8_WzxA/upload/f52a6d04bd2d2cee8de80f711f1f2f59.jpeg
tags: csharp, mongodb, dotnet

---

In this blog post, I will introduce the time-series collection type of MongoDB, which was added to MongoDB in recent years. This collection type has many uses in many IoT scenarios. But before I bring out the time series collection type, I will briefly introduce MongoDB and the time series collection idea.

MongoDB is a popular open-source document-oriented database that stores data in JSON-like format. In contrast to traditional relational databases, which use tables and rows to organize data, MongoDB uses collections and documents. A collection is a group of documents that share a common schema or structure, and a document is a record of data that consists of key-value pairs. MongoDB is designed to be scalable, flexible, and high-performance. Some of the features of MongoDB include:

* Dynamic schema: MongoDB does not enforce a fixed schema for the documents in a collection. This allows the data model to evolve over time and accommodate different types of data.
    
* Indexing: MongoDB supports various types of indexes to optimize queries and ensure data integrity. Indexes can be created on any field or combination of fields in a document, and can also be geospatial, text, or hashed.
    
* Aggregation: MongoDB provides a powerful aggregation framework that allows complex data analysis and manipulation. The aggregation pipeline consists of stages that process the documents in a collection and output the aggregated results. The aggregation framework supports various operators such as match, group, sort, project, unwind, and look up.
    
* Replication: MongoDB supports replication to provide high availability and data redundancy. Replication is achieved by using replica sets, which are groups of MongoDB servers that maintain the same data set. One server in the replica set acts as the primary, which receives all write operations and replicates them to the other servers, called secondaries. If the primary fails, one of the secondaries is elected as the new primary automatically.
    
* Sharding: MongoDB supports sharding to provide horizontal scaling and distribute data across multiple servers. Sharding is the process of partitioning the data in a collection into smaller chunks, called shards, and assigning them to different servers, called shard servers. Sharding allows MongoDB to handle large data sets and high throughput operations by balancing the load and increasing the capacity of the cluster.
    

A time-series collection type is a data structure that stores a sequence of values that are associated with timestamps. A time-series collection type can be used to represent various kinds of temporal data, such as sensor readings, stock prices, weather measurements, or user activity logs. A time-series collection type can support various operations, such as querying, aggregating, filtering, or transforming the data based on the timestamps or the values. A time-series collection type can also enable efficient storage and retrieval of the data by using compression techniques or indexing strategies that exploit the temporal properties of the data. MongoDB has added this feature since version 5.

The MongoDB time-series collection benefits from a specialized schema design that optimizes the storage and performance of time-series data. A time-series collection stores measurements or events that track changes over time, such as sensor data, stock prices, or website activity. By using a time-series collection, you can take advantage of the following benefits:

* Improved query efficiency: MongoDB automatically creates indexes on the time field and the metadata field of a time-series collection, which can speed up common queries on time-series data.
    
* Reduced storage space: MongoDB compresses the measurements or events in a time-series collection using a lossless compression algorithm, which can save up to 80% of storage space compared to a normal collection.
    
* Simplified schema design: MongoDB abstracts the schema design of a time-series collection, so you don't have to worry about creating buckets or chunks for your data. You only need to specify the time field, the metadata field, and the granularity of the data.
    

## See the MongoDB time series collection in action

MongoDB time series collection needs at least MongoDB server version 5.

### Install required packages

You need to install the MongoDB driver package from NuGet to connect MongoDB server.

```bash
dotnet add package MongoDB.Driver --version 2.19.1
```

### Create a time-series collection

Making new a collection in MongoDB is very simple and usually does not need to Create a collection because, at first insert, MongoDB automatically creates a collection. However, Creating a time-series collection from code needs setting some options which inform the server that this collection is a time-series.

```csharp
if (!await IsCollectionExist(CollectionName, database))
{
    var options = new CreateCollectionOptions { TimeSeriesOptions = new TimeSeriesOptions("time") };
    await database.CreateCollectionAsync(CollectionName, options);
}
```

Inserting data like normal MongoDB action, but you should have eyes on the Time property because if the Time property equals `null` MongoDB could not save the data and returned the error with this message `"'Time' must be present and contain a valid BSON UTC datetime value"` . You can see an example of inserting data below.

```csharp
    await collection.InsertOneAsync(new Temperature
    {
        TemperatureValue = Random.Shared.Next(),
        Time = DateTime.UtcNow
    });
```

Moreover, You can read data from a collection in the same way as reading data from a normal collection. For example

```csharp
await (await collection.FindAsync(FilterDefinition<Temperature>.Empty)).ToListAsync();
```

However, Delete and update actions have some limits which you can read on [MongoDB documentation](https://www.mongodb.com/docs/v5.0/core/timeseries/timeseries-limitations/#updates-and-deletes). Nevertheless, these limits are not the only ones and you can find the complete list in [the documentation](https://www.mongodb.com/docs/v5.0/core/timeseries/timeseries-limitations/).

## Sum up

To make a long story short, the Time-series collection type has some limitations which make working with the become uneasy. On the other hand, this type has many benefits which make it a good storage option for many IoT applications such as optimum query and storage usage. I showed an example of how could you work with C# in this post. And you can see the full code of this post on [GitHub](https://github.com/behroozbc/MongoDbTimeCollectionBlogPost). If you have any questions about it you can ask them in the comments.