# Movie Recommender System using Spark

This repository contains the code and data which I used to build a simple movie recommendation system using *PySpark*. The dataset which I used is a small subset of the [MovieLens dataset](https://grouplens.org/datasets/movielens/). This dataset describes 5-star rating and free-text tagging activity from [MovieLens](http://movielens.org/), a movie recommendation service. The code which I used to implement the recommender system is displayed in the two Jupyter notebooks contained in the *notebooks* folder below: **data_prep.ipynb** and **recommender.ipynb**. All computations were carried out using Google Dataproc.

Below is an outline of how to run the code using Spark on Google Dataproc:

1. Create a Cloud Storage Bucket on Google Cloud Platform (GCP) to host the data and upload the files below.
2. Create a cluster, with Jupyter notebook compatibility, in order to run PySpark code using the following commands in the GCP console:


`   gcloud services enable dataproc.googleapis.com \
                            compute.googleapis.com \
                            storage-component.googleapis.com \
                            bigquery.googleapis.com \
                            bigquerystorage.googleapis.com      `


`   REGION=europe-west2
    ZONE=europe-west2-b
    CLUSTER_NAME=[INSERT]
    BUCKET_NAME=[INSERT]        `


`   gcloud beta dataproc clusters create ${CLUSTER_NAME} \
        --region=${REGION} \
        --zone=${ZONE} \
        --image-version=1.5 \
        --master-machine-type=n1-standard-4 \
        --worker-machine-type=n1-standard-4 \
        --bucket=${BUCKET_NAME} \
        --optional-components=ANACONDA,JUPYTER \
        --enable-component-gateway \
        --metadata 'PIP_PACKAGES=google-cloud-bigquery google-cloud-storage' \
        --initialization-actions gs://goog-dataproc-initialization-actions-${REGION}/python/pip-install.sh      `


3. Go to the Dataproc tab in GCP and click on the cluster which was just created. Click on the 'WEB INTERFACES' tab and click on the link for *JupyterLab*. From here, the two aforementioned notebooks will be visible and clicking into these will allow you to run the code.
