
# Fashion Advisor Chatbot Project

This project demonstrates a custom chatbot that provides expert-level fashion advice using the 2023 Fashion Trends dataset. The chatbot leverages OpenAI's Completion model and integrates domain-specific data to deliver personalized, trend-aware recommendations.

## Project Structure

- `project.ipynb`: Main notebook containing all code, explanations, and demonstrations.
- `2023_fashion_trends.csv`: Dataset with 2023 fashion trend descriptions from authoritative sources.
- `character_descriptions.csv`, `nyc_food_scrap_drop_off_sites.csv`: Additional datasets (not used in the main chatbot demo).

## Key Features

- **Custom Data Integration**: Uses the 2023 Fashion Trends dataset to provide context-rich, expert advice.
- **OpenAI Model Usage**: Compares basic OpenAI responses with custom, data-driven answers.
- **Interactive Demo**: Includes an interactive loop for users to ask fashion questions and receive tailored advice.
- **Performance Comparison**: Shows clear improvements in response quality when using custom data.
- **Modular Code**: Functions for prompt creation, querying, and comparison are provided for easy extension.

## How It Works

1. **Data Wrangling**: Loads and cleans the fashion trends dataset, creating a `text` column for chatbot context.
2. **Prompt Engineering**: Builds custom prompts that incorporate relevant fashion trend information.
3. **Custom Query System**: Sends user questions to OpenAI with fashion context for expert responses.
4. **Comparison & Validation**: Demonstrates the difference between generic and custom responses.

## Getting Started

1. Open `project.ipynb` in Jupyter or VS Code.
2. Ensure you have the required Python packages:
   - `pandas`
   - `openai`
   - `python-dotenv`
3. Add your OpenAI API key and base URL to a `.env` file:
   ```env
   VOCERUM_API_KEY=your_openai_api_key
   VOCERUM_BASE_URL=https://api.openai.com/v1
   ```
4. Run the notebook cells to explore the chatbot and its features.

## Requirements

- At least 20 rows of fashion trend data with a `text` column.
- OpenAI API access (see notebook for setup instructions).

## Example Code Snippets

### 1. Load and Inspect the Dataset

```python
import pandas as pd
df = pd.read_csv('2023_fashion_trends.csv')
print(df.head())
```

### 2. Create the `text` Column

```python
df['text'] = df['Trends'].copy()
df['text'] = df['text'].str.replace('"', '').str.replace('""', '').str.strip()
```

### 3. Custom Prompt Creation

```python
def create_custom_prompt(user_question, fashion_data, max_context_length=1500):
    context_texts = []
    total_length = 0
    for text in fashion_data['text']:
        if total_length + len(text) < max_context_length:
            context_texts.append(text)
            total_length += len(text)
        else:
            break
    context = "\n\n".join(context_texts)
    custom_prompt = f"""You are a fashion expert advisor with access to the latest 2023 fashion trends.\n\nFASHION TRENDS CONTEXT:\n{context}\n\nQuestion: {user_question}\nAnswer:"""
    return custom_prompt
```

### 4. Query OpenAI for Fashion Advice

```python
from openai import OpenAI
import os
from dotenv import load_dotenv
load_dotenv()
client = OpenAI(
    api_key=os.getenv("VOCERUM_API_KEY"),
    base_url=os.getenv("VOCERUM_BASE_URL"),
)

def fashion_advisor_query(user_question, fashion_data, max_tokens=200, temperature=0.7):
    custom_prompt = create_custom_prompt(user_question, fashion_data)
    response = client.chat.completions.create(
        model="gpt-4.1-mini",
        messages=[
            {"role": "system", "content": "You are a fashion advisor who gives personalized outfit suggestions."},
            {"role": "user", "content": custom_prompt}
        ],
        max_tokens=max_tokens,
        temperature=temperature
    )
    return response.choices[0].message.content.strip()
```

### 5. Interactive Demo

```python
while True:
    user_question = input("Your question: ")
    if user_question.strip().lower() in ['exit', 'quit']:
        print("Thank you for using the Fashion Advisor. Goodbye!")
        break
    response = fashion_advisor_query(user_question, df)
    print("Fashion Advisor Response:")
    print(response)
```

## Example Usage

- Ask questions like "What colors should I wear this year?" or "How should I style denim pieces for a modern look?" and receive expert, trend-aware advice.

## Troubleshooting

- If you encounter API errors, check your `.env` file and ensure your API key and base URL are correct.
- Make sure all required packages are installed. You can install missing packages with:
  ```bash
  pip install pandas openai python-dotenv
  ```
- If the dataset is missing or columns are misnamed, verify the CSV file and column headers.

## License

This project is for educational purposes and demonstration only. Dataset sources include Refinery29, InStyle, Glamour, and Vogue.
