# lumy-chatbot

import openai
from flask import Flask, request, jsonify

app = Flask(__name__)

# Configurar sua chave da API OpenAI
OPENAI_API_KEY = "sua-chave-aqui"
openai.api_key = OPENAI_API_KEY

def chat_with_lumy(user_message):
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[
            {"role": "system", "content": "Você é Lumy, o assistente virtual da Marca Zaywan. Seja amigável, profissional e prestativo."},
            {"role": "user", "content": user_message}
        ]
    )
    return response['choices'][0]['message']['content']

@app.route("/chat", methods=["POST"])
def chat():
    data = request.json
    user_message = data.get("message", "")
    response = chat_with_lumy(user_message)
    return jsonify({"response": response})

if __name__ == "__main__":
    app.run(debug=True)
