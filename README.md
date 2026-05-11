# Ai-powdered-crop-rotation-advisor-
from flask import Flask, render_template, request
import pandas as pd

app = Flask(__name__)

# Simple crop recommendation logic
def recommend_crop(soil, season):
    if soil == "Loamy" and season == "Summer":
        return "Maize"
    elif soil == "Clay" and season == "Winter":
        return "Wheat"
    elif soil == "Sandy" and season == "Rainy":
        return "Groundnut"
    else:
        return "Rice"

@app.route('/')
def home():
    return render_template('index.html')

@app.route('/predict', methods=['POST'])
def predict():
    soil = request.form['soil']
    season = request.form['season']

    result = recommend_crop(soil, season)

    return render_template(
        'index.html',
        prediction=result
    )

if __name__ == '__main__':
    app.run(debug=True)