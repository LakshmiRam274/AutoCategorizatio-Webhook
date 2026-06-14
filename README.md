# AutoCategorizatio-Webhook
Auto Ticket Categorization wedhook using fastAPI .

from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Ticket(BaseModel):
    text: str

@app.post("/categorize")
def categorize(ticket: Ticket):

    text = ticket.text.lower()

    if "login" in text or "password" in text:  
        category = "Access Issue"

    elif "payment" in text or "refund" in text:
        category = "Billing"

    elif "error" in text or "bug" in text:
        category = "Technical Issue"

    else:
        category = "General Query"

    return {"category": category}
