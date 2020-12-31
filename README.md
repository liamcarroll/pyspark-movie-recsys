# CA4022 - Movie Recommender System using Spark

This repository contains the code and data which I used to build a simple movie recommendation system using *PySpark*. The dataset which I used is a small subset of the [MovieLens dataset](https://grouplens.org/datasets/movielens/). This dataset describes 5-star rating and free-text tagging activity from [MovieLens](http://movielens.org/), a movie recommendation service. The code which I used to implement the recommneder system is displayed in the two Jupyter notebooks conatined in the *notebooks* folder below: **data_prep.ipynb** and **recommender.ipynb**. All computations were carried out using Google Dataproc.

Below is an outline of how to run the code using Spark on Google Dataproc:

1. Create a Cloud Storage Bucket on Google Cloud Platform (GCP) to host the data and upload the files below.
2. Create a cluster, with Jupyter notebook compatibility, in order to run PySpark code using the following commands in the GCP console:\n

`   gcloud services enable dataproc.googleapis.com \ \n
                            compute.googleapis.com \ \n
                            storage-component.googleapis.com \ \n
                            bigquery.googleapis.com \ \n
                            bigquerystorage.googleapis.com      `


`   REGION=europe-west2 \n
    ZONE=europe-west2-b \n
    CLUSTER_NAME=[INSERT] \n
    BUCKET_NAME=[INSERT] \n        `

`   gcloud beta dataproc clusters create ${CLUSTER_NAME} \ \n
        --region=${REGION} \ \n
        --zone=${ZONE} \ \n
        --image-version=1.5 \ \n
        --master-machine-type=n1-standard-4 \ \n
        --worker-machine-type=n1-standard-4 \ \n
        --bucket=${BUCKET_NAME} \ \n
        --optional-components=ANACONDA,JUPYTER \ \n
        --enable-component-gateway \ \n
        --metadata 'PIP_PACKAGES=google-cloud-bigquery google-cloud-storage' \ \n
        --initialization-actions gs://goog-dataproc-initialization-actions-${REGION}/python/pip-install.sh      `


3. Go the the Dataproc tab in GCP and click on the cluster which was just created. Click on the 'WEB INTERFACES' tab and click on the link for *JupyterLab*. From here, the two aforementioned notebooks will be visible and clicking into these will allow you to run the code.