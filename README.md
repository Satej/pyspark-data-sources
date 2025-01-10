# pyspark-data-sources

```bash
git clone https://github.com/allisonwang-db/pyspark-data-sources
cd pyspark-data-sources
python3 -m venv .venv
poetry lock
poetry install
```

```bash
cd ..
git clone https://github.com/apache/spark
cd spark
./build/mvn -DskipTests clean package
cd python/packaging/classic && python setup.py sdist
```

```bash
cd ..
cd pyspark-data-sources
poetry run pip install ../spark/python/dist/pyspark-4.0.0.dev0.tar.gz
```
