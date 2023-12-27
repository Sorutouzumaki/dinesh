import logging
import random
from telegram import Update
from telegram.ext import Updater, CommandHandler, CallbackContext

# Set your Telegram bot token here
TOKEN = "YOUR_BOT_TOKEN"
updater = Updater(token=TOKEN, use_context=True)
dispatcher = updater.dispatcher

logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)

# Command to get user ID
def get_id(update: Update, context: CallbackContext) -> None:
    user_id = update.message.from_user.id
    update.message.reply_text(f"Your Telegram ID is {user_id}")

# Command to get weather (replace with your own weather API or service)
def get_weather(update: Update, context: CallbackContext) -> None:
    update.message.reply_text("Sorry, I don't have access to a weather API right now.")

# Command to get current time
def get_time(update: Update, context: CallbackContext) -> None:
    # You can customize the time format as needed
    current_time = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    update.message.reply_text(f"The current time is {current_time}")

# Command to promote a user
def promote(update: Update, context: CallbackContext) -> None:
    user = update.message.reply_to_message.from_user
    update.message.reply_text(f"{user.first_name} has been promoted!")

# Command to demote a user
def demote(update: Update, context: CallbackContext) -> None:
    user = update.message.reply_to_message.from_user
    update.message.reply_text(f"{user.first_name} has been demoted!")

# Command to spam (just echoes the message for demonstration purposes)
def spam(update: Update, context: CallbackContext) -> None:
    message_text = " ".join(context.args)
    update.message.reply_text(message_text)

# Command to mute a user
def mute(update: Update, context: CallbackContext) -> None:
    user = update.message.reply_to_message.from_user
    update.message.reply_text(f"{user.first_name} has been muted!")

# Command to ban a user
def ban(update: Update, context: CallbackContext) -> None:
    user = update.message.reply_to_message.from_user
    update.message.reply_text(f"{user.first_name} has been banned!")

# Command to kick a user
def kick(update: Update, context: CallbackContext) -> None:
    user = update.message.reply_to_message.from_user
    update.message.reply_text(f"{user.first_name} has been kicked!")

# Command for a coin toss
def toss(update: Update, context: CallbackContext) -> None:
    result = random.choice(["Heads", "Tails"])
    update.message.reply_text(f"The coin landed on: {result}")

# Command for a cricket match
def cricket(update: Update, context: CallbackContext) -> None:
    result = random.choice(["Team A wins!", "Team B wins!", "It's a draw!"])
    update.message.reply_text(result)

# Command for a judge to randomly evaluate true or false
def judge(update: Update, context: CallbackContext) -> None:
    result = random.choice(["True", "False"])
    update.message.reply_text(f"The judge's decision is: {result}")

# Add CommandHandlers to the dispatcher
dispatcher.add_handler(CommandHandler("id", get_id))
dispatcher.add_handler(CommandHandler("weather", get_weather))
dispatcher.add_handler(CommandHandler("time", get_time))
dispatcher.add_handler(CommandHandler("promote", promote))
dispatcher.add_handler(CommandHandler("demote", demote))
dispatcher.add_handler(CommandHandler("spam", spam))
dispatcher.add_handler(CommandHandler("mute", mute))
dispatcher.add_handler(CommandHandler("ban", ban))
dispatcher.add_handler(CommandHandler("kick", kick))
dispatcher.add_handler(CommandHandler("toss", toss))
dispatcher.add_handler(CommandHandler("cricket", cricket))
dispatcher.add_handler(CommandHandler("judge", judge))

# Start the bot
updater.start_polling()

# Run the bot until you press Ctrl-C to exit
updater.idle()
