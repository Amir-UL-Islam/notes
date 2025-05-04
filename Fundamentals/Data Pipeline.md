- A data pipeline is an automated process that extracts data from a source system, transforms it into a desired model, and loads the transformed data into a file, database, or other data storage tool. 
- Pipelines that extract, transform and load data are commonly referred to as ETL pipelines. Data pipelines are almost always automated, whether triggered by an event or a schedule.


> Resilient Pipeline
- Handle routine failures
 - Automatically retry on failures
 - Should Rerun Last Point of Failure
 
 > Idempotent
-  Can run multiple Time And Output remains same
- Should not contain Duplicate Values

> Scalable 
- High frequency of Invocation

> Transparency
- Avoid Black-Box Transformations
- Well-Tested and Documented

> Storing data to a file or other storage medium is known as data persistence.

> Data lineage is the practice of documenting the journey that data takes though a pipeline, from source to destination.

