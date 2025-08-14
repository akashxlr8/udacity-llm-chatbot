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

## How It Works
1. **Data Wrangling**: Loads and cleans the fashion trends dataset, creating a `text` column for chatbot context.
2. **Prompt Engineering**: Builds custom prompts that incorporate relevant fashion trend information.
3. **Custom Query System**: Sends user questions to OpenAI with fashion context for expert responses.
4. **Comparison & Validation**: Demonstrates the difference between generic and custom responses.

## Getting Started
1. Open `project.ipynb` in Jupyter or VS Code.
2. Ensure you have the required Python packages (`pandas`, `openai`, `python-dotenv`).
3. Add your OpenAI API key and base URL to a `.env` file.
4. Run the notebook cells to explore the chatbot and its features.

## Requirements
- At least 20 rows of fashion trend data with a `text` column.
- OpenAI API access (see notebook for setup instructions).

## Example Usage
- Ask questions like "What colors should I wear this year?" or "How should I style denim pieces for a modern look?" and receive expert, trend-aware advice.

## License
This project is for educational purposes and demonstration only. Dataset sources include Refinery29, InStyle, Glamour, and Vogue.
