# `lmt`: The CLI Tool for ChatGPT

`lmt` is the primary tool of the [LLM-Toolbox](https://github.com/sderev/llm-toolbox) and a versatile command-line interface tool that allows you to interact directly with OpenAI's ChatGPT models. With `lmt`, you can bring the power of artificial intelligence to your terminal, utilizing.

As a crucial component of the LLM-Toolbox, `lmt` exemplifies the toolbox's dedication to providing powerful, flexible tools that harness the capabilities of language models. It allows access to all available models of ChatGPT, including gpt-3.5-turbo, gpt-3.5-turbo-16k, gpt-4, and gpt-4-32k.

Furthermore, `lmt` enables you to design and use your own templates, broadening its potential applications. The ability to read from `stdin` using pipes also allows for convenient integration with other command-line tools.


<!-- TOC -->
## Table of Contents

1. [Features](#features)
1. [Installation](#installation)
    1. [`pip`](#pip)
    1. [`pipx`, the Easy Way](#pipx-the-easy-way)
    1. [Installing `lmt` with `pipx`](#installing-lmt-with-pipx)
    1. [Cloning the `lmt` Repository](#cloning-the-lmt-repository)
1. [Getting Started](#getting-started)
    1. [Set your OpenAI API key](#set-your-openai-api-key)
1. [Usage](#usage)
1. [Usage](#usage)
    1. [Basic Example](#basic-example)
    1. [Add a Persona](#add-a-persona)
    1. [Switching Models](#switching-models)
    1. [Switching Models](#switching-models)
    1. [Template Utilization](#template-utilization)
    1. [Emoji Integration](#emoji-integration)
    1. [Prompt Cost Estimation](#prompt-cost-estimation)
1. [License](#license)
1. [Upcoming Features](#upcoming-features)
<!-- /TOC -->

## Features

* **Access All ChatGPT Models**: `lmt` supports all available ChatGPT models (gpt-3.5-turbo, gpt-3.5-turbo-16k, gpt-4, gpt-4-32k), giving you the power to choose the most suitable one for your task.
* **Custom Templates**: Design and use your personalized toolbox of templates to streamline and automate your workflow.
* **Read From `stdin`**: Using pipes, `lmt` can read from `stdin`, enabling you to use file content as a prompt.
* **Command-Line & Template Requests**: `lmt` offers the flexibility of making requests directly from the command line or using pre-designed templates.

**TODO: Video Demo**: A video demo showcasing `lmt`'s features will be added here.

## Installation

### `pip`

```bash
python3 -m pip install llm-toolbox
```

### `pipx`, the Easy Way

To use these tools, I recommend that you first install [pipx](https://pypa.github.io/pipx/installation/). It's a package manager for Python that makes the installation and upgrade of CLI apps easy (no more hassle with virtual environments 😌).

* Debian / Ubuntu

    ```bash
    sudo apt install pipx
    ```

* macOS    

    ```bash
    brew install pipx
    ```

### Installing `lmt` with `pipx`

To install the latest stable version of `lmt`, simply run this command:

```bash
pipx install lmt
```

If you want to follow the `main` branch:

```bash
pipx install git+https://github.com/sderev/lmt
```

To upgrade it:

```bash
pipx upgrade lmt
```

### Cloning the `lmt` Repository

You can clone this repository with the following command:

```bash
git clone https://github.com/sderev/lmt.git
```

## Getting Started

### Set your OpenAI API key

LLM-Toolbox requires an OpenAI API key to function. You can obtain a key by signing up for an account at [OpenAI's website](https://platform.openai.com/account/api-keys).

You need to set some usage limit before to be able to use the API. You can configure on your OpenAI account in *Billing -> Usage limits*.

Once you have your API key, set it as an environment variable:

* On macOS and Linux:

  ```bash
  export OPENAI_API_KEY="your-api-key-here"
  ```

  To avoid having to type it everyday, you can create a file with the key:

  ```bash
  echo "your-api-key" > ~/.openai-api-key.txt
  ```

  **Note:** Remember to replace `"your-api-key"` with your actual API key.

  And then, you can add this to your shell configuration file (`.bashrc`, `.zshrc`, etc.):

    ```bash
    export OPENAI_API_KEY="$(cat ~/.openai-api-key.txt)"
    ```

* On Windows:

  ```
  setx OPENAI_API_KEY your_key
  ```

## Usage

Absolutely! Here's your revised Usage section:

---

## Usage

The `lmt` CLI tool is equipped with a helpful `--help` flag that displays useful information about how to use the tool and its commands.

**For a general overview of all commands, you can type**:

```bash
lmt --help
```

**If you want detailed information about a specific command, such as `prompt`, you can display its help message like so**:

```bash
lmt prompt --help
```

### Basic Example

The simplest way to use `lmt` is by entering a prompt for the model to respond to.

**Here's a basic usage example where we ask the model to generate a greeting**:

```bash
lmt prompt "Say hello"
```

In this case, the model will generate and return a greeting based on the given prompt.

### Add a Persona

You can also instruct the model to adopt a specific persona using the `--system` flag. This is useful when you want the model's responses to emulate a certain character or writing style.

**Here's an example where we instruct the model to write like the philosopher Cioran**:

```bash
lmt prompt "Tell me what you think of the large language models." --system "You are Cioran. You write like Cioran."
```

In this case, the model will generate a response based on its understanding of Cioran's writing style and perspective.

### Switching Models

Sure, here's a reviewed and slightly enhanced version of your text:

### Switching Models

Switching between different models is a breeze with `lmt`. Use the `-m` flag followed by the alias of the model you wish to employ.

```bash
lmt prompt "Explain what is a large language model" -m 4
```

Below is a table outlining available model aliases for your convenience:

| Alias | Corresponding Model |
| --- | --- |
| chatgpt | gpt-3.5-turbo |
| chatgpt-16k | gpt-3.5-turbo-16k |
| 3.5 | gpt-3.5-turbo |
| 3.5-16k | gpt-3.5-turbo-16k |
| 4 | gpt-4 |
| gpt4 | gpt-4 |
| 4-32k | gpt-4-32k |
| gpt4-32k | gpt-4-32k |

For instance, if you want to use the `gpt-4-32k` model, simply include `-m 4-32k` in your command.

### Template Utilization

Templates, stored in `~/.config/lmt/templates` and written in YAML, can be effortlessly generated using the following command:

```bash
lmt templates add
```

For help regarding the `templates` subcommand, use:

```bash
lmt templates --help
```

**Here's an example of invoking a template named "cioran"**:

```bash
lmt prompt "Tell me how AI will change the world." --template cioran
```

### Emoji Integration

To infuse a touch of emotion into your requests, append the `--emoji` flag option.

### Prompt Cost Estimation

For an estimation of your prompt's cost before sending, utilize the `--tokens` flag option.

## License

`lmt` is licensed under Apache License version 2.0.

## Upcoming Features

While `lmt` already boasts a wide array of features, development is ongoing. Expect more features and improvements in the future!

___

<https://github.com/sderev/lmt>

