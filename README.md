from fastapi import FastAPI
from pydantic import BaseModel
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

# Allow frontend to connect
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # You can later replace * with your Netlify URL
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

class ChatRequest(BaseModel):
    message: str

@app.post("/chat")
def chat(req: ChatRequest):
    user_message = req.message.lower()

    # Simple responses
    if "hello" in user_message:
        reply = "Hello! 👋 I'm C.G Robot 🤖. How can I help you?"
    elif "admission" in user_message:
        reply = "You can submit your admission form via our portal."
    elif "fees" in user_message:
        reply = "School fees details are available on the portal."
    else:
        reply = f"C.G Robot 🤖 says: You said '{req.message}'"

    return {"reply": reply}
