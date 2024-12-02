
# Array : 
- An array can be thought of as a list within a single column.

# Struct : 
- A struct is similar to a table within a table.

- These complex data types have usability concerns, they are harder to query and harder to work with.

# Dimensions:
- Identifier Dimensions: Uniquely identify an entity, such as userid, device id, or SSN.
- Attributes: Aid in performing various types of analyses.

- Attributes comes in two types: 
    - Slowly changing : time dependent | painful | eg: favourite food
    - fixed : set in stone | immutable | one value | eg: birthday


# Data Modeling:
- The first step is understanding who will use the model.
- It’s challenging for GPT and LLMs to handle effectively, as it requires empathy and context awareness.
- Master data refres to the type of data that other data engineers, developers, and team members across the company rely on.

There are 3 types of dimensional data modeling:

# OLTP vs OLAP vs Master Data:
- OLTP | Online Transaction Processing : Used by software engineers, focued at one user or one person.
- OLAP | Online Analytical Processing : Typically used by data engineers, analyzing entire datasets or subsets of data.
- Master Data: A middle ground, encompassing both transactional and analytical data.


Mismatched needs result in reduced business value.

- Mismatching needs = less business value.

# OLAP and OLTP is a continuuum

Flow:
Production Database Snapshots → Master Data → OLAP Cubes → Metrics

- Production Data of an App: Includes transactional information like prices, listings, and availability, all modeled in a transactional way. Merge these datasets to create master data by combining all transactional datasets into a single table.

- Master Data: Consolidates transactional datasets into a unified, comprehensive structure, serving as a bridge between OLTP and OLAP.

- OLAP Cubes: In this stage, data flattening happens; there could be multiple rows for an entity. Grouping and slicing-and-dicing enable detailed analysis, a process loved by data analysts and data scientists.


# Cumulative Data Design:

- Commonly used for creating Master Data.
- Involves retaining all dimensions that ever existed, preserving history.
- Columns in two tables should be same (in yesterday and in today). 
- There is a point in cumulative data design where u want to restrict data - depends on company and business value.

Strengths:
- Enables historical analysis without needing GROUP BY (e.g., last 30 days of data in a single row, supporting massively scalable queries).

Drawbacks:
- Backfilling must be sequential (e.g., today depends on yesterday), making parallel backfills challenging.
- Handling PII can be complex.

# Compactness vs Usability tradeoff:

Goes back to OLTP and OLAP differences

Most usables tables
- Characteristics: No complex data types, identifiers for dimensions.
- Focus: Analytics-oriented, designed for OLAP cubes.

Most compact tables
- Characteristics: Contains identifiers and blobs of bytes, can't be queries directly until decoded.
- Focus: Software engineering, production data, and online systems.

Middle Ground Tables
- Characteristics: Utilize complex data types (e.g., structs, arrays, maps), balancing compactness and queryability.
- Focus: Master Data Layer.


# Struct vs Map vs Array:

Struct:
- Definition: A table within a table.
- Key Feature: Keys and values are defined; values can have different data types.

Map:
- Definition: A collection of key-value pairs.
- Key Feature: All values must be of the same data type; keys can be numerous (e.g., up to ~65k).

Array:
- Definition: A list of values.
- Key Feature: All values must be of the same data type.

# Temporal Carinality Explosion of Dimensions:

