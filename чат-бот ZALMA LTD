# bot.py
# WhatsApp-чат-бот ZALMA LTD. (Twilio Business API)

from twilio.rest import Client
from dotenv import load_dotenv
import os

# Загружаем переменные окружения из .env
load_dotenv()

# Twilio credentials
ACCOUNT_SID = os.getenv("TWILIO_ACCOUNT_SID")
AUTH_TOKEN = os.getenv("TWILIO_AUTH_TOKEN")
TWILIO_WHATSAPP = os.getenv("TWILIO_WHATSAPP_NUMBER")   # например: 'whatsapp:+14155238886'
MY_WHATSAPP = os.getenv("MY_WHATSAPP_NUMBER")           # твой бизнес-номер WhatsApp 'whatsapp:+7XXXXXXXXXX'

client = Client(ACCOUNT_SID, AUTH_TOKEN)

# Словарь ключевых слов и ответов
RESPONSES = {
    "привет": "Здравствуйте! Вас приветствует ZALMA LTD. Чем можем помочь?",
    "здравствуйте": "Здравствуйте! Чем можем помочь?",
    "адрес": "Наш офис: г. Алматы, ул. Богенбай батыра, 305А.",
    "режим работы": "Мы работаем с понедельника по пятницу, с 09:00 до 18:00.",
    "оборудование": "Мы поставляем лабораторное, медицинское оборудование и расходные материалы.",
    "что вы продаете": "Мы занимаемся поставкой оборудования для лабораторий, молекулярной биологии, микробиологии и диагностики.",
    "сервис": "Чтобы вызвать сервис-инженера, напишите свои ФИО, организацию и модель оборудования.",
    "ремонт": "По вопросам сервисного обслуживания и ремонта свяжитесь с нами info@zalma.org.",
    "кп": "Направьте, пожалуйста, ваш email и описание запроса — мы подготовим коммерческое предложение.",
    "коммерческое предложение": "Направьте, пожалуйста, ваш email и описание запроса — мы подготовим коммерческое предложение.",
}

def detect_answer(message_text):
    """
    Возвращает ответ по словарю ключевых слов.
    """
    text = message_text.lower()
    for keyword in RESPONSES:
        if keyword in text:
            return RESPONSES[keyword]
    return "Извините, я пока не знаю, как ответить на этот вопрос."

def send_whatsapp_message(body):
    """
    Отправляет сообщение через Twilio WhatsApp API
    """
    message = client.messages.create(
        body=body,
        from_=TWILIO_WHATSAPP,
        to=MY_WHATSAPP
    )
    return message.sid


def main():
    print("ZALMA WhatsApp Bot запущен.")
    print("Сообщение будет отправлено на указанный ваш WhatsApp-номер для теста.")

    while True:
        user_input = input("Введите входящее WhatsApp-сообщение (или 'выход'): ")
        if user_input.lower() in ['выход', 'quit', 'exit']:
            print("Завершение работы бота.")
            break

        reply = detect_answer(user_input)
        sid = send_whatsapp_message(reply)
        print("Ответ отправлен. SID:", sid)


if __name__ == "__main__":
    main()
