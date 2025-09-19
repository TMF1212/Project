
**AIDev Dataset Challenge - Studying AI Coding Agents on Github** (Who adopts coding agents on GitHub, How do adoption patterns vary across repositories and ecosystems?, What practices correlate with the quantity of agentic PRs?, How can these practices inform concrete guidelines for developers? )






**Dataset Description**

The problems in this study relies on a two-part dataset collected from AIDev Dataset GitHub, consisting of metadata on both users and their pull requests (PRs). The dataset contain the period 2016–2025 and covers multiple open-source repositories across diverse ecosystems.

1.**User Dataset (all_user_df)**

The user dataset provides background information about GitHub contributors such as -

id: Unique identifier for each user.

login: GitHub username.

followers / following: Social connectivity metrics indicating the number of followers a user has and the number of accounts they follow.

created_at: Account creation timestamp.

This dataset is primarily used to infer developer experience levels, differnciate between newcomers (accounts less than six months old at the dataset cutoff) and experienced developers (accounts older than six months).

Size: 72,189 users.


2. **Pull Request Dataset (all_pr_df)**

The pull request dataset contains detailed records of PR activity across repositories such as -

id: Unique pull request identifier.

number: PR number within a repository.

title: Title of the pull request.

body: Descriptive text accompanying the PR.

agent: Field indicating whether the PR was authored by a coding agent (e.g., Claude_Code, Devin). If null, the PR is assumed to be authored by a human.

user_id / user: Links the PR to its corresponding user in the user dataset.

state: Current status of the PR (open, closed, merged).

created_at / closed_at / merged_at: Timestamps for the PR lifecycle.

repo_id / repo_url / html_url: Repository identifiers and links.

This dataset allows analysis of adoption patterns, PR size, task type, and commit granularity.

Size: 932,788 pull requests.


3.**Derived Features**

To support analysis to answer the questions, additional features were achieved, they are -

experience: Categorization of users as newcomers or experienced based on account age.

is_agentic: Boolean flag indicating whether a PR was authored by a coding agent.

pr_size: Length of the PR body text, used as a proxy for PR scope.

task_type: Categorization of PRs into bugfix, feature, refactor, docs, or other based on title keywords.

commits: Number of commits associated with each PR (when available).


The dataset integrates 72,000 users and ~933,000 pull requests, providing sufficient granularity to analyze:

Who adopts coding agents,

How adoption varies across repositories and ecosystems, and

Which development practices correlate with agentic PR activity.



**Getting Started**


This project was developed entirely in Google Colab for accessibility and reproducibility. No local installation is required.


1. **Open in Google Colab**
Click the hugging face to open the notebook directly in Colab:



2. **Install Dependencies**
Most libraries are pre-installed in Colab. If needed, install missing packages:

!pip install pandas numpy matplotlib seaborn scikit-learn


3. **Dataset Setup**
Upload or link the dataset into your Colab session:

from google.colab import files
uploaded = files.upload()  # select your CSV/Parquet/JSON file

Alternatively, load directly from GitHub:

import pandas as pd
url = ["https://raw.githubusercontent.com/your-username/agentic-prs-analysis/main/data/prs.csv"](https://github.com/SAILResearch/AI_Teammates_in_SE3/blob/main/analysis/dataset_overview.ipynb)
prs_df = pd.read_csv(url)


4. **Run the Analysis**
Execute the notebook cells in order to:



Load and preprocess the dataset


Explore adoption patterns across repositories and ecosystems


Investigate correlations with practices (PR size, commit granularity, etc.)


Derive actionable guidelines for developers


**Evaluation Methods and Results**


**Evaluation Methods**

To answer the research questions, we applied the following methods:

**Data Preprocessing**

Loaded PR metadata (all_pr_df) and user information.

Converted timestamps (e.g., created_at, creation_date) to datetime objects.

Labeled users as newcomers (<6 months) or experienced (≥1 year) relative to cutoff dates.

**Adoption Analysis (Q1)**



Filtered PRs involving AI/coding agents.

Counted adoption by user type (newcomer vs. experienced).

Visualized adoption using a pie chart to show proportions.



**Repository and Ecosystem Patterns (Q2)**

Grouped PRs by repository_id and ecosystem fields.

Measured adoption intensity as proportion of agentic PRs in each repository.

Compared adoption patterns across repositories and ecosystems using bar plots.



**Correlation with Practices (Q3)**

Computed PR size as a proxy for task complexity (additions + deletions).

Correlated PR size with the number of agentic PRs using scatter plots and correlation coefficients.

(Optional extension: commit granularity, task types).



**Guideline Derivation (Q4)**



Interpreted statistical and visual findings.

Translated correlations into practical guidelines for developers working with agentic PRs.



**Results**

Adoption Across User Types



Total Agentic PRs analyzed: N

Newcomers contributed 14.5% of Agentic PRs.

Experienced developers contributed 85.5% of Agentic PRs.

The pie chart shows that both groups adopt agents, but experienced developers dominate adoption.

Repository and Ecosystem Variation

Adoption is not evenly distributed.

Certain repositories and ecosystems (e.g., high-activity or ML-related projects) show a higher proportion of Agentic PRs.

This suggests adoption is influenced by project domain and community norms.

Correlation with Practices

PR size shows a positive correlation with Agentic PR usage (larger PRs are more likely to involve agents).

This indicates developers may rely on agents more for complex or large-scale changes.

Smaller PRs and bug fixes are less associated with agent involvement.



**Practical Guidelines**

Developers should adopt incremental PR practices (moderate size, clear commits) to maximize agent-assisted workflows.

Projects can encourage adoption by providing guidelines for newcomers on integrating agents safely.

Ecosystems with structured contribution norms (tests, templates, CI/CD pipelines) may benefit more from agentic PRs.



**Acknowledgements**

I would like to express my sincere gratitude to Prof. JW for providing the project and dataset that formed the foundation of this research.
