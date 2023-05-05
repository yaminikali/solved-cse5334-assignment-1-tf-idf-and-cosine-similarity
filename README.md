Download Link: https://assignmentchef.com/product/solved-cse5334-assignment-1-tf-idf-and-cosine-similarity
<br>
The instructions on this assignment are written in an .ipynb file. You can use the following commands to install the Jupyter notebook viewer. “pip” is a command for installing Python packages. You are required to use “Python 3.6.x” (any version of Python equal to or greater than version Python 3.6.0.) in this project.

pip install jupyter

To run the Jupyter notebook viewer, use the following command:

jupyter notebook P1.ipynb

The above command will start a webservice at <u><a href="http://localhost:8888/">http://localhost:8888/ </a></u><a href="http://localhost:8888/">(</a><u><a href="http://localhost:8888/">http://localhost:8888/)</a></u> and display the instructions in the ‘.ipynb’ file.

<h1>Requirements</h1>

This assignment must be done individually. You must implement the whole assignment by yourself.

Academic dishonety will have serious consequences.

You can discuss topics related to the assignment with your fellow students. But you are not allowed to discuss/share your solution and code.

<h1>Assignment Files</h1>

All the files for this assignment can be downloaded from Blackboard (“Course Materials” &gt; “Programming Assignments” &gt; “Programming Assignment 1 (P1)” &gt; “Attached Files”).

<ol>

 <li><strong>This instruction file itself “P1.ipynb”</strong></li>

 <li><strong>Data file “debate.txt”</strong></li>

</ol>

We use the transcript of the latest Texas Senate race debate between Senator Ted Cruz and Representative Beto O’Rourke, which took place on October 16, 2018. We pre-processed the transcript and provide you a text file debate.txt. In the file each paragraph is a segement of the debate from one of the candidates or moderators.

<ol start="3">

 <li><strong>Sample results “sampleresults.txt”</strong></li>

 <li><strong>Grading rubrics “rubrics.txt”</strong></li>

</ol>

<h1>Programming Language</h1>

