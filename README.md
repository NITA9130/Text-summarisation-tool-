# Text-summarisation-tool-

**COMPANY**: CODTECH IT SOLUTIONS 

**NAME**: NITA PURI

**INTERN ID**: CT08HZO

**DOMAIN**: AI

**BATCH DURATION**: December 30th,2024 to January 30th,2025.

**MENTOR NAME**: NEELA SANTHOSH

https://github.com/NITA9130/Text-summarisation-tool-/edit/main/README.md


# ENTER DESCRIPTION OF TASK PERFORMED NOT LESS THAN 500 WORDS
flask import Flask, request, jsonify
from transformers import pipeline

# Create a Flask app
app = Flask(__name__)

# Load summarization pipeline
summarizer = pipeline("summarization")

@app.route("/")
def home():
    return "Welcome to the Text Summarization Tool!"

@app.route("/summarize", methods=["POST"])
def summarize():
    try:
        # Getting text from user through POST method in JSON
        data = request.json
text = data.get(\"text")
        if not text:
            return jsonify({\"error\": "No text provided" }), 400

        # Generate summary
        summary = summarizer(text, max_length=100, min_length=30, do_sample=False)
return jsonify({"summary": summary[0]['summary_text']})
    except Exception as e:
        return jsonify({"error": str(e)}), 500

if __name__ == "__main__":
    app.run(debug=True)
