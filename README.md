# TeleBot

import telebot
import random
token = "5475253815:AAG4mql9Il1ZuqyuLgwlhp7yKVVuDpzQlqM"
bot = telebot.TeleBot(token)
RANDOM_TASKS = ["Записаться на курс в Нетологию", "Написать Гвидо письмо", "Покормить кошку",
"Помыть машину"]
HELP_"
/help - вывести список доступных команд
/add - добавим задачу в список(название задачи запрашивем
у пользователя)
/show - напечатать все добавленные задачи
/random - добавить случайную задачу на дату Сегодня"""
tasks={}
def add_todo(date, task):
  if date in tasks:
    tasks[date].append(task)
  else:
    tasks[date]=[]
    tasks[date].append(task)
@bot.message_handler(commands=["help"])
def help(message):
    bot.send_message(message.chat.id, HELP)
@bot.message_handler(commands=["add"])
def add(message):
    command = message.text.split(maxsplit=2)
    date = command[1].lower()
    task = command[2]
    add_todo(date, task)
    text="Задача " + task + " добавлена на дату " +  date 
    bot.send_message(message.chat.id, text)
@bot.message_handler(commands=["random"])
def random_add(message):
    date = "сегодня"
    task = random.choice(RANDOM_TASKS)
    add_todo(date, task)
    text="Задача" + task + " добавлена на дату " + date
    bot.send_message(message.chat.id, text)
@bot.message_handler(commands=["show", "print"])
def show(message):
    command = message.text.split(maxsplit=1)
    date = command[1].lower()
    text=""
    if date in tasks:
      text = date.upper() + "\n"
      for task in tasks[date]:
        text = text + "@ " + task + "\n"
