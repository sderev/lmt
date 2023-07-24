# LMT: The CLI Tool for ChatGPT

`lmt` is the primary tool of the [LLM-Toolbox](https://github.com/sderev/llm-toolbox) and a versatile CLI interface tool that allows you to interact directly with OpenAI's ChatGPT models.

As a crucial component of the LLM-Toolbox, `lmt` exemplifies the toolbox's dedication to provide powerful and flexible tools that harness the capabilities of language models. It allows access to all available models of ChatGPT, including gpt-3.5-turbo, gpt-3.5-turbo-16k, gpt-4, and gpt-4-32k.

Furthermore, `lmt` enables you to design and use your own templates, broadening its potential applications. The ability to read from `stdin` using pipes also allows for convenient integration with other command-line tools.

If you find this project beneficial, consider expressing your support by giving it a star ⭐😊.

![cioran](https://github.com/sderev/lmt/assets/24412384/2e79cc97-903a-46ee-8a48-c5e42dbf7a63)

<!-- TOC -->
## Table of Contents

1. [Features](#features)
1. [Installation](#installation)
    1. [`pip`](#pip)
    1. [`pipx`, the Easy Way](#pipx-the-easy-way)
    1. [Installing `lmt` with `pipx`](#installing-lmt-with-pipx)
    1. [Cloning the `lmt` Repository](#cloning-the-lmt-repository)
1. [Getting Started](#getting-started)
    1. [Configuring your OpenAI API key](#configuring-your-openai-api-key)
1. [Usage](#usage)
    1. [Basic Example](#basic-example)
    1. [Add a Persona](#add-a-persona)
    1. [Switching Models](#switching-models)
    1. [Template Utilization](#template-utilization)
    1. [Emoji Integration](#emoji-integration)
    1. [Prompt Cost Estimation](#prompt-cost-estimation)
    1. [Reading from stdin](#reading-from-stdin)
    1. [Output Redirection](#output-redirection)
1. [Theming Colors for Code Blocks](#theming-colors-for-code-blocks)
    1. [Example](#example)
1. [License](#license)
1. [Upcoming Features](#upcoming-features)
<!-- /TOC -->

## Features

* **Access All ChatGPT Models**: `lmt` supports all available ChatGPT models (gpt-3.5-turbo, gpt-3.5-turbo-16k, gpt-4, gpt-4-32k), giving you the power to choose the most suitable one for your task.
* **Custom Templates**: Design and use your personalized toolbox of templates to streamline and automate your workflow.
* **Read From `stdin`**: Using pipes, `lmt` can read from `stdin`, enabling you to use file content as a prompt.
* **Command-Line & Template Requests**: `lmt` offers the flexibility of making requests directly from the command line or using pre-designed templates.
* **Vim Integration**: As a CLI tool, it can easily be integrated in Vim as a filter command. 

## Installation

### `pip`

```bash
python3 -m pip install lmt-cli
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
pipx install lmt-cli
```

If you want to follow the `main` branch:

```bash
pipx install git+https://github.com/sderev/lmt
```

To upgrade it:

```bash
pipx upgrade lmt-cli
```

### Cloning the `lmt` Repository

You can clone this repository with the following command:

```bash
git clone https://github.com/sderev/lmt.git
```

## Getting Started

### Configuring your OpenAI API key

For LMT to work properly, it is necessary to acquire and configure an OpenAI API key. Follow these steps to accomplish this:

1. **Acquire the OpenAI API key**: You can do this by creating an account on the [OpenAI website](https://platform.openai.com/account/api-keys). Once registered, you will have access to your unique API key.

2. **Set usage limit**: Before you start using the API, you need to define a usage limit. You can configure this in your OpenAI account settings by navigating to *Billing -> Usage limits*.

3. **Configure the OpenAI API key**: Once you have your API key, you can set it up by running the `lmt key set` command.

    ```bash
    lmt key set
    ```

With these steps, you should now have successfully set up your OpenAI API key, ready for use with the LMT.

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
lmt prompt "Tell me what you think of large language models." \
        --system "You are Cioran. You write like Cioran."
```

In this case, the model will generate a response based on its understanding of Cioran's writing style and perspective.

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

For instance, if you want to use the `gpt-4` model, simply include `-m 4` in your command.

### Template Utilization

Templates, stored in `~/.config/lmt/templates` and written in YAML, can be generated using the following command:

```bash
lmt templates add
```

**For help regarding the `templates` subcommand, use**:

```bash
lmt templates --help
```

**Here's an example of invoking a template named "cioran"**:

```bash
lmt prompt "Tell me how AI will change the world." --template cioran
```

You can also use the shorter version: `-t cioran`.

### Emoji Integration

To infuse a touch of emotion into your requests, append the `--emoji` flag option.

### Prompt Cost Estimation

For an estimation of your prompt's cost before sending, utilize the `--tokens` flag option.

### Reading from stdin

`lmt` facilitates reading inputs directly from `stdin`, allowing you to pipe in the content of a file as a prompt. This feature can be particularly useful when dealing with longer or more complex prompts, or when you want to streamline your workflow by incorporating `lmt` into a larger pipeline of commands.

To use this feature, you simply need to pipe your content into the `lmt` command like this:

```bash
cat your_file.txt | lmt prompt
```

In this example, `lmt` would use the content of `your_file.txt` as the input for the `prompt` command.

Also, remember that you can still use all other command line options with `stdin`. For instance, you might run:

```bash
cat your_file.py | lmt prompt \
        --system "You explain code in the style of \
        a fast-talkin' wise guy from a 1940's gangster movie" \
        -m 4 --emoji
```

In this example, `lmt` takes the content of `your_file.py` as the input for the `prompt` command. With the `gpt-4` model selected via `-m 4`, the system is instructed to respond in the style of a fast-talking wiseguy from a 1940s gangster movie, as specified in the `--system` option. The `--emoji` flag indicates that the response may include emojis for added expressiveness.

### Output Redirection

You can use output redirections with the tools. For instance:

```bash
lmt prompt "List 5 Wikipedia articles" --raw > wiki_articles.md
```

## Theming Colors for Code Blocks

Once you used `lmt`, you should have a configuration file (`~/.config/lmt/config.json`) in which you can configure the colors for inline code and code blocks.

Here are the styles for the code blocks: <https://pygments.org/styles/>

As for the inline code blocks, they can be styled with the 256 colors (names or hexadecimal code).

### Example

```json
{
    "code_block_theme": "autumn",
    "inline_code_theme": "blue on #f0f0f0"
}
```

## License

`lmt` is licensed under Apache License version 2.0.

## Upcoming Features

While `lmt` already boasts a wide array of features, development is ongoing. Expect more features and improvements in the future!

___

<https://github.com/sderev/lmt>
