# Task No.1: CHATBOT WITH RULE-BASED RESPONSES
Build a simple chatbot that responds to user inputs based on predefined rules. Use if-else statements or pattern matching techniques to identify user queries and provide appropriate responses. This will give you a basic understanding of natural language processing and conversation flow.

![image](https://github.com/KhanRayyan3622/codsoft_taskno.1/assets/92469975/43ef5784-67b0-47ac-9b87-1e6c326be66f)

# CODE
import random
import re

class SupportBot:
    negative_res = ("no", "nope", "nahi", "nay", "not a chance", "sorry")
    exit_commands = ("end", "quit", "pause", "exit", "goodbye", "bye", "farewell")

    def __init__(self):
        self.support_responses = {
            'ask_about_product': r'.*\s*product.*',
            'technical_support': r'.*technical.*support.*',
            'about_returns': r'.*\s*returnpolicy.*',
            'general_query': r'.*how.*help.*',
        }

    def greet(self):
        self.name = input("Hello! Welcome to our customer support. What's your name?\n")
        will_help = input(f"Hi {self.name}, how can I assist you today?\n")
        if will_help in self.negative_res:
            print("Alright, have a great day!")
            return
        self.chat()

    def make_exit(self, reply):
        for command in self.exit_commands:
            if command in reply:
                print("thanks for reaching out, have a great day!")
                return True
        return False

    def chat(self):
        reply = input("Please tell me your query: ").lower()
        while not self.make_exit(reply):
            reply = input(self.match_reply(reply))

    def match_reply(self, reply):
        for intent, regex_pattern in self.support_responses.items():
            found_match = re.search(regex_pattern, reply)
            if found_match and intent == 'ask_about_product':
                return self.ask_about_product()
            elif found_match and intent == 'technical_support':
                return self.technical_support()
            elif found_match and intent == 'about_returns':
                return self.about_returns()
            elif found_match and intent == 'general_query':
                return self.general_query()
        return self.no_match_intent()

    def ask_about_product(self):
        responses = ["Our product is topnotch and has excellent results!\n",
                     "You can find all product details on our website.\n"]
        return random.choice(responses)

    def technical_support(self):
        responses = ["please visit our technical support page for detailed assistance.\n",
                     "You can also call our tech support helpline for immediate help.\n"]
        return random.choice(responses)

    def about_returns(self):
        responses = ["we have a 3-day return policy.\n",
                     "Please ensure the product is in its original condition when returning.\n"]
        return random.choice(responses)

    def general_query(self):
        responses = ["How can I assist you further?\n",
                     "Is there anything else you'd like to know?\n"]
        return random.choice(responses)

    def no_match_intent(self):
        responses = ["I'm sorry, I didn't quite understand that. Can you please rephrase?\n",
                     "My apologies, can you provide more details?\n"]
        return random.choice(responses)

bot = SupportBot()
bot.greet()


