# CoverTele - A private covert channel over the Telegram
Tool and library to provide a simple way to exchange private text messages through the blocking-based covert channels between users written in Python. 

## Installation
- Clone this repo: `git clone https://github.com/LabunskyA/covertele` 
- Acquire Telegram api_id and api_hash following [this manual](https://core.telegram.org/api/obtaining_api_id).
- Edit covertele.py: set `api_id` and `api_hash` in the file header to your values.
- Done

### Dependencies
Python 3 is required to run covertele.
You will also need [Telethon](https://github.com/LonamiWebs/Telethon) to be installed as it is used to call Telegram API methods.
You can install it with pip: `pip install telethon`

## Usage
### Command-line tool
~~~
python3 covertele.py [-s/-r] [your username] [other username] [message]
~~~
Example to get message as user @mark from @tony you can call:
~~~
python3 covertele.py -r mark tony
~~~
And to send message "OH, HI MARK!..." from @tony to @mark do this after mark has started listening:
~~~
python3 covertele.py -s tony mark oh, hi mark!..
~~~

### API
Here is a basic usage example:
~~~
from covertele import TelegramBlockingAPI
from cochannel import CovertChannel


# To channel to use telegram you will need to create a suitable interface
# By default standard IO will be used to authorize you, 
# but you can do it automatically if you want to (see the source code)
id = input("Enter your id")
api = TelegramBlockingAPI(id)

# Now you can create channel object
friend = input("Enter your friend's id:")
channel = CovertChannel(api, friend)

# You can use channel.receive() and channel.send() to transmit data between the users
channel.send("Bork, bork!")
print(channel.receive) 

# If you want to send and receive raw codes, you can call functions with '_raw' suffix
codes = channel.receive_raw()
for code in codes:
    check_correct(code)
channel.send_raw([19, 24, 24, 13])
~~~

## Licence
Simplified BSD, see [LICENSE](LICENSE) file.
