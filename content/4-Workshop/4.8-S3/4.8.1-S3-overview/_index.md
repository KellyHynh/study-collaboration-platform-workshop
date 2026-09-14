---

title: "Amazon S3 Overview"

date: 2026-09-14

weight: 1

chapter: false

pre: " <b> 4.8.1. </b> "

---

# Amazon S3 Overview

#### 4.8.1.1. Role of Amazon S3

Amazon S3 (Simple Storage Service) is used in KnoVerse as an object storage service for storing uploaded files and application assets.

The system separates structured application data from file-based data.

![ALB as CloudFront Origin](images/4-Workshop/4.8-S3/1.png)

Amazon RDS PostgreSQL is responsible for structured relational data such as course information, lessons, quizzes, questions, and related metadata. Amazon S3 is used to store files and objects such as course thumbnails.

For example, instead of storing the binary image directly inside PostgreSQL, the database can store an object key:

thumbnailKey =
courses/thumbnails/course-react.png

while the actual image is stored in S3. This separation makes the storage architecture more appropriate for different types of data and allows the object storage layer to be extended in the future.

#### 4.8.1.2. S3 Use Case in KnoVerse

The initial S3 use case is course asset storage, specifically course thumbnails.

The initial object structure is:

knoverse-assets-2026/
└── courses/
    └── thumbnails/
        └── course-react.png

The structure can later be extended to support other uploaded resources:

knoverse-assets-2026/
├── courses/
│   └── thumbnails/
├── lessons/
├── materials/
└── users/

At the current implementation stage, the objective is to establish the S3 infrastructure, configure secure access, and verify that the EC2 backend can access the bucket through an IAM Role.


