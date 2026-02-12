# Storage Service

## 1. The Storage Backend (filesystem vs. Others)
By default, Harbor uses your local disk (filesystem). However, 
if you are running Harbor in a professional cloud environment, 
you might want to use Object Storage.

* Supported Backends: S3 (AWS), GCS (Google), Azure, Swift (OpenStack), and 
OSS (Alibaba).

* **Why use Cloud Storage?** If your server crashes, your images are safe in 
the cloud. It also makes it much easier to scale Harbor.

## 2. ca_bundle
If you connect Harbor to a private cloud storage (like a local MinIO server) 
that uses a self-signed certificate, Harbor's internal components won't trust 
it by default.

* You put the path to your Root CA certificate here so Harbor knows 
the connection is safe.

## 3. maxthreads
This is specific to the filesystem driver. It defines how many simultaneous 
"workers" can read or write data to the disk.

* 100 is the default. If you have extremely fast NVMe drives, you might increase 
this; if you have very slow mechanical disks, you might lower it to prevent the 
disk from "choking."

## 4. redirect: disable
This is a very clever setting.

* If false (Default): When a user pulls an image, Harbor tells the Docker 
client: "Go download the data directly from S3/Azure." This saves Harbor's bandwidth.

* If true: Harbor downloads the data from the cloud first, then passes it to the 
user. You only do this if your Harbor server is in a restricted network where 
users can't "see" the external cloud storage directly.

|Storage Type|Best For...|Reliability|
|:-:|:-:|:-:|
|Filesystem|Local testing, small teams, single-server setups.|Moderate (limited by disk)|
|S3 / GCS / Azure|Production, High Availability, large teams.|Very High|
