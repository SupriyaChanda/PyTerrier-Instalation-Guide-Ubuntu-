# PyTerrier

PyTerrier is a declarative platform for information retrieval experiemnts in Python. It uses the Java-based [Terrier information retrieval platform](http://terrier.org/) internally to support indexing and retrieval operations. It is a Python API for Terrier - v.0.9

# Installation

### Linux
1. Check `pip` already installed in your system or not?
2. If not, then `sudo apt install python3-pip`
3. If yes, then `pip install python-terrier`
4. If it there is any error, then have to check `g++ --version`
5. Then `sudo apt-get install libpcre3 libpcre3-dev`
6. Then `pip install python-terrier`
7. Install Java Runtime Environment
8. `sudo apt install default-jdk`
9. `sudo apt install default-jre`
10. `update-alternatives --config java`
11. You may need to set JAVA_HOME environment variable if Pyjnius cannot find your Java installation.
```python
JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64/bin/java"
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin"
```
12. ```python gedit test.py ```

# Retrieval and Evaluation

```python
import pyterrier as pt
if not pt.started():
    pt.init()
    
dataset = pt.get_dataset("vaswani")

bm25 = pt.BatchRetrieve.from_dataset(dataset, "terrier_stemmed", wmodel="BM25")
dph = pt.BatchRetrieve.from_dataset(dataset, "terrier_stemmed", wmodel="DPH")

result=pt.Experiment(
    [bm25, dph],
    dataset.get_topics(),
    dataset.get_qrels(),
    eval_metrics=["map", "recip_rank"]
)

print(result)
```
