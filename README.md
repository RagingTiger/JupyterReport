# Jupyter Report
A Jupyter Notebook template for creating PDF reports from Jupyter Notebooks.

## Docker
Below we discuss how to run the `Jupyter Notebooks` using **Docker**:

### Development
To run the notebooks locally, and persist changes made to the notebooks, first
`git clone` the repo:
```
git clone https://github.com/RagingTiger/JupyterReport.git
```
Then `cd JupyterReport` and run the following:
```
docker run -d \
           --rm \
           --name jupyter_report \
           -e JUPYTER_ENABLE_LAB=yes \
           -p 8888 \
           -v $PWD:/home/jovyan \
           ghcr.io/ragingtiger/omega-notebook:master && \
sleep 5 && \
  docker logs jupyter_report 2>&1 | grep "http://127.0.0.1" | tail -n 1 | \
    sed "s/:8888/:$(docker port jupyter_report | grep '0.0.0.0:' | \
    awk '{print $3'} | sed 's/0.0.0.0://g')/g"
```
Click the link (should look similar to:
http://127.0.0.1:RANDOM_PORT/lab?token=LONG_ALPHANUMERIC_STRING) which will
`automatically` log you in and allow you to start running the *notebooks*.
