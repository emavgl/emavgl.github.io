+++
title = "About me"
slug = "about"
+++

{{< rawhtml >}}
<div style="text-align: left;">
    <img src="/images/avatar.jpg" width="300" />
</div>
{{< /rawhtml >}}  

**_Emanuele Viglianisi_**
*Senior Software Engineer (Data)*
*emavgl@gmail.com*
*[github.com/emavgl](https://github.com/emavgl)*
*[linkedin.com/in/emanuele-viglianisi](https://linkedin.com/in/emanuele-viglianisi)*

Senior Software Engineer with strong background in data engineering, cloud computing, big data, distributed systems, and security. Originally from Sicily (Italy), currently based in Linz (Austria). Beyond engineering, I enjoy cooking (and eating) authentic food, hacking on personal side projects, and exploring new places.

### Work experience

### Senior Software Engineer at Dynatrace
**July 2023 – Present**
- Core contributor to GRAIL (Dynatrace's mass-scale data lakehouse), focusing on query performance, security framework execution, and cross-team feature delivery.
- **Query Performance**: Designed and owned a filter pushdown framework that evaluates conditions at the coarsest data boundary first, skipping entire blocks rather than scanning every record, coordinating across the query engine and multiple storage teams
- **Access Control**: Core contributor to the record-level and column-level permission framework, delivering multiple performance improvements
    - Shipped a partial evaluator rejecting entire data groups at once (up to ~40% faster permissions' execution); introduced a more efficient lookup with a gain of ~75% for large permission sets
    - Introduced caching for permission evaluation, leading to a ~20% reduction in query time for dashboard executions; optimized policy resolution by merging overlapping rules and skipping irrelevant ones
- **Record deletion**: Co-owned the query-layer implementation of a GDPR feature letting customers delete their own data, covering request validation (allowed operations, table eligibility, timeframe constraints) and translating validated requests into deletion instructions for the storage system
- **AI-first adoption**: Actively driving an AI-adoption operational shift by introducing AI agents to automate the development lifecycle; optimizing internal projects and tooling while coordinating across teams to align engineering practices
- **Mentorship**: Manage the end-to-end internship lifecycle from initial technical interviews and selection to project completion. Concurrently shape the scope and technical trajectory of Master's theses, advising colleagues on research direction to deliver high-quality code and novel solutions, with select work successfully resulting in pending patent applications
- **Technologies**: Java, Spring Boot, OpenAPI, gRPC, Docker, Kubernetes, Gradle, Python, LLMs

#### Software Engineer (Data) at Runtastic (adidas Digital)
**2020 – July 2023**
- **Data Platform Architecture**: Co-designed and implemented Runtastic's cloud data platform on Databricks and Azure, migrating legacy on-prem infrastructure, engineered robust streaming ETL pipelines, GDPR compliance systems, data quality frameworks, CI/CD, and alerting.
- **Data Science Product Engineering**: Partnered with the Data Science team to design and productionize high-impact data products, including:
    - **Follower Recommendation**: Developed a graph-based system (PySpark & GraphFrames) that increased average user followers by 60%.
    - **Zero2Hero**: Built a behavioral model identifying key app features driving long-term retention for new users (presented at Big Data Week 2022 and Big Data Conference Europe 2022)
- **adidas Strategic Secondment (Q3 2022)**: Worked with the sales Data & Analytics team of adidas. Advised on best practices for implementing data pipelines and KPI. Designed and helped with the implementation of a new ETL streaming pipeline for adidas' sellout data, which powers an almost real-time dashboard used for quick decisions in key selling times (e.g., Black Friday).
- **Technologies**: Python, PySpark, Databricks, Airflow, Azure EventHub, Azure Web App, Azure Functions

####  **Software Engineer and Researcher at Fondazione Bruno Kessler**
**2018 - 2019**
- **Applied Research & Innovation**: Developed a state-of-the-art black-box testing tool for functional and security validation of RESTful APIs within an EU-funded project (EIT Digital). The resulting research paper won the Distinguished Paper Award at the ICST 2020 conference and laid the foundation for subsequent PhD research.

### Educations

- **Master of Science - Computer Science**, University of Trento, full marks with honors  
    - Specializing in Software Engineering, Security Testing, Machine Learning, Big Data Analysis and Data mining. Thesis in collaboration with FBK, consisting in a novel tool for [black-box security testing](https://www.sciencedirect.com/science/article/pii/S0164121220301163) of Ethereum Smart Contracts. Technologies: Python, Z3, Blockchain (Ethereum), Solidity, Web3JS, Truffle Framework, Node.JS.

### Certifications

- [Microsoft Certified: Azure Fundamentals](https://docs.microsoft.com/en-us/learn/certifications/azure-fundamentals/) - 2023
- [Microsoft Certified: Azure Data Engineer Associate](https://docs.microsoft.com/en-gb/learn/certifications/azure-data-engineer/) - 2023

### Presentations at conferences

- [Big Data Week 2022 Bucharest](https://bucharest.bigdataweek.com/session/zero2hero-an-advanced-data-platform-to-drive-user-engagement/) and [Big Data Conference Europe 2022](https://events.pinetool.ai/2749/#speakers/789010?referrer%5Bpathname%5D=%2Fspeakers&referrer%5Bsearch%5D=&referrer%5Btitle%5D=Speakers)  
ZERO2HERO: An Advanced Data Platform To Drive User Engagement - **Emanuele Viglianisi**, Daniele Montesi
- [Data+AI Summit Europe, 2020-11-18](https://databricks.com/session_eu20/developing-ml-enabled-data-pipelines-on-databricks-using-ide-ci-cd-at-runtastic) and [CI/CD Template Webinar, 2020-10-20](https://databricks.com/p/webinar/developing-ml-enabled-data-pipelines-on-databricks-using-ide-ci-cd)  
Developing ML-enabled Data Pipelines on Databricks using IDE & CI/CD at Runtastic - **Emanuele Viglianisi**, Michael Shtelma

### Publications

I am the main author of the following research publications:

- [RESTTESTGEN: Automated Black-Box Testing of RESTful APIs](https://ieeexplore.ieee.org/abstract/document/9159077/)  **(Distinguished Paper Award)**  
**E Viglianisi**, M Dallago, M Ceccato - 2020 IEEE 13th International Conference on Software Testing, Validation and Verification (ICST)
- [A federated society of bots for smart contract testing](https://www.sciencedirect.com/science/article/pii/S0164121220301163)  
**E Viglianisi**, M Ceccato, P Tonella - Journal of Systems and Software, 2020
More on the [Google Scholar](https://scholar.google.com/citations?user=jSjoAKEAAAAJ&hl=it).


