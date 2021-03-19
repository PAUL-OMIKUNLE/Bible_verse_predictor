# Bible_verse_predictor
1) Created my work environment and installed the necessary libraries 
2) Creation of the model saved as as a pickle file for easy reusability
3) Creation of a web interface (using html and CSS) where the verses can be inputed and where the prediction of old or new testament can be diplayed with sentiment and probability score for old and new testament 
4) Below is the explanantion of the app (app.py) itself using the pickled model (naive bayes for calssification, raw text in this case) 
A)From flask we import **Flask,render_template,request and url_for
 also import pandas as pd  and import numpy as np** to render the html template and generate the url for the raw text input, pandas and numpy so we can read the data set to be used 
B) For Machine learning packages,
**from sklearn.feature_extraction.text import CountVectorizer** to help identify the words in vector form from the data   
**from sklearn.externals import joblib** to be able to use our serialized models that hve been created so asto save time
c) For Natural language procesing 
**from textblob import TextBlob** for text sentiment analysis
D) USING A WEB INTERFACE 
**@app.route('/')
def index():
	return render_template('index.html')** this line is to help us render the web page (created seperatly) for input of the bible verse and the ouput prediction 
 
 E)  PREDICTING using the data splitting it into features and target 
**@app.route('/predict',methods=["GET","POST"])
def predict():
	df= pd.read_csv("data/kjvmindata.csv")
	# Features and Labels
	df_X = df.text
	df_Y = df.label**
F) VECTORIZATION OF FEATURES, so the machine can use the vectorized format to train and predict easily
**orpus = df_X
	cv = CountVectorizer()
	X = cv.fit_transform(corpus)** 
G) Loading our saved naive bayes model with Joblib 
**naivebayes_model = open("models/biblepredictionNV_model.pkl","rb")
	clf = joblib.load(naivebayes_model)**
H) 
if request.method == 'POST':
		raw_text = request.form['rawtext']
		data = [raw_text]
		vect = cv.transform(data).toarray()
		my_prediction = clf.predict(vect)
		pred_score = clf.predict_proba(vect)
		nlp_text = TextBlob(raw_text)
		text_sentiment = nlp_text.sentiment.polarity
		verse_sentiment = text_sentiment