<ol>

 <li>We will test your code under the particular version of Python 3.6.x. So make sure you develop your code using the same version.</li>

 <li>You are free to use anything from the Python Standard Library that comes with Python 3.6.x <a href="https://docs.python.org/3.6/library/">(</a><u><a href="https://docs.python.org/3.6/library/">https://docs.p</a></u><a href="https://docs.python.org/3.6/library/">y</a><u><a href="https://docs.python.org/3.6/library/">or</a></u><a href="https://docs.python.org/3.6/library/">g</a><u><a href="https://docs.python.org/3.6/library/">/3.6/librar</a></u><a href="https://docs.python.org/3.6/library/">y</a><u><a href="https://docs.python.org/3.6/library/">/ </a></u><a href="https://docs.python.org/3.6/library/">(</a><u><a href="https://docs.python.org/3.6/library/">https://docs.p</a></u><a href="https://docs.python.org/3.6/library/">y</a><u><a href="https://docs.python.org/3.6/library/">thon.or</a></u><a href="https://docs.python.org/3.6/library/">g</a><u><a href="https://docs.python.org/3.6/library/">/3.6/librar</a></u><a href="https://docs.python.org/3.6/library/">y</a><u><a href="https://docs.python.org/3.6/library/">/)</a></u><a href="https://docs.python.org/3.6/library/">)</a>.</li>

 <li>You are expected to use several modules in NLTK–a natural language processing toolkit for Python. NLTK doesn’t come with Python by default. You need to install it and “import” it in your .py file. NLTK’s website (<u><a href="http://www.nltk.org/index.html">http://www.nltk.or</a></u><a href="http://www.nltk.org/index.html">g</a><u><a href="http://www.nltk.org/index.html">/index.html </a></u><a href="http://www.nltk.org/index.html">(</a><u><a href="http://www.nltk.org/index.html">http://www.nltk.or</a></u><a href="http://www.nltk.org/index.html">g</a><u><a href="http://www.nltk.org/index.html">/index.html)</a></u>) provides a lot of useful information, including a book <u><a href="http://www.nltk.org/book/">http://www.nltk.or</a></u><a href="http://www.nltk.org/book/">g</a><u><a href="http://www.nltk.org/book/">/book/ </a></u><a href="http://www.nltk.org/book/">(</a><u><a href="http://www.nltk.org/book/">http://www.nltk.or</a></u><a href="http://www.nltk.org/book/">g</a><u><a href="http://www.nltk.org/book/">/book/)</a></u>, as well as installation instructions (<u><a href="http://www.nltk.org/install.html">http://www.nltk.or</a></u><a href="http://www.nltk.org/install.html">g</a><u><a href="http://www.nltk.org/install.html">/install.html </a></u><a href="http://www.nltk.org/install.html">(</a><u><a href="http://www.nltk.org/install.html">http://www.nltk.or</a></u><a href="http://www.nltk.org/install.html">g</a><u><a href="http://www.nltk.org/install.html">/install.html)</a></u>).</li>

 <li><strong>You are NOT allowed to use any non-standard Python package, except NLTK.</strong></li>

</ol>

<h1>Task TF-IDF and Cosine Similarity</h1>

<h2>1. Description of Task</h2>

You code should accomplish the following tasks:

<ul>

 <li><strong>Read</strong> the text file debate.txt. This is the transcript of the latest Texas Senate race debate between Ted Cruz and Beto O’Rourke. The following code does it.</li>

 <li><strong>Tokenize</strong> the content of the file. For this, you need a tokenizer. For example, the following piece of code uses a regular expression tokenizer to return all course numbers in a string. Play with it and edit it. You can change the regular expression and the string to observe different output results.</li>

</ul>

For tokenizing the Texas Senate debate transcript, let’s all use RegexpTokenizer(r'[a-zA-Z]+’). What tokens will it produce? What limitations does it have?

In [ ]: <strong>from</strong> <strong>nltk.tokenize</strong> <strong>import</strong> RegexpTokenizer tokenizer = RegexpTokenizer(r'[A-Z]{2,3}[1-9][0-9]{3,3}’)

tokens = tokenizer.tokenize(“CSE4334 and CSE5334 are taught together. IE

3013 is an undergraduate course.”) print(tokens)

[‘CSE4334’, ‘CSE5334’, ‘IE3013’]

<ul>

 <li>Perform <strong>stopword removal</strong> on the obtained tokens. NLTK already comes with a stopword list, as a corpus in the “NLTK Data” (<u><a href="http://www.nltk.org/nltk_data/">http://www.nltk.or</a></u><a href="http://www.nltk.org/nltk_data/">g</a><u><a href="http://www.nltk.org/nltk_data/">/nltk_data/ </a></u><a href="http://www.nltk.org/nltk_data/">(</a><u><a href="http://www.nltk.org/nltk_data/">http://www.nltk.or</a></u><a href="http://www.nltk.org/nltk_data/">g</a><u><a href="http://www.nltk.org/nltk_data/">/nltk_data/)</a></u><a href="http://www.nltk.org/nltk_data/">)</a>. You need to install this corpus. Follow the instructions at <u><a href="http://www.nltk.org/data.html">http://www.nltk.or</a></u><a href="http://www.nltk.org/data.html">g</a><u><a href="http://www.nltk.org/data.html">/data.html </a></u><a href="http://www.nltk.org/data.html">(</a><u><a href="http://www.nltk.org/data.html">http://www.nltk.or</a></u><a href="http://www.nltk.org/data.html">g</a><u><a href="http://www.nltk.org/data.html">/data.html)</a></u>. You can also find the instruction in this book: <u><a href="http://www.nltk.org/book/ch01.html">http://www.nltk.or</a></u><a href="http://www.nltk.org/book/ch01.html">g</a><u><a href="http://www.nltk.org/book/ch01.html">/book/ch01.html </a></u><a href="http://www.nltk.org/book/ch01.html">(</a><u><a href="http://www.nltk.org/book/ch01.html">http://www.nltk.or</a></u><a href="http://www.nltk.org/book/ch01.html">g</a><u><a href="http://www.nltk.org/book/ch01.html">/book/ch01.html)</a></u> (Section 1.2 Getting Started with NLTK). Basically, use the following statements in Python interpreter. A pop-up window will appear. Click “Corpora” and choose “stopwords” from the list.</li>

</ul>

showing info https://raw.githubusercontent.com/nltk/nltk_data/gh-pages/ index.xml

After the stopword list is downloaded, you will find a file “english” in folder nltk_data/corpora/stopwords, where folder nltk_data is the download directory in the step above. The file contains 179 stopwords. nltk.corpus.stopwords will give you this list of stopwords. Try the following piece of code.

In [ ]: <strong>from</strong> <strong>nltk.corpus</strong> <strong>import</strong> stopwords

print(stopwords.words(‘english’)) print(sorted(stopwords.words(‘english’)))

<ul>

 <li>Also perform <strong>stemming</strong> on the obtained tokens. NLTK comes with a Porter stemmer. Try the following code and learn how to use the stemmer.</li>

 <li>Using the tokens, compute the <strong>TF-IDF vector</strong> for each <strong>paragraph</strong>. <strong>In this assignment, for calculating inverse document frequency, treat debate.txt as the whole corpus and the paragraphs as documents. </strong>That is also why we ask you to compute the TF-IDF vectors separately for all the paragraphs, one vector per paragraph.</li>

</ul>

Use the following equation that we learned in the lectures to calculate the term weights, in which t is a token and d is a document (i.e., paragraph):

N

wt,d = (1 + log10 tft,d) × (log10 ).

df<sub>t</sub>

Note that the TF-IDF vectors should be normalized (i.e., their lengths should be 1).

Represent a TF-IDF vector by a dictionary. The following is a sample TF-IDF vector.

In [ ]: {‘sanction’: 0.014972337775895645, ‘lack’: 0.008576372825970286, ‘regre t’: 0.009491784747267843, ‘winter’: 0.030424375278541155}

<ul>

 <li>Given a query string, calculate the query vector. Compute the <strong>cosine similarity</strong> between the query vector and the paragraphs in the transcript. Return the paragraph that attains the highest cosine similarity score. In calculating the query vector, the vector is also to be normalized.</li>

</ul>