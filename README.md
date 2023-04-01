# newimproved
import openai

def chat_with_gpt3(prompt, conversation_history):
    full_prompt = f"{conversation_history}User: {prompt}\nAI:"
    response = openai.Completion.create(
        engine="davinci-codex",
        prompt=full_prompt,
        max_tokens=100,
        n=1,
        stop=None,
        temperature=0.5,
    )

    message = response.choices[0].text.strip()
    return message

conversation_history = ""
while True:
    user_input = input("You: ")
    if user_input.lower() == "quit":
        break
    conversation_history += f"User: {user_input}\nAI:"
    response = chat_with_gpt3(user_input, conversation_history)
    print("AI:", response)
    conversation_history += f"{response}\n"
