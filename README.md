---
title: AutoQuizzer
emoji: 🧑‍🏫
colorFrom: purple
colorTo: blue
sdk: gradio
sdk_version: 4.31.1
app_file: app.py
header: mini
pinned: true
models: [meta-llama/Meta-Llama-3-8B-Instruct]
---

# 🧑‍🏫 AutoQuizzer

Generates a quiz from a URL. You can play the quiz, or let the LLM play it.

Built using: [🏗️ Haystack](https://haystack.deepset.ai/) • 🦙 Llama 3 8B Instruct • ⚡ Groq

<!--- Include in Info tab -->

## How does it work?

![AutoQuizzer](autoquizzer.png)

- **Quiz generation Pipeline**: downloads HTML content from the URL, extracts the text and passes it to Llama 3 to generate a quiz in JSON format.
- You can play the quiz and get a score.
- You can let Llama 3 play the quiz:
  - **closed book answer Pipeline**: the LLM is provided given the general quiz topic and questions. It can answer the questions based on its parametric knowledge and reasoning abilities.
  - **Web RAG answer Pipeline**: for each question, a Google search is performed and the top 3 snippets are included in the prompt for the LLM.

## How to run it locally?

- Clone the repo: `git clone https://github.com/anakin87/autoquizzer`
- Install: `cd autoquizzer && pip install -r requirements.txt`
- Export two environment variables:
  - `GROQ_API_KEY`: API key for the [Groq API](https://groq.com/), used to serve Llama 3.
  - `SERPERDEV_API_KEY`: API key for the [SerperDev API](https://serper.dev/), used to fetch search results.
- Run the webapp: `gradio app.py`

## Customization and potential improvements
- We are using the `OpenAIGenerator` to query Llama 3 on Groq. You can use an OpenAI model with the same generator. You can also use a different generator ([Haystack generators](https://docs.haystack.deepset.ai/docs/generators)).
- In the quiz generation pipeline, we ask the model to generate a JSON. Llama-3-8B-Instruct usually works. You can also create a more robust JSON generation pipeline, as shown in this tutorial: [Generating Structured Output with Loop-Based Auto-Correction](https://haystack.deepset.ai/tutorials/28_structured_output_with_loop).
