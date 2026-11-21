AWS Backup & Recovery Lab:
     A small hands-on project where I back up data on AWS, simulate data loss, and recover it.

Tools used
- Amazon S3 (versioning)
- Amazon EC2 (Ubuntu Server 22.04)
- Amazon Machine Image (AMI) for server backup

What I did:
Part 1: Recover a deleted file in S3
1. Created an S3 bucket and turned on "versioning".
2. Uploaded 'lab.txt' (version 1), then uploaded a changed copy (version 2). S3 kept both versions.
3. Deleted the file to simulate an accident. S3 added a "delete marker" instead of removing the data.
4. Removed the delete marker and the file came back

Two versions of the file: [screenshot- s3-versions.png]
File restored after removing the delete marker: [screenshot- s3-file-restored.png]

Part 2: Back up and restore an EC2 server
1. Launched an Ubuntu server on EC2.
2. Created a folder 'company-data' with a file 'records.txt' containing sample data.
3. Created an **AMI** (a full backup image of the server).
4. Deleted the 'company-data' folder to simulate data loss.
5. Launched a new server from the AMI. The folder and file were back

AMI available [screenshot- ami-available.png]
Restored-data [screenshot- restored data.png]

Commands used on the server:

mkdir ~/company-data
echo "Customer records - important" > ~/company-data/records.txt
cat ~/company-data/records.txt
rm -rf ~/company-data

My Learning:
- Versioning protects against accidental deletes and overwrites.
- A delete in a versioned bucket only adds a delete marker, so it can be undone.
- An AMI saves a full copy of a server, which can be used to rebuild it after a failure.
- The restored server had the same data because it started from the backup, not from a fresh image.
- Backups should be tested. A backup that has never been restored isn't proven to work.
