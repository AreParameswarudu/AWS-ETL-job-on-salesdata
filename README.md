# AWS-ETL-job-on-salesdata
Exploring the AWS services for creating ETL pipeline for sales data of a e-commerce data.
AWS serveces covered includes 
1. Amazon S3 Bucket.
2. AWS Glue
   2.1 AWS Glue Catalog
   2.2 AWS Glue Crawler.
   2.3 AWS Glue ETL jobs.
3. AWS IAM roles/users.
4. AWS Athena.

THe Outline of Project looks like:
***

![Screenshot 2024-11-02 191506](https://github.com/user-attachments/assets/db1ee01f-7805-445a-a9aa-b1969207df77)
***

# Raw Data.

The data was actually populated using python. It was not real data from any real time e-commerce website.
The reason behind populating data by own was that mostly everywhere( google, kaggle etc) the avalible data is almost cleaned and ready to query or to get insights. 
So to have a hands on with AWS Glue Studio (ETL jobs), a messy data is required that need to be transformed and hence the data.
___
# Steps to follow:
1. Creating s3 bucket to store raw data and transformed data.
2. Creating IAM role that work with Glue and S3.
3. Using Glue catalog for populating database and Glue Crawler to create tables for database.
4. Using Glue ETL for transfoming data and storing into S3.
5. Creating table outof transformed data to work with Athena.
6. Accessing Transformed data in Athena and querying.

## Step 1:  Creating S3 bucket.
Search for the S3 in the AWS console and use create option to create a bucket for the project. <br>
Search S3 → Creat bucket → Create folders in it → Upload the file. <br>
I followed this structure 
> param-supermarket-sales-data (BucketName)
>> sales-database              (Folder)
>>> raw-sales-data             (Folder)
>>>> raw.csv                   (File)
***
![image](https://github.com/user-attachments/assets/80eae1dc-7b75-4870-bee4-9487f09d22c1)
***

_Note: Reason for creating multiple folder is,_ <br>
_Every e-commerce website can have multiple databases (products, sales, Representatives, Stores ETC)._
_In order to store them seperately Sales-database (folder) is created._
_In sales-database, we have to folders, one for raw data and other for transformed data. We have stored the raw.csv file in the raw-data folder._

***
## Step 2: Creating a IAM role for the project.
Go to AWS IAM → Roles → Create Role

Use cases for other AWS services : Select Glue

Add Permissions Policies : Search and Select ‘S3 full access’, 'Aws Glue Service Role'

Role name : Appropiate Name _(‘aws-sales-data-role’ for me)_ .

***
![image](https://github.com/user-attachments/assets/02d90209-6dcc-40cf-b7ac-7412ceb7d08e)

***
## Step 3: Glue Catalog and Glue Crawler.
### 3.1 Go to Glue → Glue Catalog →  Database → Add Database.
    Give an appropiate name for the data base. (Sales-database).

***
![image](https://github.com/user-attachments/assets/38ccc001-34f5-4442-84a3-ace2ff997eca)

***
### 3.2 In Glue Catalog → Databases → Tables.
    Use Add table suing Crawler. <br>
   * [x] Step1 → Name : Appropiate name _(crawler-sales for me)._ <br>
  * [x]  Step2 → Add a data source → Choose the location of raw.csv file. <br>
  * [x]  Step3 → Choose IAM role that we created previously. <br>
 * [x]   Step4 → Choose Data Base that we created perviously. <br>
            For Scheduling → On demand. <br>
    _Note: No need to worry about the name for table. It will be populated uisng the same name of choosen file._
    
***
![image](https://github.com/user-attachments/assets/d3bcb186-3d25-4811-9e38-029ee1cd95e5)

***

In the Crawlers section, use can see the new crawler created. <br>
Select the crawler → Run the crawler.<br>
Once the run was sucessful, table will be populated. Go to tables section and verify the table.

***
![image](https://github.com/user-attachments/assets/316a2d7d-9516-4b5d-be97-fcb0cee66d59)

***




  
