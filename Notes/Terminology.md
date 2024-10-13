# Client
  This is who is responsible for performing CRUD operations. This is analogous to a user.

# CURD Operations
  This is an acronym for Create, Update, Read, Delete.

# Network Layer
  This is a part of the database system that allows it to communicate with a client. Databases usually run on a different server. However, some databases - like SQLite - are embeddable, meaning they can run in the same process as the rest of the client application.

# Query
  This is a request sent from a client to a database server.

# Parse Tree
  This is what a parser commonly outputs. This is an ordered collection of instructions the database needs to perform.

# Asset Properties
  Asset properties include atomicity, consistency, isolation, and durability. Not all databases have these properties, but most do.

# Lock
  A system may lock some information to avoid potential data inconsistencies by following multiple instructions at once.

# Concurrency
  This is an attribute of a database handling multiple transactions at the same time.
  
# MVCC (Multiversion Concurrency Control)
  This is a way to handle concurrent transactions.

# Persistence
  This is a property of storage media that means the data is kept when the power is removed or the database crashes. Disk is persistent; RAM is not.

# Page
  A disk drive is divided into sectors called pages. If we want to access information from the disk, we need to load the whole page into memory before we can perform any actions. We cannot directly process things on disk.