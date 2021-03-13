# Bible_verse_predictor
1) Created my work environment and installed the necessary libraries 
2) Creation of the model saved as as a pickle file for easy reusability
3) Creation of a web interface (using html and CSS) where the verses can be inputed and where the prediction of old or new testament can be diplayed with sentiment and probability score for old and new testament 
4) Below is the explanantion of the app (app.py) itself using the pickled model (naive bayes for calssification, raw text in this case) 
A)From flask we import **Flask,render_template,request and url_for
 also import pandas as pd  and import numpy as np** to render the html template and generate the url for the raw text input, pandas and numpy so we can read the data set to be used 
B) For Machine learning packages,
**from sklearn.feature_extraction.text import CountVectorizer
from sklearn.externals import joblib** .............sill in progress
 
