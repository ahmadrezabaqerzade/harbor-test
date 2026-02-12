# Data Volume
## What is it?
The data_volume is the persistent storage location. Even though Harbor runs inside 
Docker containers, the containers themselves are "ephemeral" 
(meaning they lose their data if they are deleted). 
This setting maps a folder on your physical server's hard drive into 
those containers so your data is saved forever.

## What gets stored here?
If you use the default /data, Harbor will create several sub-folders inside it:

* /data/registry: All your Docker images and OCI artifacts.

* /data/database: The actual PostgreSQL data files.

* /data/redis: Cached data and job states.

* /data/job_logs: Logs for background tasks (like image scanning).

* /data/ca_download: Root certificates for users to download.

## Crucial Advice for Production:
* 1.Disk Space: This directory will grow very fast as you push more Docker images. 
Ensure the partition where this folder sits has plenty of gigabytes 
(or terabytes) available.

* 2.Separate Partition: It is highly recommended to mount a separate, large disk 
or cloud volume to this path. If /data fills up your root partition (/), 
your entire Linux server might crash.

* 3.Permissions: Harbor's installation script will attempt to set the correct 
permissions on this folder, but you must ensure the user running the installation 
has sudo or root access to create and write to this path.

* 4.Backups: If you want to back up your Harbor instance, this is the folder you 
must back up. If you lose /data, you lose all your images and your database.
