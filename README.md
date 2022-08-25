
# AWS S3 Operations

A jar file that can be used to perform all operations 
available in the amazon s3.

# Jar Files to be Included
- aws-java-sdk-core-1.12.283
- aws-java-sdk-kms-1.12.283
- aws-java-sdk-s3-1.12.283
- commons-codec-1.15
- commons-logging-1.1.3
- httpclient-4.5.13
- httpcore-4.4.13
- ion-java-1.0.2
- jackson-annotations-2.12.6
- jackson-core-2.12.6
- jackson-databind-2.12.6.1
- jackson-dataformat-cbor-2.12.6
- jmespath-java-1.12.283
- joda-time-2.8.1
- S3operations

# Libraries to Import
    import S3operations.s3operations;
This will import all the required packages

# Methods available in s3operations

**Note:** If any error occurs it will be dispayed in the console

### **NewConnection**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
This method is used to create a S3 connection by means of 
access key, secret key and Region.

    void NewConnection(String accesskey,String secretkey,String Region)
**Note** : Region needed to be passed as a string in aws standard.It is case
insensitive.      

**Example:**

    s3operations obj = new s3operations;
    obj.NewConnection("accesskey","secretkey","us_east_1");
We can perform all operations using the obj object.

### **DoesBucketExist**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
This method is used to check whether a bucket with a given
name exists or not.Returns true if bucket exists else return false.

    Boolean DoesBucketExist(String BucketName)

**Example:**

    obj.DoesBucketExist("bucketname");

### **DoesFileExist**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
This method is used to check whether a file with a given
path exists or not.Returns true if file exists else returns false.

    Boolean DoesFileExist(String BucketName, String Path)
**Example:**

**Case1** : If file exist in the root directory

    obj.DoesFileExist("bucketname","welcome.png”);

**Case2** : If file exist in a particular directory mention the path. 

    obj.DoesFileExist("bucketname","Mydocs/Pictures/welcome.png”);

### **CreateBucket**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Creates a Bucket with a specified name.Returns true if a bucket with a given name is created else
returns false

    Boolean CreateBucket(String BucketName)
**Example:**

    obj.CreateBucket("Samplebucket");

### **DeleteBucket**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Deletes a Bucket with a specified name.Returns true if the 
bucket is deleted else returns false.

    Boolean DeleteBucket(String BucketName)
**Example:**

    obj.DeleteBucket("Samplebucket");

### **ListAllBuckets**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Returns a List of String data type that contains all Bucket Names

    List<String> ListAllBuckets()
**Example:**

    List<String> buckets = new ArrayList<String>();
    buckets = obj.ListAllBuckets();

### **UploadFile**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Uploads a File to the given Path. Returns true if file 
uploaded else returns false.

    Boolean UploadFile(String BucketName,String Path,File file)
**Example:**

    obj.UploadFile("Samplebucket", "Docs/Office/notes.txt",file);
**Note** : If Path does not exists it will automatically create a new path with
relevant folders and uploads the file.

### **DeleteFile**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Deletes a file present in the given path.Returns 
true if file is deleted else returns false.

    Boolean DeleteFile(String BucketName,String path)
**Example:**

**Case1** : Delete File

    obj.DeleteFile("Samplebucket", "Docs/Office/notes.txt");
**Case2** : Delete folder

    obj.DeleteFile("Samplebucket", "Docs/Work);
**Note** : If we want to delete a folder.the folder should
be empty.

### **DeleteAllFiles**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Deletes an entire folder along with its contents
Returns true if folder along with its files are deleted else return false

    Boolean DeleteAllFiles(String BucketName,String Path)
**Example:**

    obj.DeleteAllFiles("Samplebucket", "Docs/Office");
This will delete the Office Folder along with its files.

### **DeleteMultipleFiles**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Deletes Multiple files with Bucketname and an array of strings
which include the filepath.Returns true if all the files are 
deleted else returns false.

    Boolean DeleteMultipleFiles(String BucketName,String[] filepaths)
**Example:**

    String objkeyArr[] = { "document/hello.txt", "document/pic.png" }
    obj.DeleteMultipleFiles(objkeyArr)

### **ListAllFiles**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Returns a List of String data type that contains all File and Folder
Names Along with their paths.

    ListAllFiles(String BucketName)
**Example:**

    List<String> files = new ArrayList<String>();
    files = obj.ListAllFiles();

### **CopyFiles**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Copy file from one folder to another.Returns true if file is Copied else returns false

    Boolean CopyFiles(String FromBucket,String FromPath,String ToBucket,String ToPath)
**Example:**

**Case1:** Copy files from one bucket to another
    
    obj.CopyFiles("Samplebucket", "Docs/Office/notes.txt","Anotherbucket", "Sample/test/notes.txt");
**Case2:** Copy files within a bucket

    obj.CopyFiles("Samplebucket", "Docs/Office/notes.txt","Samplebucket", "Sample/test/notes.txt");

### **MultiPartFileUpload**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Uploads large file as parts. Returns a object of type Upload which
can be used to track the status of completion.It accepts Bucketname, 
path and file as inputs.

    Upload MultiPartFileUpload(String BucketName,String path,File file)

**Example:**
    
    Upload progress = obj.MultiPartFileUpload("Samplebucket", "Docs/Office/notes.mp4");
**Note:** It returns null if some error occurs.