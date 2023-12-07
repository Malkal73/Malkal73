from flask import Flask, request

app = Flask(__name__)

@app.route("/", methods=["GET", "POST"])
def ussd():
    session_id = request.values.get("sessionId", None)
    phone_number = request.values.get("phoneNumber", None)
    text = request.values.get("text", "Welcome to the USSD service. Press 1 to charge Ksh. 20.")

    if text == "1":
        response_text = "You have been charged Ksh. 20. Thank you for using our service."
    else:
        response_text = "Invalid input. Press 1 to charge Ksh. 20."

    response = f"CON {response_text}"

    return response

if __name__ == "__main__":
    app.run(port=5000)
