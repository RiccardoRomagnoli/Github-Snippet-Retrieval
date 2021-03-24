# Github-Snippet-Retrieval

In this project, a subset of all the java repositories publicly available on Github has been crawled, processed and indexed into elastic search.

## System requirements
   - Python 3.6 or later
   - requests 2.13.0 or later
   - Flask 1.0 or later
   - elasticsearch 7.0.1
   - nltk 3.2.5
   - javalang 0.11.0
   - beautifulsoup4 4.7.1
   - PyGithub 1.43.7
   - PyYAML 5.1

```
pip install -r requirements.txt
```

## Crawling
```
cd Crawl/
mkdir -p code

python crawl.py --token=token --query="query language:java"
```

## Processing
Replace the tokenize.py file inside the javalang package (C:\Users\****\AppData\Local\Programs\Python\Python**\Lib\site-packages\javalang) with our tokenizer.py file

```
python process_files.py --code=<path_to_code_folder>
```

## Indexing

First you should start elastic search server.
```
https://www.elastic.co/downloads/elasticsearch
```
Download and unpack the Elasticsearch official distribution.

Run `bin/elasticsearch` on Linux or macOS. Run `bin\elasticsearch.bat` on Windows.

Run `curl -X GET http://localhost:9200/` to verify Elasticsearch is running.

After you start the server you should delete any previously create git_source index

```
CURL -XDELETE localhost:9200/git_source
```

The search engine API will index our records once is started.
## Starting the Search Engine
```
cd Frontend/
```

Edit the config file found in config/config.yml to add the path to the records json created by the Processing part
You can also define host and port for ElasticSearch, as well as the port for the api.

Upload the record and setup the ElasticSearch instance:
```
python search_api.py
```

## Opne UI

Connect to http://localhost:8080/ in your browser




