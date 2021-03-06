This document briefly introduces the running environment and basic operations of the command line tool.

## Environment Requirements

Python interpreter: Python 2.7

Dependent libraries: 

- cas_python_sdk (included)
- pyaml
- ordereddict

## Installation and Deployment

The command line tool `cascmd.py` used for performing basic operations for CAS is provided in the Python SDK package of CAS. Install the Python SDK to complete the installation of the command line tool. [Get a Python SDK](https://github.com/tencentyun/cas_python_sdk/tree/v1.0.0)

- Install the SDK via pip

``` shell
pip install cassdk
```

- Install via SDK source code

``` shell
python setup.py install
```

## Verifying the Installation

``` shell
cascmd.py -h
```

If the subcommand list is returned, the installation is successful.

## Getting Help

### Command options

You can use the following command to get the list of supported subcommands.

``` shell
cascmd.py -h
```
You can use the following command to get the descriptions of related subcommand parameters.
``` shell
cascmd.py <subcommand> -h
```

### Example

To get detailed help information on `create_job`, execute the following:

``` shell
cascmd.py create_job

```

The help information is output as follows:

``` shell
usage: cascmd.py create_job [-h] [--start START] [--size SIZE] [--desc DESC]
                            [--tier TIER] [--endpoint ENDPOINT]
                            [--appid APPID] [--secretid SECRETID]
                            [--secretkey SECRETKEY]
                            [--config-file CONFIG_FILE]
                            vault [archive_id]

positional arguments:
  vault                 format cas://vault-name
  archive_id            ID of archive to be downloaded. If not provided, an
                        inventory-retrieval job will be created

optional arguments:
  -h, --help            show this help message and exit
  --start START         start position of archive to retrieve, default to be 0
  --size SIZE           size to retrieve, default to be (totalsize - start)
  --desc DESC           description of the job
  --tier TIER           The retrieval option to use for the archive retrieval.
                        Standard is the default value used.
  --endpoint ENDPOINT   endpoint, e.g. cas.ap-chengdu.myqcloud.com
  --appid APPID         appid, please refer to https://console.cloud.tencent.com/capi
  --secretid SECRETID   secretid, please refer to
                        https://console.cloud.tencent.com/capi
  --secretkey SECRETKEY
                        secretkey, please refer to
                        https://console.cloud.tencent.com/capi
  --config-file CONFIG_FILE
                        configuration file

```

## Configuration of Information

If you are using cascmd.py **for the first time**, configure the CAS access information:

``` shell
cascmd.py config --endpoint HOST --appid APPID --secretid SECRETID --secretkey SECRETKEY [--config-file CONFIG_FILE] 

```

**Parameter description**:

| Parameter | Description |
| ----------- | ---------------------------------------- |
| HOST | The access address of the CAS service, which takes the form of `cas.<Region>.myqcloud.com`. The values available for Region are `ap-chengdu`, `ap-guangzhou`, `ap-beijing`, and `ap-shanghai`. |
| APPID | A unique user ID assigned to each developer when he or she accesses the CAS service. It is generated by the system automatically after the successful application for CAS. Get APPID from [here](https://console.cloud.tencent.com/developer) |
| SECRETID | The key ID owned by a developer. Get SECRETID from [here](https://console.cloud.tencent.com/capi) |
| SECRETKEY | The signing key value owned by a developer. Get SECRETKEY from [here](https://console.cloud.tencent.com/capi) |
| CONFIG_FILE | Specifies the location of the file storing the access information. It is saved under your home directory by default with the name of .cascmd_credentials. |

## Creating a Vault

### Command options

``` shell
cascmd.py create_vault cas://vault-name

```

### Return value

``` shell
Vault Location: /12xxxxxxxx/vaults/vault-name
0.087(s) elapsed

```

**Note**: "cas://" is the prefix identifier of a vault. Add it when you need to make reference to a vault in the cascmd tool.

## Deleting a Vault

### Command options

``` shell
cascmd.py delete_vault cas://vault-name 

```

### Return value

``` shell
Delete success

```

**Note**: If the vault is not empty, the deletion will fail and the following message will be returned:

``` shell
Error Headers:
[('content-length', '120'), ('x-cas-requestid', 'NTlhNTE5MDRfNGM5ZTU4NjRfN2YyY183NzOQ=='), ('server', 'nginx'), ('connection', 'keep-alive'), ('date', 'Tue, 29 Aug 2017 07:34:28 GMT'), ('content-type', 'application/json')]
Error Body:
{
   "code" : "BadRequest",
   "message" : "vault is not empty, only empty vault can be delete",
   "type" : "Client"
}

Error Status:
400
Failed!
```

## Uploading an Archive

### Command options

Use the following command to upload a local file to CAS while specifying the vault for the archive.

```shell
cascmd.py upload cas://vault-name [local-file-name]
```

### Return value

The archive ID will be returned when the upload is successful. Only the archive ID can be used to perform operations on an archive. By default, the name of the local file is written to the archive description, and cannot be used to perform an operation on an archive.

```
Archive ID: ikMDFA46zWpP6tez5EJb6Bc8Asqd7_HCqCt7c_MaPkqgCqrsFc8ZChsR13rDgO_xxxxxxxxxxxxx

```

**Notes**:

1. If you have uploaded the same file multiple times, different archive IDs are generated, and previous archives will not be overwritten. As such, the archive ID is the only basis for performing operations on an archive, and not the local file name.
2. The CAS service allows multipart upload, that is, a file larger than 100 MB will be automatically split into multiple parts for multipart uploading. This method returns the following message:

``` shell
File larger than 100MB, multipart upload will be used
Use 7 parts with partsize 16.00 MB to upload
MultiPartUpload ID: 1A1S1RrfNxVuIYCcnL21OyqZLB7cTJVL8WHC8pjQYLP6CNqOXLK3tMmI3v792ji3
Uploading part 1...

Upload success

Uploading part 2...

...

68.048(s) elapsed
```
The MultipartUpload ID can be used to resume upload from breakpoint if the transmission fails due to a network interruption or other reasons. Assume that the file upload above is interrupted at part 2,

``` shell
cascmd.py upload cas://vault-name [local-large-file] --upload_id 1A1S1RrfNxVuIYCcnL21OyqZLB7cTJVL8WHC8pjQYLP6CNqOXLK3tMmI3v792ji3

```

the following is output after the transmission is resumed from breakpoint:

``` shell
Resume last upload with partsize 16.00MB
Uploading part 2 ...

...

Upload success
Archive ID: tICk7wdqQB9YdCg3zoWblY4YJND4H5tqdvJipmWNR-uHOK3JqGKS6JDcDPMwJAjDTRwXcUZyBTS5dzixWOxMwPCHR8cWDzRaRYAO8_ZLhQu8Wl0C66pPBZRyTIYR7aTk
60.592(s) elapsed

```

**Note**: The partsize here is 16 MB by default, and can be manually set to a multiple of 16 MB.

``` shell
cascmd.py upload cas://vault-name [local-file-name] -p 32M

```

## Deleting an Archive

### Command options

Executing the following command deletes an uploaded archive. You need to specify the vault and ID of the archive in the parameters.

``` shell
cascmd.py delete_archive cas://vault-name ikMDFA46zWpP6tez5EJb6Bc8Asqd7_HCqCt7c_MaPkqgCqrsFc8ZChsR13rDgO_xxxxxxxxxxxxx

```

### Return value

``` shell
Delete success
0.092(s) elapsed

```

## Retrieving an Archive

### Step 1: Initiate a retrieval job

#### Command options

Create an archive download job using create_job.

```shell
cascmd.py create_job cas://vault-name <archive-id> [--start START] [--size SIZE] [--tier TIER]
```

Descriptions of parameters:

- archive-id: ID of archive to be downloaded
- START: Downloading begins from the START location of the archive
- SIZE: Specifies the size of the data to be downloaded
- TIER: Archive retrieval can be performed in three modes: Expedited (a job takes 1-5 minutes to complete), Standard (a job takes 3-5 hours to complete), and Bulk (a job takes 5-12 hours to complete)

**Note**: Expedited mode is only applicable for files no larger than 256 MB.

#### Example

Retrieve the archives from 32 MB to 128 MB in expedited mode.

```shell
cascmd.py create_job cas://vault-name <archive-id> --start 32M --size 96M --tier Expedited
```

### Step 2: Query job status

#### Command options

An inventory job normally takes 3-5 hours. Use the returned job ID to query the running status of a job:

```shell
cascmd.py desc_job cas://vault-name <job-id>
```

### Step 3: Get the content of a job

#### Command options

After running a job, use the subcommand `fetch_job_output` to retrieve the downloaded content to a local file.

```shell
cascmd.py fetch_job_output cas://vault-name <job-id> <local-file-name>
```

## Retrieving an archive list

### Step 1: Initiate a retrieval job

#### Command options

Execute the following command to create an archive list retrieval job for a vault. The job results in a list of all archives in the specified vault.

``` shell
cascmd.py create_job cas://vault-name

```

#### Returned value

```
inventory-retrieval job created, job ID: E-nVoA6erIw71cTwI4gY6kaYpCrV1ehUrqXCkDHNfObQSfkqk_f5KyeKcxVvo--8
Use

    cascmd.py fetch cas://vault-name E-nVoA6erIw71cTwI4gY6kaYpCrV1ehUrqXCkDHNfObQSfkqk_f5KyeKcxVvo--8 <local_file>

to check job progress and download the data when job finished
NOTICE: Jobs usually take about 4 HOURS to complete.
0.100(s) elapsed
```

### Step 2: Query job status

#### Command options

An inventory job normally takes 3-5 hours. Use the returned job ID to query the running status of a job:
``` shell
cascmd desc_job cas://vault-name E-nVoA6erIw71cTwI4gY6kaYpCrV1ehUrqXCkDHNfObQSfkqk_f5KyeKcxVvo--8
```
#### Returned value

The output of querying the job running status:

```shell
JobId: E-nVoA6erIw71cTwI4gY6kaYpCrV1ehUrqXCkDHNfObQSfkqk_f5KyeKcxVvo--8
Action: InventoryRetrieval
StatusCode: InProgress
StatusMessage: InProgress
ArchiveId: None
ArchiveSizeInBytes: None
SHA256TreeHash: None
ArchiveSHA256TreeHash: None
RetrievalByteRange: None
Completed: False
CompletionDate: None
CreationDate: 2017-08-29T08:29:41.000Z
InventorySizeInBytes: 0
JobDescription:
Tier: None
VaultQCS: qcs:id/0:cas:ap-[RegionName]:uid/12xxxxx:vaults/vault-name
0.084(s) elapsed
```

### Step 3: Get the content of a job

#### Command options

After the job is completed, use the following command to download the job result to a local file.
``` shell
cascmd.py fetch cas://vault-name E-nVoA6erIw71cTwI4gY6kaYpCrV1ehUrqXCkDHNfObQSfkqk_f5KyeKcxVvo--8 <local_file>
```
## More Features

The command line tool enables various operations. This document only lists the operations that are more frequently used on a daily basis. For help with more operations, see `cascmd.py -h`.

