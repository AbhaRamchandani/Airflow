Completed: 16-Aug-2019

# Project: Build Data Pipelines with Airflow
For an ETL from S3 to Redshift, create custom operators to perform tasks such as staging the data, filling the data warehouse, and running checks on the data as the final step. 

# Available information
#1 - Dataset: 2 datasets that reside in S3:
     - Song data: s3a://udacity-dend/song_data
     - Log data: s3a://udacity-dend/log_data

#2 - Template files
     The project template package contains three major components for the project:
      - The dag template has all the imports and task templates in place, but the task dependencies have not been set
      - The operators folder with operator templates
      - A helper class for the SQL transformations

# Setup Instructions
For this project, I used the Udacity workspace.
 . Create an IAM user (I created AirflowProject) with full access to Redshift and read-only access to S3.
 . Download and save the credentials.csv generated while creating the IAM ser.
 . Spin up a Redshift cluster (I created redshift-cluster-1, with DB Name 'dev', Master Username 'awsuser' with a password).
 . From the create_tables.py in the Udacity workspace, execute each query, for creating Redshift tables, in the Query editor of the Redshift cluster created above.
 . Run /opt/airflow/start.sh command to start the Airflow webserver.
 . Add Airflow connections to AWS:
   (1) Go to Admin -> Connections -> Create
   (2) On the create connection page, enter the following values:
       - Conn Id: Enter aws_credentials.
       - Conn Type: Enter Amazon Web Services.
       - Login: Enter your Access key ID from the IAM User credentials you downloaded earlier.
       - Password: Enter your Secret access key from the IAM User credentials you downloaded earlier.
   (3) Once you've entered these values, select Save and Add Another.
   (4) On the next create connection page, enter the following values:
       - Conn Id: Enter redshift.
       - Conn Type: Enter Postgres.
       - Host: Enter the endpoint of your Redshift cluster, excluding the port at the end. You can find this by selecting your cluster in the Clusters page of the Amazon Redshift console. See where this is located in the screenshot below. IMPORTANT: Make sure to NOT include the port at the end of the Redshift endpoint string.
       - Schema: Enter dev. This is the Redshift database you want to connect to.
       - Login: Enter awsuser.
       - Password: Enter the password you created when launching your Redshift cluster.
       - Port: Enter 5439.
   (5) Once you've entered these values, select Save.
 
# Program execution
 From the Airflow UI, turn on the DAG 'udac_example_dag' and observe it's execution in tree / graph mode. 
 Once the execution is complete, the data can be queried in th Query editor of the Redshift Cluster.
    
# Testing the program
To test the execution, I ran a few SQL queries in the Query editor of the Redshift Cluster.
       
### NOTE: The task of table creation could have also been added to the DAG, but I chose to run the table creation SQLs in the Query editor on Redshift Cluster.

# Reference
(1) Udacity lessons
(2) Udacity Slack channels and mentor