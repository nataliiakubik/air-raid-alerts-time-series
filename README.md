##### **Time Series Analysis of Air Raid Alerts in Ukraine**

##### **Project overview**



This project analyses temporal patterns in official air-raid alert records across Ukrainian oblasts.



###### **The main research question is:**



How did the weekly frequency and cumulative duration of oblast-level air-raid alerts change over time, and which oblasts accumulated the greatest recorded alert burden?



The analysis was completed in Python using Google Colab.



###### Data source



The project uses the public official\_data\_en.csv file from the Ukrainian Air Raid Sirens Dataset.



The source file contains event-level records with:



oblast, raion, and hromada names;

geographic reporting level;

alert start and end timestamps;

data source.



Timestamps were converted from UTC to the Europe/Kyiv timezone.



Data-quality findings



The initial audit identified several important issues:



the file contained oblast-, raion-, and hromada-level records;

combining these geographic levels could produce double counting;

113,845 exact duplicate rows were detected;

reporting shifted substantially from oblast-level to raion-level records beginning in August 2025.



To preserve comparability, the final analysis was restricted to unique, valid oblast-level records from 15 March 2022 through 31 July 2025.



The final analytical cohort contained 62,139 alert records representing 25 top-level geographic units, including Kyiv City.



##### **Methods**



Exact duplicates were removed using all seven original source fields:



oblast

raion

hromada

level

started\_at

finished\_at

source



Records with missing timestamps, missing oblast names, or non-positive durations were excluded.



Two weekly metrics were calculated:



Weekly alert frequency: number of oblast-level alert records beginning during each week.

Weekly cumulative oblast-alert hours: total alert duration summed across oblasts.



Alerts crossing weekly boundaries were divided between the relevant weeks. The first and final partial calendar weeks were excluded from the weekly figures.



A separate ranking was calculated using cumulative alert duration for each oblast across the full study period.



Main findings



Weekly alert frequency was highly variable, ranging from approximately 90 to 600 records per complete week. There was no single continuous upward or downward trend.



A lower-frequency period was visible around late 2022 and early 2023. Several of the largest weekly frequency peaks occurred during early and mid-2024.



Weekly cumulative oblast-alert duration showed a clearer increase. From approximately mid-2024 through July 2025, cumulative duration remained persistently elevated and frequently reached around 550–850 oblast-alert hours per week.



Weekly alert counts and cumulative duration did not always move in parallel. This shows that frequency and total duration capture different dimensions of recorded alert burden. Mean alert duration was not calculated, so the figures should not be interpreted as evidence that individual alerts became longer.



Donetska oblast had the greatest recorded cumulative alert duration, followed by Kharkivska and Sumska oblasts.



###### **Figures**

Weekly alert frequency

Weekly cumulative alert duration

Oblasts with the greatest cumulative alert duration





###### **Limitations**

The analysis includes only oblast-level records through 31 July 2025. Later observations were excluded because reporting shifted substantially toward the raion level.

The results describe officially declared alerts, not attacks, casualties, military activity, or objective regional danger.

Alert patterns may be influenced by reporting systems, regional policies, administrative decisions, and official threat-assessment practices.

Alert frequency and cumulative duration are complementary but not interchangeable.

The first and final partial calendar weeks were excluded from the weekly figures.


**Repository structure**
---

.

├── README.md

├── requirements.txt

├── air\_raid\_alerts\_analysis.ipynb

├── air\_raid\_alerts\_analysis.py

├── figures/

│   ├── weekly\_oblast\_alert\_count.png

│   ├── weekly\_oblast\_alert\_hours.png

│   └── top10\_oblasts\_cumulative\_alert\_hours.png

└── outputs/

&#x20;   ├── weekly\_oblast\_metrics.csv

&#x20;   └── oblast\_cumulative\_alert\_hours.csv


**How to run**

Open air\_raid\_alerts\_analysis.ipynb in Google Colab.

Select Runtime → Run all.

The notebook downloads the public source dataset directly.

The final cells recreate the figures and output tables.



No manual dataset download is required.



**Use of AI**



ChatGPT was used to brainstorm the initial project scope, review methodological risks, generate and refine Python code, and check interpretations.



All code was executed in Google Colab. Outputs, errors, assumptions, and methodological decisions were reviewed manually. The project scope was reduced after the AI initially proposed an unnecessarily extensive audit, and the analysis period was revised after inspection revealed duplicate records and a change in geographic reporting structure.

