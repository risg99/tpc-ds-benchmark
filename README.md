# TPC Benchmarking Brainstorming

*Note: Charlotte is our concerned subject, that is why try to define even the basic stuff.*

## TPC KIT Process

1) Loading Data Via the TPC Generator


`dsdgen /SCALE 1 /DIR csv_data /suffix ".csv" /delimiter "|" /VERBOSE Y /PARALLEL 4 /QUIET N`


2) To tackle the `_END not defiend error` add another step
Ensure that the file `query_templates/netezza.tpl` contains the following line:



`define _END = "";`


3) Converting Templates to SQL - Needs to be called iteratively


`dsqgen /input query_templates\templates.lst /directory query_templates /dialect netezza /output_dir sqls/query1.tpl /scale 1 /verbose y /template query1.tpl`


## Mirwise's Findings

### What is TPC?
TPC is **Transaction Performance Processing Counsel** formerly known as **Transaction Processing Councel**. The purpose of the councel is to ensure that benchmarks claimed by vendors are trustworthy and excludes the exaggeration factor.

### Supporting Repositories

1. https://github.com/promogekko/tpc-ds-postgresql
2. https://github.com/bahadley/tpc-di
3. https://github.com/JimTsesm/TPC-DI


### What is Decision Support Benchmarking?
#### TPC-DI
#### TPC-DS
#### TPC-H

### Preliminary Annex

* **Fact Table** 
consists of the measurements, metrics or facts of a business process. Facts tables could contain information like sales against a set of dimensions like Product and Date.*

* **Dimension Table**
contains attributes which describe the details of the dimension. E.g., Product dimensions can contain Product ID, Product Category, etc.*

* **Snowflake Schema**
is centralized by Fact table and surrounded by dimension tables such that the resultant shape of entity relational diagram resembels snowflake.

\* *The definations are taken from web and requires revision for plagiarism purposes.*

## < Your-Name > Findings

Add your own findings under you own heading


## Updates
11/10 Ahmad:
1) "preprocess_db_setup_load_script.ipynb" is to setup db and load data

2) "query_run_test_script.ipynb" was used to do a test run on all 99 queries (took about 2.5 hrs for 1 SF, and I've identified 23 queries that need to be updated to match with postgres syntax) 

3) "all_queries" folder holds the 99 queries, and also two text files, one with the list of queries with error and the other with the full result of the initial run test

*********
Next steps: From those 23 queries, we can each update some and push to git so that we don't mix it up, lemme know if u have any preference
Note: There is a seperate folder called "updated_queries" inside "all_queries" in which we can do the updates in, so that we distinguish the initial ones in a seperate folder

Once these 23 queries are updated, we can begin the benchmarking
