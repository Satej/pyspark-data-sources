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
curl -fsSL https://pyenv.run | bash
export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init - bash)"

# Restart your shell for the changes to take effect.
# Load pyenv-virtualenv automatically by adding
# the following to ~/.bashrc:
eval "$(pyenv virtualenv-init -)"

sudo apt update
sudo apt install -y build-essential libbz2-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev zlib1g-dev libsqlite3-dev liblzma-dev
pyenv install 3.9
pyenv local 3.9  # Activate Python 3.9 for the current project

sudo apt install python3.12-venv
python3.9 -m venv .venv
. .venv/bin/activate
cd spark
cd python/packaging/classic && python setup.py sdist
```

```bash
cd ../../../../.
git clone https://github.com/allisonwang-db/pyspark-data-sources
cd pyspark-data-sources
pip install poetry wheel faker
poetry lock
poetry install
poetry run pip install ../spark/python/dist/pyspark-4.0.0.dev0.tar.gz
```

Output

```bash
Processing /home/ubuntu/spark/python/dist/pyspark-4.0.0.dev0.tar.gz
  Preparing metadata (setup.py) ... done
Requirement already satisfied: py4j==0.10.9.8 in /home/ubuntu/.venv/lib/python3.9/site-packages (from pyspark==4.0.0.dev0) (0.10.9.8)
Building wheels for collected packages: pyspark
  Building wheel for pyspark (setup.py) ... done
  Created wheel for pyspark: filename=pyspark-4.0.0.dev0-py2.py3-none-any.whl size=390438906 sha256=0f8e95648ce1073cdb26e807c2fc2485012b6f4fb88c622ccf04be5338d3d43e
  Stored in directory: /home/ubuntu/.cache/pip/wheels/b4/22/ad/d9e2e585794948b8fcdbf0df9be32a096bc113698647363e02
Successfully built pyspark
Installing collected packages: pyspark
  Attempting uninstall: pyspark
    Found existing installation: pyspark 4.0.0.dev0
    Uninstalling pyspark-4.0.0.dev0:
      Successfully uninstalled pyspark-4.0.0.dev0
Successfully installed pyspark-4.0.0.dev0

[notice] A new release of pip is available: 23.0.1 -> 24.3.1
[notice] To update, run: pip install --upgrade pip
```

```bash
pyspark
>>> from pyspark_datasources import FakeDataSource
>>> spark.dataSource.register(FakeDataSource)
>>> spark.read.format("fake").load().show()
+------------+----------+-------+-----------+                                   
|        name|      date|zipcode|      state|
+------------+----------+-------+-----------+
|  Lisa Mills|1976-12-19|  23138|Mississippi|
|  Amber West|2000-10-05|  82350|   Oklahoma|
|Frances Chen|1991-07-28|  90949|   New York|
+------------+----------+-------+-----------+
```
