# Universal Telegram Bot Library

 https://ldijkman.github.io/async-esp-fs-webserver/ino/thermostat_web_flash/Telegram_WebApp/Telegram_WebApp.html

# video

# https://t.me/Luberth_Dijkman/84


if https://t.me/LuberthDijkmanbot/schedule

is opened in another way as via bottom keyboard key, reply keyboard?

it is not sending the data
 
<pre>

 
#made changes for WebApp bottom keyboard to open webapp
 so webapp can send without external servers
 
bool sendMessageWithReplyKeyboard(const String& chat_id, const String& text,
                                   const String& parse_mode, const String& keyboard,
                                   bool resize = false, bool oneTime = false,
                                   bool selective = false, const String& web_app_url = "");

and trying to get webappdata
struct telegramMessage {
  String text;
  String chat_id;
  String chat_title;
  String from_id;
  String from_name;
  String date;
  String type;
  String file_caption;
  String file_path;
  String file_name;
  String web_app_data; // Add this line to store web app data
  bool hasDocument;
  long file_size;
  float longitude;
  float latitude;
  int update_id;
  int message_id;  

  int reply_to_message_id;
  String reply_to_text;
  String query_id;
};


</pre>

![telegram_arduino_esp8266_web_app_data](https://github.com/ldijkman/Universal-Arduino-Telegram-Bot/assets/45427770/867ee0c3-c730-43ad-b150-a93327b8c87f)


![Travis CI status](https://api.travis-ci.org/witnessmenow/Universal-Arduino-Telegram-Bot.svg?branch=master)
![License](https://img.shields.io/github/license/witnessmenow/Universal-Arduino-Telegram-Bot)
![Release stable](https://badgen.net/github/release/witnessmenow/Universal-Arduino-Telegram-Bot/stable)

An Arduino IDE library for using Telegram Bot API. It's designed to be used with multiple Arduino architectures.

Join the [Arduino Telegram Library Group Chat](https://t.me/arduino_telegram_library) if you have any questions/feedback or would just like to be kept up to date with the library's progress.

## Help support what I do!

I have created a lot of different Arduino libraries that I hope people can make use of. [If you enjoy my work, please consider becoming a Github sponsor!](https://github.com/sponsors/witnessmenow/)

## Introduction

This library provides an interface for [Telegram Bot API](https://core.telegram.org/bots/api).

Telegram is an instant messaging service that allows for the creation of bots. Bots can be configured to send and receive messages. This is useful for Arduino projects as you can receive updates from your project or issue it commands via your Telegram app from anywhere.

This is a library forked from [one library](https://github.com/Gianbacchio/ESP8266-TelegramBot) and inspired by [another](https://github.com/CasaJasmina/TelegramBot-Library)

Each library only supported a single type of Arduino and had different features implemented. The only thing that needs to be different for each board is the actual sending of requests to Telegram so I thought a library that additional architectures or boards could be configured easily would be useful, although this springs to mind:

![alt text](https://imgs.xkcd.com/comics/standards.png "standards")

## Installing

The downloaded code can be included as a new library into the IDE selecting the menu:

```
 Sketch / include Library / Add .Zip library
```

You also have to install the ArduinoJson library written by [Benoît Blanchon](https://github.com/bblanchon). Search for it on the Arduino Library manager or get it from [here](https://github.com/bblanchon/ArduinoJson).

## Getting Started

To generate your new Bot, you need an Access Token. Talk to [BotFather](https://telegram.me/botfather) and follow a few simple steps described [here](https://core.telegram.org/bots#botfather).

Include UniversalTelegramBot in your project:

```ino
#include <UniversalTelegramBot.h>
```

and pass it a Bot token and a SSL Client (See the [examples](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/tree/master/examples) for more details)

```ino
// Telegram BOT Token (Get from Botfather)
#define BOT_TOKEN "XXXXXXXXX:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
WiFiClientSecure secured_client;
UniversalTelegramBot bot(BOT_TOKEN, secured_client);
```

## Features

Here is a list of features that this library covers. (Note: The examples link to the ESP8266 versions)

| Feature                      | Description                                                                                                                                                                                                                                                                                                                  | Usage                                                                                                                                                                                                                                                                                                        | Example                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _Receiving Messages_         | Your bot can read messages that are sent to it. This is useful for sending commands to your arduino such as toggle and LED                                                                                                                                                                                                   | `int getUpdates(long offset)` <br><br> Gets any pending messages from Telegram and stores them in **bot.messages** . Offset should be set to **bot.last_message_received** + 1. Returns the numbers new messages received.                                                                                   | [FlashLED](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/blob/master/examples/ESP8266/FlashLED/FlashLED.ino) or any other example                                                                                                                                                                                                                                                                                                                          |
| _Sending messages_           | Your bot can send messages to any Telegram or group. This can be useful to get the arduino to notify you of an event e.g. Button pressed etc (Note: bots can only message you if you messaged them first)                                                                                                                    | `bool sendMessage(String chat_id, String text, String parse_mode = "")` <br><br> Sends the message to the chat_id. Returns if the message sent or not.                                                                                                                                                       | [EchoBot](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/blob/master/examples/ESP8266/EchoBot/EchoBot.ino#L51) or any other example                                                                                                                                                                                                                                                                                                                         |
| _Reply Keyboards_            | Your bot can send [reply keyboards](https://camo.githubusercontent.com/2116a60fa614bf2348074a9d7148f7d0a7664d36/687474703a2f2f692e696d6775722e636f6d2f325268366c42672e6a70673f32) that can be used as a type of menu.                                                                                                        | `bool sendMessageWithReplyKeyboard(String chat_id, String text, String parse_mode, String keyboard, bool resize = false, bool oneTime = false, bool selective = false)` <br><br> Send a keyboard to the specified chat_id. parse_mode can be left blank. Will return true if the message sends successfully. | [ReplyKeyboard](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/blob/master/examples/ESP8266/CustomKeyboard/ReplyKeyboardMarkup/ReplyKeyboardMarkup.ino)                                                                                                                                                                                                                                                                                                     |
| _Inline Keyboards_           | Your bot can send [inline keyboards](https://camo.githubusercontent.com/55dde972426e5bc77120ea17a9c06bff37856eb6/68747470733a2f2f636f72652e74656c656772616d2e6f72672f66696c652f3831313134303939392f312f324a536f55566c574b61302f346661643265323734336463386564613034). <br><br>Note: URLS & callbacks are supported currently | `bool sendMessageWithInlineKeyboard(String chat_id, String text, String parse_mode, String keyboard)` <br><br> Send a keyboard to the specified chat_id. parse_mode can be left blank. Will return true if the message sends successfully.                                                                   | [InlineKeyboard](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/blob/master/examples/ESP8266/CustomKeyboard/InlineKeyboardMarkup/InlineKeyboardMarkup.ino)                                                                                                                                                                                                                                                                                                  |
| _Send Photos_                | It is possible to send phtos from your bot. You can send images from the web or from the arduino directly (Only sending from an SD card has been tested, but it should be able to send from a camera module)                                                                                                                 | Check the examples for more info                                                                                                                                                                                                                                                                             | [From URL](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/blob/master/examples/ESP8266/SendPhoto/PhotoFromURL/PhotoFromURL.ino)<br><br>[Binary from SD](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/blob/master/examples/ESP8266/SendPhoto/PhotoFromSD/PhotoFromSD.ino)<br><br>[From File Id](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/blob/master/examples/ESP8266/SendPhoto/PhotoFromFileID/PhotoFromFileID.ino) |
| _Chat Actions_               | Your bot can send chat actions, such as _typing_ or _sending photo_ to let the user know that the bot is doing something.                                                                                                                                                                                                    | `bool sendChatAction(String chat_id, String chat_action)` <br><br> Send a the chat action to the specified chat_id. There is a set list of chat actions that Telegram support, see the example for details. Will return true if the chat actions sends successfully.                                         |
| _Location_                   | Your bot can receive location data, either from a single location data point or live location data.                                                                                                                                                                                                                          | Check the example.                                                                                                                                                                                                                                                                                           | [Location](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/tree/master/examples/ESP8266/Location/Location.ino)                                                                                                                                                                                                                                                                                                                                               |
| _Channel Post_               | Reads posts from channels.                                                                                                                                                                                                                                                                                                   | Check the example.                                                                                                                                                                                                                                                                                           | [ChannelPost](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/tree/master/examples/ESP8266/ChannelPost/ChannelPost.ino)                                                                                                                                                                                                                                                                                                                                      |
| _Long Poll_                  | Set how long the bot will wait checking for a new message before returning now messages. <br><br> This will decrease the amount of requests and data used by the bot, but it will tie up the arduino while it waits for messages                                                                                             | `bot.longPoll = 60;` <br><br> Where 60 is the amount of seconds it should wait                                                                                                                                                                                                                               | [LongPoll](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/tree/master/examples/ESP8266/LongPoll/LongPoll.ino)                                                                                                                                                                                                                                                                                                                                               |
| _Update Firmware and SPIFFS_ | You can update firmware and spiffs area through send files as a normal file with a specific caption.                                                                                                                                                                                                                         | `update firmware` <br>or<br>`update spiffs`<br> These are captions for example.                                                                                                                                                                                                                              | [telegramOTA](https://github.com/solcer/Universal-Arduino-Telegram-Bot/blob/master/examples/ESP32/telegramOTA/telegramOTA.ino)                                                                                                                                                                                                                                                                                                                                              | ``` |
| _Set bot's commands_         | You can set bot commands programmatically from your code. The commands will be shown in a special place in the text input area                                                                                                                                                                                               | `bot.setMyCommands("[{\"command\":\"help\", \"description\":\"get help\"},{\"command\":\"start\",\"description\":\"start conversation\"}]");`. See examples                                                                                                                                                  | [SetMyCommands](examples/ESP8266/SetMyCommands/SetMyCommands.ino)                                                                                                                                                                                                                                                                                                                                                                                                           |

The full Telegram Bot API documentation can be read [here](https://core.telegram.org/bots/api). If there is a feature you would like added to the library please either raise a Github issue or please feel free to raise a Pull Request.

## Other Examples

Some other examples are included you may find useful:

- BulkMessages : sends messages to multiple subscribers (ESP8266 only).

- UsingWifiManager : Same as FlashLedBot but also uses WiFiManager library to configure WiFi (ESP8266 only).

## License

![License](https://img.shields.io/github/license/witnessmenow/Universal-Arduino-Telegram-Bot)
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
