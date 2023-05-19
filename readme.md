<!-- Framework Title description and logo -->
<h1 align="center">KORTEX Data Engineering ETL Framework</h1>
<p align="center">
  <a href="https://github.com/kelloggcompany/kortex-etl-pipeline-devops">
    <img src="images/Global Data & Analytics_Logo_Block.gif" alt="Logo" width="100" height="100">
  </a>
</p>
<p align="center">
    give your complete Framework_description, snapshots and links are much appreciated, images can be saved into images directory of repository and can be refrenced
</p>

----

<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary><h2 style="display: inline-block">Table of Contents</h2></summary>
  <ol>
    <li>
      <a href="#about-the-Framework">About The Framework</a>
      <ul>
        <li><a href="#Objective">Objective</a></li>
        <li><a href="#planview-id">Planview ID</a></li>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
	<li><a href="#architecture-and-technical-design">Architecture & Technical Design</a></li>
	<li><a href="#process-details">Process Details</a></li>
    <li>
      <a href="#scripts-path">Scripts Path</a>
      <ul>
          <ul><li><a href="#dev-env">Dev Env</a></li></ul>
		  <ul><li><a href="#qa-env">QA Env</a></li></ul>
          <ul><li><a href="#prod-env">Prod Env</a></li></ul>
      </ul>
    </li>
    <li><a href="#contacts">Contacts</a></li>
      <ul>
		<li><a href="#GDA">GDA</a></li>
        <li><a href="#IT">IT</a></li>
		<li><a href="#IDS">IDS</a></li>
      </ul>
    <li><a href="#sustainment">Sustainment</a></li>
		<ul>
		<li><a href="#email-distro">Email Distribution List</a></li>
		</ul>
    <li><a href="#roadmap-ahead">Future road map for this Framework</a></li>
	<li><a href="#issues">Issues</a></li>
	<li><a href="#included-gitHub-actions">Included GitHub Actions</a></li>
  </ol>
</details>



<!-- ABOUT THE Framework -->
## About The Framework

### Objective
ETL framework
The initiative objectives are: 
* 
* 

The Framework will enable:
* 
* 
* 
* 


### Built With

* Glue - PySpark
* Redshift
* Lambda functions
* S3
* Cloud formation stack

