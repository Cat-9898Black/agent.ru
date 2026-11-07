# agent.ru

import os
import google.generativeai as genai

os.environ["GEMINI_API_KEY"] = "ВСТАВЬ_СЮДА_СВОЙ_КЛЮЧ"
genai.configure(api_key=os.environ["GEMINI_API_KEY"])

def calculator(expression: str) -> str:
"""Вычисляет математическое выражение."""
try:
result = eval(expression, {"builtins": None}, {})
return str(result)
except Exception as e:
return f"Ошибка вычисления: {e}"

model = genai.GenerativeModel(
model_name="gemini-1.5-flash",
tools=[calculator],
system_instruction="Ты полезный ассистент. Если нужно посчитать что-то, используй инструмент calculator."
)

def run_agent(user_input: str):
print(f"\nВы: {user_input}")
chat = model.start_chat(enable_automatic_function_calling=True)
response = chat.send_message(user_input)
print(f"Агент: {response.text}")

if name == "main":
print("Агент запущен! Напиши 'выход', чтобы завершить.")
while True:
user_input = input("\nВы: ")
if user_input.lower() in ["выход", "exit"]:
break
run_agent(user_input)