# Table of Contents
1. [Problem](README.md#problem)
2. [Input Dataset](README.md#input-dataset)
3. [Instructions](README.md#instructions)
4. [Output](README.md#output)
5. [Tips on getting an interview](README.md#tips-on-getting-an-interview)
6. [Instructions to submit your solution](README.md#instructions-to-submit-your-solution)
7. [FAQ](README.md#faq)
8. [Questions?](README.md#questions?)

# Problem

A newspaper editor was researching immigration data trends on H1B(H-1B, H-1B1, E-3) visa application processing over the past years, trying to identify the occupations and states with the most number of approved H1B visas. She has found statistics available from the US Department of Labor and its [Office of Foreign Labor Certification Performance Data](https://www.foreignlaborcert.doleta.gov/performancedata.cfm#dis). But while there are ready-made reports for [2018](https://www.foreignlaborcert.doleta.gov/pdf/PerformanceData/2018/H-1B_Selected_Statistics_FY2018_Q4.pdf) and [2017](https://www.foreignlaborcert.doleta.gov/pdf/PerformanceData/2017/H-1B_Selected_Statistics_FY2017.pdf), the site doesn’t have them for past years. 

As a data engineer, you are asked to create a mechanism to analyze past years data, specificially calculate two metrics: **Top 10 Occupations** and **Top 10 States** for **certified** visa applications.

Your code should be modular and reusable for future. If the newspaper gets data for the year 2019 (with the assumption that the necessary data to calculate the metrics are available) and puts it in the `input` directory, running the `run.sh` script should produce the results in the `output` folder without needing to change the code.

# Input Dataset

Raw data could be found [here](https://www.foreignlaborcert.doleta.gov/performancedata.cfm) under the __Disclosure Data__ tab (i.e., files listed in the __Disclosure File__ column with ".xlsx" extension). 
For your convenience we converted the Excel files into a semicolon separated (";") format and placed them into this Google drive [folder](https://drive.google.com/drive/folders/1Nti6ClUfibsXSQw5PUIWfVGSIrpuwyxf?usp=sharing). However, do not feel limited to test your code on only the files we've provided on the Google drive 

**Note:** Each year of data can have different columns. Check **File Structure** docs before development. 

# Instructions

We designed this coding challenge to assess your coding skills and your understanding of computer science fundamentals. They are both prerequisites of becoming a data engineer. To solve this challenge you might pick a programing language of your choice (preferably Python, Scala, Java, or C/C++ because they are commonly used and will help us better assess you), but you are only allowed to use the default data structures that come with that programming language (you may use I/O and other standard libraries). For example, you can code in Python, **but you should not use Pandas or other external libraries**. 

***The objective here is to see if you can implement the solution using basic data structure building blocks and software engineering best practices (by writing clean, modular, and well-tested code).*** 

# Output 

Your program must create 2 output files:
* `top_10_occupations.txt`: Top 10 occupations for certified visa applications
* `top_10_states.txt`: Top 10 states for certified visa applications

Each line holds one record and each field on each line is separated by a semicolon (;).

Each line of the `top_10_occupations.txt` file should contain these fields in this order:
1. __`TOP_OCCUPATIONS`__: Use the occupation name associated with an application's Standard Occupational Classification (SOC) code
2. __`NUMBER_CERTIFIED_APPLICATIONS`__: Number of applications that have been certified for that occupation. An application is considered certified if it has a case status of `Certified`
3. __`PERCENTAGE`__: % of applications that have been certified for that occupation compared to total number of certified applications regardless of occupation. 

The records in the file must be sorted by __`NUMBER_CERTIFIED_APPLICATIONS`__, and in case of a tie, alphabetically by __`TOP_OCCUPATIONS`__.

Each line of the `top_10_states.txt` file should contain these fields in this order:
1. __`TOP_STATES`__: State where the work will take place
2. __`NUMBER_CERTIFIED_APPLICATIONS`__: Number of applications that have been certified for work in that state. An application is considered certified if it has a case status of `Certified`
3. __`PERCENTAGE`__: % of applications that have been certified in that state compared to total number of certified applications regardless of state.

The records in this file must be sorted by __`NUMBER_CERTIFIED_APPLICATIONS`__ field, and in case of a tie, alphabetically by __`TOP_STATES`__. 

Depending on the input (e.g., see the example below), there may be fewer than 10 lines in each file. There, however, should not be more than 10 lines in each file. In case of ties, only list the top 10 based on the sorting instructions given above.

Percentages also should be rounded off to 1 decimal place. For instance, 1.05% should be rounded to 1.1% and 1.04% should be rounded to 1.0%. Also, 1% should be represented by 1.0%

## Example
If you are given the input file, `./input/h1b_input.csv` with the following data:
```
;CASE_NUMBER;CASE_STATUS;CASE_SUBMITTED;DECISION_DATE;VISA_CLASS;EMPLOYMENT_START_DATE;EMPLOYMENT_END_DATE;EMPLOYER_NAME;EMPLOYER_BUSINESS_DBA;EMPLOYER_ADDRESS;EMPLOYER_CITY;EMPLOYER_STATE;EMPLOYER_POSTAL_CODE;EMPLOYER_COUNTRY;EMPLOYER_PROVINCE;EMPLOYER_PHONE;EMPLOYER_PHONE_EXT;AGENT_REPRESENTING_EMPLOYER;AGENT_ATTORNEY_NAME;AGENT_ATTORNEY_CITY;AGENT_ATTORNEY_STATE;JOB_TITLE;SOC_CODE;SOC_NAME;NAICS_CODE;TOTAL_WORKERS;NEW_EMPLOYMENT;CONTINUED_EMPLOYMENT;CHANGE_PREVIOUS_EMPLOYMENT;NEW_CONCURRENT_EMP;CHANGE_EMPLOYER;AMENDED_PETITION;FULL_TIME_POSITION;PREVAILING_WAGE;PW_UNIT_OF_PAY;PW_WAGE_LEVEL;PW_SOURCE;PW_SOURCE_YEAR;PW_SOURCE_OTHER;WAGE_RATE_OF_PAY_FROM;WAGE_RATE_OF_PAY_TO;WAGE_UNIT_OF_PAY;H1B_DEPENDENT;WILLFUL_VIOLATOR;SUPPORT_H1B;LABOR_CON_AGREE;PUBLIC_DISCLOSURE_LOCATION;WORKSITE_CITY;WORKSITE_COUNTY;WORKSITE_STATE;WORKSITE_POSTAL_CODE;ORIGINAL_CERT_DATE
0;I-200-18026-338377;CERTIFIED;2018-01-29;2018-02-02;H-1B;2018-07-28;2021-07-27;MICROSOFT CORPORATION;;1 MICROSOFT WAY;REDMOND;WA;98052;UNITED STATES OF AMERICA;;4258828080;;N;",";;;SOFTWARE ENGINEER;15-1132;"SOFTWARE DEVELOPERS, APPLICATIONS";51121.0;1;0;1;0;0;0;0;Y;112549.0;Year;Level II;OES;2017.0;OFLC ONLINE DATA CENTER;143915.0;0.0;Year;N;N;;;;REDMOND;KING;WA;98052;
1;I-200-17296-353451;CERTIFIED;2017-10-23;2017-10-27;H-1B;2017-11-06;2020-11-06;ERNST & YOUNG U.S. LLP;;200 PLAZA DRIVE;SECAUCUS;NJ;07094;UNITED STATES OF AMERICA;;2018723003;;Y;"BRADSHAW, MELANIE";TORONTO;;TAX SENIOR;13-2011;ACCOUNTANTS AND AUDITORS;541211.0;1;0;0;0;0;1;0;Y;79976.0;Year;Level II;OES;2017.0;OFLC ONLINE DATA CENTER;100000.0;0.0;Year;N;N;;;;SANTA CLARA;SAN JOSE;CA;95110;
2;I-200-18242-524477;CERTIFIED;2018-08-30;2018-09-06;H-1B;2018-09-10;2021-09-09;LOGIXHUB LLC;;320 DECKER DRIVE;IRVING;TX;75062;UNITED STATES OF AMERICA;;2145419305;;N;",";;;DATABASE ADMINISTRATOR;15-1141;DATABASE ADMINISTRATORS;541511.0;1;0;0;0;0;1;0;Y;77792.0;Year;Level II;OES;2018.0;OFLC ONLINE DATA CENTER;78240.0;0.0;Year;N;N;;;;IRVING;DALLAS;TX;75062;
3;I-200-18070-575236;CERTIFIED;;2018-03-30;H-1B;2018-09-10;2021-09-09;"HEXAWARE TECHNOLOGIES, INC.";;101 WOOD AVENUE SOUTH;ISELIN;NJ;08830;UNITED STATES OF AMERICA;;6094096950;;Y;"DUTOT, CHRISTOPHER";TROY;MI;SOFTWARE ENGINEER;15-1132;"SOFTWARE DEVELOPERS, APPLICATIONS";541511.0;5;5;0;0;0;0;0;Y;84406.0;Year;Level II;OES;2017.0;OFLC ONLINE DATA CENTER;84406.0;85000.0;Year;Y;N;Y;;;NEW CASTLE;NEW CASTLE;DE;19720;
4;I-200-18243-850522;CERTIFIED;2018-08-31;2018-09-07;H-1B;2018-09-07;2021-09-06;"ECLOUD LABS,INC.";;120 S WOOD AVENUE;ISELIN;NJ;08830;UNITED STATES OF AMERICA;;7327501323;;Y;"ALLEN, THOMAS";EDISON;NJ;MICROSOFT DYNAMICS CRM APPLICATION DEVELOPER;15-1132;"SOFTWARE DEVELOPERS, APPLICATIONS";541511.0;1;0;0;0;0;0;1;Y;87714.0;Year;Level III;OES;2018.0;OFLC ONLINE DATA CENTER;95000.0;0.0;Year;Y;N;Y;Y;;BIRMINGHAM;SHELBY;AL;35244;
5;I-200-18142-939501;CERTIFIED;2018-05-22;2018-05-29;H-1B;2018-05-29;2021-05-28;OBERON IT;;1404 W WALNUT HILL LN;IRVING;TX;75038;UNITED STATES OF AMERICA;;8666609190;;Y;"GARRITSON, JAMES";RICHARDSON;TX;SENIOR SYSTEM ARCHITECT;15-1132;"SOFTWARE DEVELOPERS, APPLICATIONS";541511.0;1;0;0;0;0;0;1;Y;71864.0;Year;Level II;Other;2017.0;OFLC ONLINE DATA CENTER;74000.0;0.0;Year;Y;N;Y;;;SUNRISE;BROWARD;FL;33323;
6;I-200-18121-552858;CERTIFIED;2018-05-01;2018-05-07;H-1B;2018-05-02;2018-10-26;ICONSOFT INC.;;101 CAMBRIDGE STREET SUITE 360;BURLINGTON;MA;01803;UNITED STATES OF AMERICA;;8882054614;1;N;",";;;SENIOR ORACLE ADF DEVELOPER;15-1132;"SOFTWARE DEVELOPERS, APPLICATIONS";541511.0;1;0;1;0;0;0;0;Y;92331.0;Year;Level III;Other;2017.0;OFLC ONLINE DATA CENTER;114000.0;0.0;Year;Y;N;Y;;;JACKSONVILLE;DUVAL COUNTY;FL;32202;
7;I-200-18215-849606;CERTIFIED;2018-08-03;2018-08-09;H-1B;2018-08-11;2021-08-11;COGNIZANT TECHNOLOGY SOLUTIONS US CORP;;211 QUALITY CIRCLE;COLLEGE STATION;TX;77845;UNITED STATES OF AMERICA;;2019661249;;N;",";;;SENIOR SYSTEMS ANALYST JC60;15-1121;COMPUTER SYSTEMS ANALYST;541512.0;1;0;1;0;0;0;0;Y;80579.0;Year;Level II;OES;2018.0;OFLC ONLINE DATA CENTER;80579.0;0.0;Year;Y;N;Y;;;OWINGS MILLS;BALTIMORE;MD;21117;
8;I-201-17339-472823;CERTIFIED;2017-12-08;2017-12-14;H-1B1 Chile;2017-12-08;2019-06-07;ISHI SYSTEMS INC;;185 HUDSON STREET;JERSEY CITY;NJ;07311;UNITED STATES OF AMERICA;;2013326900;;N;",";;;ASSOCIATE PRODUCT MANAGER(15-1199.09);15-1199;"COMPUTER OCCUPATIONS, ALL OTHER";541511.0;1;0;1;0;0;0;0;Y;88317.0;Year;Level III;OES;2017.0;OFLC ONLINE DATA CENTER;90000.0;0.0;Year;;;;;;JERSEY CITY;HUDSON;NJ;07311;
9;I-200-18233-239931;CERTIFIED;2018-08-21;2018-08-27;H-1B;2018-09-05;2021-09-04;"WB SOLUTIONS, LLC";;7320 E FLETCHER AVE;TAMPA;FL;33637;UNITED STATES OF AMERICA;;8133300099;;Y;"KIDAMBI, VAMAN";TRUMBULL;CT;SENIOR JAVA DEVELOPER;15-1132;"SOFTWARE DEVELOPERS, APPLICATIONS";541511.0;1;0;0;0;0;1;0;Y;104790.0;Year;Level III;OES;2018.0;OFLC ONLINE DATA CENTER;105000.0;0.0;Year;Y;N;Y;Y;;ALPHARETTA;FULTON;GA;30005;
```

then your output files would be:

`./output/top_10_occupations.txt`:
```
TOP_OCCUPATIONS;NUMBER_CERTIFIED_APPLICATIONS;PERCENTAGE
SOFTWARE DEVELOPERS, APPLICATIONS;6;60.0%
ACCOUNTANTS AND AUDITORS;1;10.0%
COMPUTER OCCUPATIONS, ALL OTHER;1;10.0% 
COMPUTER SYSTEMS ANALYST;1;10.0%
DATABASE ADMINISTRATORS;1;10.0%
```
`./output/top_10_states.txt`:
```
TOP_STATES;NUMBER_CERTIFIED_APPLICATIONS;PERCENTAGE
FL;2;20.0%
AL;1;10.0%
CA;1;10.0%
DE;1;10.0%
GA;1;10.0%
MD;1;10.0%
NJ;1;10.0%
TX;1;10.0%
WA;1;10.0%
``` 

# Tips on getting an interview

## What we are looking at
As a data engineer, it’s important that you write clean, well-tested, well-documented code that scales for a large amount of data. For this reason, it’s important to ensure that your solution works well for a large number of records.
Your solution should safisfy the following requirements:
* Repo follows the required repo directory structure
* `run.sh` script works as is in our environment and correct results are generated. If your code needs to be compilied before being executed, you must modify this script to include both compiling and executing your code
* The code is well-commented
* `README.md` contains Problem, Approach and Run instructions sections

You may write your solution in any mainstream programming language, such as C, C++, C#, Go, Java, Python, Ruby, or Scala. 
Once your solution satisfies all requirements listed above, submit a link of your Github or Bitbucket repo with your source code.


## Repo directory structure

The directory structure for your repo should look like this:
```
      ├── README.md 
      ├── run.sh
      ├── src
      │   └──h1b_counting.py
      ├── input
      │   └──h1b_input.csv
      ├── output
      |   └── top_10_occupations.txt
      |   └── top_10_states.txt
      ├── insight_testsuite
          └── run_tests.sh
          └── tests
              └── test_1
              |   ├── input
              |   │   └── h1b_input.csv
              |   |__ output
              |   |   └── top_10_occupations.txt
              |   |   └── top_10_states.txt
              ├── your-own-test_1
                  ├── input
                  │   └── h1b_input.csv
                  |── output
                  |   |   └── top_10_occupations.txt
                  |   |   └── top_10_states.txt
```
**Don't fork this repo** and don't use this `README` instead of your own. The content of `src` does not need to be a single file called `h1b-counting.py`, which is only an example. Instead, you should include your own source files and give them expressive names.

## Testing your directory structure and output format

To make sure that your code has the correct directory structure and the format of the output files are correct, we have included a test script called `run_tests.sh` in the `insight_testsuite` folder.

The tests files are stored in `.csv` format under the `insight_testsuite/tests` folder. Each test should have a separate folder with an `input` folder and `h1b_input.csv` file and an `output` folder with the two requested output files.

You can run the test with the following command from within the `insight_testsuite` folder:

    insight_testsuite~$ ./run_tests.sh 

On a failed test, the output of `run_tests.sh` should look like:

    [FAIL]: test_1
    [Thu Mar 30 16:28:01 PDT 2017] 0 of 1 tests passed

On success:

    [PASS]: test_1
    [Thu Mar 30 16:25:57 PDT 2017] 1 of 1 tests passed


One test has been provided as a way to check your formatting and simulate how we will be running tests when you submit your solution. We urge you to write your own additional tests. `test_1` is only intended to alert you if the directory structure or the output for this test is incorrect.

Your submission must pass at least the provided test in order to pass the coding challenge.

For a limited time we also are making available a <a href="http://ec2-18-210-131-67.compute-1.amazonaws.com/test-my-repo-link">website</a> that will allow you to simulate the environment in which we will test your code. It has been primarily tested on Python code but could be used for Java and C++ repos. Keep in mind that if you need to compile your code (e.g., javac, make), that compilation needs to happen in the run.sh file of your code repository. For Python programmers, you are able to use Python2 or Python3 but if you use the later, specify python3 in your run.sh script.

# Instructions to submit your solution
* To submit your entry please use the link you received in your coding challenge invite email
* You will only be able to submit through the link one time 
* Do NOT attach a file - we will not admit solutions which are attached files 
* Use the submission box to enter the link to your GitHub or Bitbucket repo ONLY
* Link to the specific repo for this project, not your general profile
* Put any comments in the `README.md` inside your project repo, not in the submission box
* We are unable to accept coding challenges that are emailed to us 

# FAQ

**Which Github link should I submit?**
You should submit the URL for the top-level root of your repository. For example, this repo would be submitted by copying the URL https://github.com/InsightDataScience/h1b_statistics into the appropriate field on the application. Do NOT try to submit your coding challenge using a pull request, which would make your source code publicly available.

**Do I need a private Github repo?**
No, you may use a public repo, there is no need to purchase a private repo. You may also submit a link to a Bitbucket repo if you prefer.

**May I use R, Matlab, or other analytics programming languages to solve the challenge?**
No. It's important that your implementation scales to handle large amounts of data. While many of our Fellows have experience with R and Matlab, applicants have found that these languages are unable to process data in a scalable fashion, so you must consider another language.

**May I use distributed technologies like Hadoop or Spark?**
No. Your code will be tested on a single machine, so using these technologies will negatively impact your solution. We're not testing your knowledge on distributed computing, but rather on computer science fundamentals and software engineering best practices.

**What sort of system should I use to run my program on (Windows, Linux, Mac)?**
You may write your solution on any system, but your source code should be portable and work on all systems. Additionally, your run.sh must be able to run on either Unix or Linux, as that's the system that will be used for testing. Linux machines are the industry standard for most data engineering teams, so it is helpful to be familiar with this. If you're currently using Windows, we recommend installing a virtual Unix environment, such as VirtualBox or VMWare, and using that to develop your code. Otherwise, you also could use tools, such as Cygwin or Docker, or a free online IDE such as Cloud9.

**How fast should my program run?**
While there are no strict performance guidelines to this coding challenge, we will consider the amount of time your program takes when grading the challenge. Therefore, you should design and develop your program in the optimal way (i.e. think about time and space complexity instead of trying to hit a specific run time value).

**Will you email me if my code doesn't run?**
Unfortunately, we receive hundreds of submissions in a very short time and are unable to email individuals if their code doesn't compile or run. We will do everything we can to properly test your code, but this requires good documentation. More so, we have provided a test suite so you can confirm that your directory structure and format are correct.

**Can I use a database engine?**
While a database engine can be used to complete this coding challenge, we are looking to see how well you program so please do not submit code that relies on a database engine for this challenge. 

**What should the format of the output be?**
In order to be tested correctly, you must use the format described above. You can ensure that you have the correct format by using the testing suite we've included.

**Should I check if the files in the input directory are text files or non-text files(binary)?**
No, for simplicity you may assume that all of the files in the input directory are text files, with the format as described above.

**Can I use an IDE like Eclipse or IntelliJ to write my program?**
Yes, you can use whatever tools you want - as long as your run.sh script correctly runs the relevant target files and creates the expected files in the output directory.

**What should be in the input directory?**
You can put any text file you want in the directory since our testing suite will replace it. Indeed, using your own input files would be quite useful for testing. The file size limit on Github is 100 MB so you won't be able to include the larger sample input files in your input directory.

**How long will it take for me to hear back from you about my submission?**
We receive hundreds of submissions and try to evaluate them all in a timely manner. We try to get back to all applicants within two or three weeks of submission, but if you have a specific deadline that requires expedited review, please email us at cc@insightdataengineering.com.

# Questions?
Re-read this README first and if you can't find an answer to your question, Email us at cc@insightdataengineering.com
