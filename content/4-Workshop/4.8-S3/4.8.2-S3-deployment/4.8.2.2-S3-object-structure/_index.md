---

title: "Create Object Structure"
date: 2026-09-14
weight: 2
chapter: false
pre: " <b> 4.8.2.2. </b> "

---

# Create Object Structure

After creating the bucket, an object structure is created to organize course assets.

#### Step 1: Open the Bucket

Navigate to:

S3 → Buckets → knoverse-assets-2026

#### Step 2: Create the Courses Prefix

Click Create folder and create:

courses/

#### Step 3: Create the Thumbnails Prefix

Open the courses/ folder and create:

thumbnails/

The resulting structure is:

knoverse-assets-2026/
└── courses/
    └── thumbnails/

Although the S3 console displays these as folders, S3 stores objects using keys and prefixes. The structure therefore provides a logical organization for uploaded objects.

Evidence 4.8.2.2: Screenshot showing the courses/thumbnails/ structure.