### Planview Id
* Planview ID is: 123456
* [Planview link](https://change_link.com)


<!-- Architecture & Technical Design -->
## Architecture and Technical Design

Low level design architecture
![Low Level Architecture](./images/Framework-images/Architecture Design Diagram.png)

<!-- Process Details -->
## Process Details

Below process for metadata changes
Below process for metadata changes
1.	Go to AWS S3 and navigate to klg-nga-{env}-{region}-sr-cd bucket > glue_etl > metadata_files and make metadata changes to the below files.
		a. kortex_dataset/kortex_dateset.csv
		b. kortex_dataset_location/kortex_dataset_location.csv
		c. kortex_dataset_entity/kortex_dataset_entity.csv
2.	Go to AWS Glue console, click Triggers and create the trigger as follows.
		a. Add name of the trigger "klg-nga-{env}-{region}-etl-glue-job-{dataset_id}", choose On-demand and click Next
			![step2a](./images/Framework-images/step2a.png)
		b. Choose trigger job klg-nga-{env}-{region}-upload-cz-parent from the jobs list and click add (Navigate to 200 – 300 range)
			![step2b](./images/Framework-images/step2b.png)
		c.	Add key-value parameters and click Next to save the changes to create the trigger
			1.key: --meta_dataset_prefix value: glue_etl/metadata_files/
			2.key: --dataset_id value: your_dataset_id
			3.key: --meta_bucket_name value: klg-nga-{env}-{region}-src-cd
			4.key: --ingestion_layer_id value: 2
			5.key: --environment_name value: dev, qa or prod
			![step2c](./images/Framework-images/step2c.png)
3.	Create the crawlers for Landing zone(lz), Raw zone(rz) and Clense zone(cz) by running the trigger klg-nga-{env}-{region}-etl-create-crawler-dataset by adding dataset_id and ingestion_layer_id: 2,3,4 for lz,rz and cz respectively.
![step3](./images/Framework-images/step3.png)
4. 	Click on crawlers in the Glue console and verify if all the 3 crawlers were created by executing step 3.
	Example: 
	- klg_nga_dev_kna_lz_kna_crm_matrl_mstr
	- klg_nga_dev_kna_rz_kna_crm_matrl_mstr
	- klg_nga_dev_kna_cz_kna_crm_matrl_mstr

5.	Validate if the databases are created in Athena for all 3 zones for your dataset.
```Before executing the step 5 make sure your data is present in the land folder of internal bucket. Otherwise copy the data with the folder structure from QA / PROD. s3 > buckets > klg-nga-dev-kna-raw-intrnl > upload > kna_crm > matrl_mstr > ZV_PTNR_PRORANGE```
6.	Now run the trigger klg-nga-{env}-{region}-etl-glue-job-{dataset_id} which invokes the cz-parent job. Monitor the status of the cz-parent job from Jobs in Glue console.
7.	Once completed successfully validate if all the tables were created in Athena databases for all 3 zones.
8.	If step 7 is success, then query the count of records in Raw and Clense from Athena and capture the evidences.
9. 	In Athena, got to clense database and generate the DDLs for all the tables. Make sure the last 4 coulmns prefix with kortex.
10.	Go to Glue jobs and select create-redshift-dev (Check the respective environments to run the job) and add the DDLs in the Script tab then save and run the job.
sql_statement = """
{DDL statements}
"""
![step4](./images/Framework-images/step4.png)
11.	Re-run the trigger klg-nga-{env}-{region}-etl-glue-job-{dataset_id} to load the data into Redshift.
12. Open dbeaver and navigate to the Stage folder and check if the data is present in the table of your dataset.
13. Validate for the count of data is same accross all the zones till Redshfit.
	

<!-- Framework scripts path-->

## Scripts Path

### Dev Env
AWS account 953495608177 (KLG-AWS-KEY-KNA-NPD)

### QA Env
AWS account 953495608177 (KLG-AWS-KEY-KNA-NPD)

### Prod Env
AWS account 895344418283 (KLG-AWS-KEY-KNA-PRD)

<!-- CONTACTS -->
## Contacts
<!-- Global Data Analytics and Governance-->
### GDA
- Dennis Hoyle
- 

<!-- IT -->
### IT
IT Partner Names & email addresses
- Mastek

<!-- IDS Manager -->
### IDS
IDS Manager Names & email addresses
- Harshdeep Singh, Harshdeep.Singh@kellogg.com

<!-- SUSTAINMENT details -->
## Sustainment
This Framework is currently been supported by
* Resource Vendor partner - Wipro
* email id
### Email distro
Email groups or distribution
- 

## Roadmap Ahead
Future Kortex improvements

## Issues
Feel free to log issues in existing ETL framework
[issue](https://github.com/kelloggcompany/kortex-etl-pipeline-devops/issues)


## Included GitHub Actions
Some starter [GitHub Actions workflows](https://docs.github.com/en/actions/learn-github-actions) included with this repo are:
- [Stale issue](https://github.com/actions/stale) - labels and closes issues and pull requests with no activity for a set period of time
- [LFS Warning](https://github.com/ActionsDesk/lfs-warning) - issues warnings when large files are added to the repository
- [Release Drafter](https://github.com/marketplace/actions/release-drafter) - drafts release notes based on merged pull requests
- [First Interaction](https://github.com/actions/first-interaction) - Greets new contributors to the repo
- A [Dependabot config file](https://docs.github.com/en/github/administering-a-repository/configuration-options-for-dependency-updates) for alerting on dependency vulnerabilities
