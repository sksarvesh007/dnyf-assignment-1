Classify the review into a 1-5 star rating based on the examples below.
Return ONLY the JSON object.

Example 1:
Review: "The food was okay, but the service was terrible. Waiter was rude."
Output:
{{
"predicted_stars": 2,
"explanation": "Food was average but negative service experience pulls the rating down."
}}

Example 2:
Review: "Absolutely amazing! Best pizza I've ever had. Highly recommend."
Output:
{{
"predicted_stars": 5,
"explanation": "Superlative positive language indicates a perfect score."
}}

Example 3:
Review: "It was meh. Not bad, not good. Just average."
Output:
{{
"predicted_stars": 3,
"explanation": "Neutral sentiment, average experience."
}}

Target Review: "{review_text}"

Output:
