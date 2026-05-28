## Embedding
```python
from sentence_transformers import SentenceTransformer

model = SentenceTransformer('all-MiniLM-L6-v2')

documents = [
    "Python is used for AI",
    "Flask is a web framework",
    "Vectors are used in semantic search",
    "Machine learning uses data"
]

embeddings = model.encode(documents)

print(embeddings)
```
# vecterdb

```python
import faiss
import numpy as np

dimension = embeddings.shape[1]

index = faiss.IndexFlatL2(dimension)

index.add(np.array(embeddings))
```
# Sematic Search
```
query = "AI applications"

query_embedding = model.encode([query])

D, I = index.search(np.array(query_embedding), k=2)

print(I)

for idx in I[0]:
    print(documents[idx])
```
```python



``` python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello, Flask is working!"

if __name__ == "__main__":
    app.run(debug=True)
```

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Home Page"

@app.route("/about")
def about():
    return "About Page"

@app.route("/contact")
def contact():
    return "Contact Page"

if __name__ == "__main__":
    app.run(debug=True)

```

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route("/")
def home():
    return render_template("index.html")

if __name__ == "__main__":
    app.run(debug=True)
```

```python
<!DOCTYPE html>
<html>
<body>
    <h1>Welcome to Flask</h1>
</body>
</html>
```



