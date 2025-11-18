# Job-Postings-Data-Analysis
## Dataset
Source: Kaggle - Job Descriptions 2025 – Tech & Non-Tech Roles by Aditya Raj Srivastava
https://www.kaggle.com/datasets/adityarajsrv/job-descriptions-2025-tech-and-non-tech-roles/data

ML project for analyzing job postings data. TF-IDF and Multinomial Naive Bayes, One-vs-rest Logistic Regression for multi-label and clustering with KMeans; PostgreSQL database for results writing.
## Data preparation
Use the psycopg2 adapter to connect to PostgreSQL. After establishing the connection, create a job_postings table matching the dataset schema and insert the job data.
## Predicting Job Title from Responsibilities
Treat title prediction as a multi-class text classification problem, using the job Responsibilities text to predict Title. Vectorize the responsibilities (via TF-IDF) and train a classifier (Naive Bayes).

Obtain an accuracy metric and after training, store the predicted titles back in the database.
## Predicting Job Skills from Title and Responsibilities
Predicting skills is a multi-label classification problem: each job can have multiple skills. First convert the skills into a list of labels and then use MultiLabelBinarizer to create a binary matrix of shape (jobs × unique_skills). For features combine Title and Responsibilities text. Train a multi-label classifier (one-vs-rest logistic regression) to predict the set of skills for each job. Insert the predicted skills into the database.

## Clustering Analysis
Perform several clustering experiments to uncover trends and groupings in the job data.

- Responsibilities Clustering: use TF-IDF on the Responsibilities field and apply K-Means.

- Skills Clustering: represent each job by its multi-hot skill vector (from the MultiLabelBinarizer) and apply K-Means.

## Overall
- 2D PCA responsibilities clusters: cluster 0 is clearly separated along PC1 from the other clusters. This means its job responsibilities use a very different vocabulary from the rest (likely a distinct family of roles: core software/tech vs business)

- Skills vs skills cluster heatmap: cluster 0 – marketing & management (team leadership, email marketing automation etc.); cluster 1 – Software/Data Engineering (Python, Java, SQL, MongoDB, PostgreSQL etc.).