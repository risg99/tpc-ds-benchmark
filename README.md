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
