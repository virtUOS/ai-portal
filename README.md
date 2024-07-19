# kiwi

[kiwi](https://ki.uni-osnabrueck.de/) is a proxy to unify access to large language models for universities, currently tailored towards Open AI's chat models.

![screenshot.png](docs/assets/screenshot.png)

Some of its features are:
- Multi-language support (currently English and German)
- Simple interface for OpenAI's chat models
- LDAP support
- Modifiable chatbot prompts
- Ability to save and delete conversations
- Use images in your chats with GPT-4!
  - Upload images
  - Use image URLs
  - Take pictures with the camera

## Chat with Images Feature

![screenshot_images_1.png](docs/assets/screenshot_images_1.png)

![screenshot_images_2.png](docs/assets/screenshot_images_2.png)

# Usage & Configuration

We provide a docker container image in the GitHub repository.

You can configure the service using environment variables.
See the docker compose example below for the list of variables that you can set.
Additionally, you might want to change the logo by overwriting the existing logo in `/kiwi/img/logo.svg`

A docker compose file could look like this:

```yml
---
version: '3'
services:
  kiwi:
    image: ghcr.io/virtuos/kiwi:main
    container_name: kiwi
    restart: unless-stopped
    ports:
      - '127.0.0.1:8501:8501'
    environment:
      # App name (english, german):
      APP_NAME_EN: "Kiwi"
      APP_NAME_DE: "Kiwi"
      # OpenAI settings:
      OPENAI_API_KEY: "CHANGE!"
      OPENAI_MODELS: '{"models":["gpt-4o-mini","gpt-4o"]}'
      # Extra settings for models
      DEFAULT_MODEL: "gpt-4o"
      MULTI_MODELS: '{"models":["gpt-4o-mini","gpt-4o"]}'
      # User settings
      USER_ROLES: '{"user1":"open","user2":"restricted"}'
      MODELS_PER_ROLE: '{"restricted":["gpt-3.5-turbo"],"open":["gpt-3.5-turbo","gpt-4o"]}'
      # App customizations:
      # German service sites
      DATENSCHUTZ_DE: 'https://www.example.org/de/datenschutz/'
      IMPRESSUM_DE: 'https://www.example.org/de/impressum/'
      # English service sites
      DATENSCHUTZ_EN: 'https://www.example.org/en/privacy/'
      IMPRESSUM_EN: 'https://www.example.org/en/legal/'
      # Your Institution
      INSTITUTION_EN: "Osnabrück University"
      INSTITUTION_DE: "Universität Osnabrück"
      # LDAP settings:
      LDAP_SERVER: 'ldap.example.org'
      LDAP_PORT: 636
      LDAP_BASE_DN: 'ou=people,dc=example-org,dc=de'
      LDAP_USER_DN: 'uid={username},ou=people,dc=example-org,dc=de'
      LDAP_SEARCH_FILTER: '(uid={username})'
      # Cookie settings:
      COOKIES_PASSWORD: "CHANGE!"
      COOKIES_PREFIX: "virtuos/kiwi"
    volumes:
      # Here you can override the default logo of the app
      - './logo.svg:/kiwi/img/logo.svg'
      # You could do the same for the promtps:
      # - './chat_basic_prompts_de.yml:/kiwi/prompts_config/chat_basic_prompts_de.yml
      # - './chat_basic_prompts_en.yml:/kiwi/prompts_config/chat_basic_prompts_en.yml
```

## Development

The app is developed in the [streamlit](https://streamlit.io/) framework.

You can install the requirements needed to run and develop the app using `pip install -r requirements.txt`.
Then simply run a development server like this:

```bash
streamlit run start.py
```

## Community contributions

This app uses the following Streamlit community libraries:

- [streamlit-cookies-manager](https://github.com/ktosiek/streamlit-cookies-manager): Handles access cookies and user roles.
- [streamlit-float](https://github.com/bouzidanas/streamlit-float): Allows floating Streamlit containers to make the interface more flexible. Special thanks to its creator, bouzidanas, on the Streamlit forums for all the help.



## Authors

virtUOS
