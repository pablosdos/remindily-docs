============
Run locally
============

Telegram Bot
===============================

Use shell commands as follows to create and run Telegram Bot:

.. code-block:: sh

    cd /path/to/project-directory
    cp .env-dev .env


Create Telegram Bot and paste API key to .env-file. Create Venv, install dependencies and run the bot:

.. code-block:: sh

    cd /path/to/project-directory
    pipenv shell
    pipenv install
    pipenv run python client/bots/TelegramBotDev/main.py
