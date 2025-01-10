# pyspark-data-sources

[Databricks blog ref](https://www.databricks.com/blog/simplify-data-ingestion-new-python-data-source-api)

```bash
cd ..
git clone https://github.com/apache/spark
cd spark
./build/mvn -DskipTests clean package
```

```bash
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary for Spark Project Parent POM 4.0.0-SNAPSHOT:
[INFO] 
[INFO] Spark Project Parent POM ........................... SUCCESS [ 55.597 s]
[INFO] Spark Project Tags ................................. SUCCESS [ 32.083 s]
[INFO] Spark Project Sketch ............................... SUCCESS [ 15.109 s]
[INFO] Spark Project Common Utils ......................... SUCCESS [ 58.889 s]
[INFO] Spark Project Local DB ............................. SUCCESS [ 22.970 s]
[INFO] Spark Project Networking ........................... SUCCESS [ 34.766 s]
[INFO] Spark Project Shuffle Streaming Service ............ SUCCESS [ 21.998 s]
[INFO] Spark Project Variant .............................. SUCCESS [  7.922 s]
[INFO] Spark Project Unsafe ............................... SUCCESS [ 29.435 s]
[INFO] Spark Project Connect Shims ........................ SUCCESS [  7.254 s]
[INFO] Spark Project Launcher ............................. SUCCESS [ 18.024 s]
[INFO] Spark Project Core ................................. SUCCESS [04:38 min]
[INFO] Spark Project ML Local Library ..................... SUCCESS [ 48.445 s]
[INFO] Spark Project GraphX ............................... SUCCESS [ 48.490 s]
[INFO] Spark Project Streaming ............................ SUCCESS [01:35 min]
[INFO] Spark Project SQL API .............................. SUCCESS [01:10 min]
[INFO] Spark Project Catalyst ............................. SUCCESS [04:08 min]
[INFO] Spark Project SQL .................................. SUCCESS [07:20 min]
[INFO] Spark Project ML Library ........................... SUCCESS [05:01 min]
[INFO] Spark Project Tools ................................ SUCCESS [  7.666 s]
[INFO] Spark Project Hive ................................. SUCCESS [01:42 min]
[INFO] Spark Project Connect Common ....................... SUCCESS [01:12 min]
[INFO] Spark Avro ......................................... SUCCESS [ 46.121 s]
[INFO] Spark Protobuf ..................................... SUCCESS [ 53.926 s]
[INFO] Spark Project REPL ................................. SUCCESS [ 30.003 s]
[INFO] Spark Project Connect Server ....................... SUCCESS [01:24 min]
[INFO] Spark Project Connect Client ....................... SUCCESS [01:43 min]
[INFO] Spark Project Assembly ............................. SUCCESS [  7.834 s]
[INFO] Kafka 0.10+ Token Provider for Streaming ........... SUCCESS [ 30.359 s]
[INFO] Spark Integration for Kafka 0.10 ................... SUCCESS [ 49.158 s]
[INFO] Kafka 0.10+ Source for Structured Streaming ........ SUCCESS [01:05 min]
[INFO] Spark Project Examples ............................. SUCCESS [01:03 min]
[INFO] Spark Integration for Kafka 0.10 Assembly .......... SUCCESS [ 17.042 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  42:50 min
[INFO] Finished at: XX
[INFO] ------------------------------------------------------------------------
```

Took me around 43 mins to build in a 8 gb machine.

```bash
cd ..
python3 -m venv .venv
. .venv/bin/activate
cd spark
pip install setuptools
cd python/packaging/classic && python setup.py sdist
```

```bash
cd ../../../../.
git clone https://github.com/allisonwang-db/pyspark-data-sources
cd pyspark-data-sources
pip install poetry filelock
poetry lock
poetry install
poetry run pip install ../spark/python/dist/pyspark-4.0.0.dev0.tar.gz
```

Output

```bash
Processing /home/ubuntu/spark/python/dist/pyspark-4.0.0.dev0.tar.gz
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Collecting py4j==0.10.9.8 (from pyspark==4.0.0.dev0)
  Downloading py4j-0.10.9.8-py2.py3-none-any.whl.metadata (1.3 kB)
Downloading py4j-0.10.9.8-py2.py3-none-any.whl (202 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 202.8/202.8 kB 4.6 MB/s eta 0:00:00
Building wheels for collected packages: pyspark
  Building wheel for pyspark (pyproject.toml) ... done
  Created wheel for pyspark: filename=pyspark-4.0.0.dev0-py2.py3-none-any.whl size=390438949 sha256=5efdf9694aaa39607f411ad027c5ed65870a503a99943e3c0c77de41b6b465bc
  Stored in directory: /home/ubuntu/.cache/pip/wheels/f0/7b/b8/4d9a067c31e669ac0f1714a49fe2e2261b21fd9f189b97149c
Successfully built pyspark
Installing collected packages: py4j, pyspark
Successfully installed py4j-0.10.9.8 pyspark-4.0.0.dev0
```
