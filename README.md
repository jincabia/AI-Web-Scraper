AI Web Scraper

This repository contains an AI-powered web scraping tool that leverages Selenium, BeautifulSoup, LangChain, and Ollama3.1. This project enables efficient web scraping, content extraction, and intelligent parsing using Ollama3.1 for insightful data handling and summarization.
Features

    Automated Web Scraping: Utilizes Selenium to navigate and scrape website content programmatically.
    Content Extraction: Processes and cleans HTML content using BeautifulSoup, extracting relevant data for further analysis.
    Intelligent Parsing with Ollama3.1: Processes scraped content with Ollama3.1, providing structured and insightful parsing and summarization.
    LangChain Integration: Utilizes LangChain for structured processing, enabling multi-step workflows and chain-of-thought reasoning on the scraped data.

Installation

To set up this project locally, follow these steps:

    Clone the repository:

    bash

git clone https://github.com/jincabia/AI-Web-Scraper.git
cd AI-Web-Scraper

Install dependencies: Ensure you have Python 3.7 or higher installed.

bash

    pip install -r requirements.txt

    Download and Configure Chromedriver: Make sure chromedriver is installed and in your PATH. This project uses Chrome to render web pages, so update chromedriver as per your Chrome version.

Usage

    Run the UI using "streamlit run main.py"
    Enter a URL to scrape, wait for content to be returned
    Enter the next prompt, "What do you want parsed?"
    Then allow Ollama to complete parsing through the content from web scraping.
    

    
    
Example Code Snippet

    Here's a brief example of how the scraper works:
    
    python
    
    from langchain_ollama import OllamaLLM
    from langchain_core.prompts import ChatPromptTemplate
    
    
    template = (
        "You are tasked with extracting specific information from the following text content: {dom_content}. "
        "Please follow these instructions carefully: \n\n"
        "1. **Extract Information:** Only extract the information that directly matches the provided description: {parse_description}. "
        "2. **No Extra Content:** Do not include any additional text, comments, or explanations in your response. "
        "3. **Empty Response:** If no information matches the description, return an empty string ('')."
        "4. **Direct Data Only:** Your output should contain only the data that is explicitly requested, with no other text."
    )

    model = OllamaLLM(model="llama3.1")
    
    def parse_with_ollama(dom_chunks,parse_desc):
        prompt = ChatPromptTemplate.from_template(template)
        chain = prompt | model 

    parsed_results = []

    for i, chunk in enumerate(dom_chunks,start=1):
        response = chain.invoke(
            {"dom_content":chunk,"parse_description":parse_desc}
            )
        print(f"Parsed Batch {i} of {len(dom_chunks)}")

        parsed_results.append(response)

    return "\n".join(parsed_results)
 

Dependencies

    Selenium: Automates web interactions
    BeautifulSoup: Parses HTML content
    LangChain: Manages advanced workflows
    Ollama3.1: Performs natural language parsing and summarization



Contributions are welcome! Feel free to open issues or submit pull requests to enhance this project.
License

This project is licensed under the MIT License.
