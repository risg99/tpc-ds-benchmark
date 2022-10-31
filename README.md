# TPC-DS Benchmarking 2022

### Introduction
This project is part of the **Big Data Management and Analytics (BDMA) - Erasmus Mundus Joint Master Degree Program** course **Data Warehouse**. The purpose of this repository is to allow others to reproduce our results and to explain better the steps for a meaningful TPC-DS benchmark for those seeking open-source solutions.

*******

## Reproducing results

1) The TPC-DS tool itself is not part of this repository it can be downloaded from [official website](https://www.tpc.org/tpcds/default5.asp).
2) For our use case, the TPC-DS tool 3.x version had build problems therefore either we could use [older refined version](https://github.com/gregrahn/tpcds-kit) or use the latest version on Linux.
3) Our team tried to install WSL (Windows Subsystem for Linux) on Windows 11 but it had driver problem and internet connectivity issues inside Ubuntu, therefore we used Docker.
4) Building the TPC-DS tool itself:

    1) **On Docker/Linux:** To build the tool itself on Ubuntu, we need to install bison, flex and then use `make` command to build the C source code to an executable utility. Ending up with `dsdgen.sh` (Data Generator), `dsqgen.sh` (Query Generator). The detailed instructions are provided in  `tpc-ds-tool > tools > How_To_Guide.doc` under Linux section. 
    2) **On Windows:** The tool has to be built using the oldest available Visual Studio Express (in our case 2017). We built the TPC-DS tool (TPCDS-KIT) on Windows just for exploration but went with Docker one since it supported the latest version 3.x instead of 2.x.
      
5) Generating data:
    1) **On Linux:** To gererate the data use the command `dsdgen -scale 1 -dir .\tmp -suffix .csv -delimiter "^" -parallel 4 -child 1 -quiet n -terminate n &`.
    2)  **On Windows:** `dsdgen /SCALE 1 /DIR .\tmp /suffix ".csv" /delimiter "^" /VERBOSE Y /PARALLEL 4 /CHILD 1 /QUIET N`.

6) Generating queries:
    1) **On Linux:** `./dsqgen -DIRECTORY ../query_templates -INPUT ../query_templates/templates.lst -VERBOSE Y -QUALIFY Y -DIALECT netezza`.
    2)  **On Windows:** `./dsqgen /DIRECTORY ../query_templates /INPUT query_templates/templates.lst /VERBOSE Y /QUALIFY Y /DIALECT netezza`. 
    
7) Once the data and queries have been generated, the Python notebooks listed in the repository are self-explainitory. Nevertheless:
    1) `preprocess_db_setup_load_script.ipynb` is to setup db and load data.
    2) `query_run_test_script.ipynb` was used to do a test run on all 99 queries (took about 2.5 hrs for 1 SF, and I've identified 23 queries that need to be updated to match with postgres syntax) 
    3) `all_queries` folder holds the 99 queries, and also two text files, one with the list of queries with error and the other with the full result of the initial run test.
    4) The folder `all_queries > updated_queries` contains the queries that have been optimized/modified.

### Exceptional Circumstances:

To tackle the `_END not defiend error` add another step
Ensure that the file `query_templates/netezza.tpl` contains the following line:

`define _END = "";`

### Supporting Repositories

1. https://github.com/promogekko/tpc-ds-postgresql
2. https://github.com/bahadley/tpc-di
3. https://github.com/JimTsesm/TPC-DI
4. https://github.com/stanislawbartkowski/mytpcds
5. https://ankane.org/tpc-ds
6. https://datacadamia.com/data/type/relation/benchmark/tpcds/dsqgen
