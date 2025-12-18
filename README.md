# Initial file content.
git init
uv venv .venv
source .venv/bin/activate
uv pip install -r requirements.txt

dvc init
dvc add data/wine_sample.csv

dvc remote add -d wine-remote s3://<s3_bucket_name>
dvc push

git add data/wine_sample.csv.dvc
git commit -am "new version of the data"