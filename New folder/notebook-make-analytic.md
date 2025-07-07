---
link: https://notebooklm.google.com/notebook/b4624c29-6eeb-4ce9-92c2-44b1fb4d6719?original_referer=https:%2F%2Fnotebooklm.google%23&pli=1
---
This document provides a comprehensive overview of **make.com**, a no-code automation platform used for automating tasks and workflows across thousands of different software applications.

Here's a summary of the key concepts and features discussed:

- **What is make.com?**
    
    - It's a **no-code automation platform** that allows users to automate tasks and workflows across thousands of software applications.
    - It boasts a **drag-and-drop interface** and numerous built-in modules for working with various data types and structures.
    - Make.com is positioned as a middle-ground option between easier-to-use but less flexible platforms like Zapier and more technical but highly customisable ones like n8n. It is considered **easy to use yet offers significant flexibility and customisation**, often at a lower cost than Zapier.
    - It has **over 2,000 native integrations**, making it easier to connect to different software without custom APIs.
- **Why use make.com?**
    
    - To **automate business processes** and increase efficiency.
    - The integration of **AI has significantly enhanced its power**, enabling automation of more complex processes and advanced tasks, such as researching and qualifying leads with enriched data.
    - Automation, especially with AI, is becoming a **fundamental pillar for businesses** to remain competitive and efficient.
    - Examples of automations include automating newsletters, social media content generation, inbound lead qualification, and personalised outbound email campaigns.
- **Key Concepts/Terminology:**
    
    - **Scenarios:** The term make.com uses for a single workflow or automation system.
    - **Modules:** One step within a scenario, which can be an API, software, or data transformation module.
    - **Connections:** Links established with different software applications.
    - **Webhooks and Triggers:** The only two ways to activate or trigger an automation or workflow.
        - **Pulling Triggers:** Check for updates at defined time intervals (e.g., every 15 minutes).
        - **Instant Triggers (Webhooks):** Instantly trigger a workflow as soon as something happens in another software. They are more efficient as they only run when a specific action occurs.
    - **Operations:** Represent one run of one module. Users are charged based on the number of operations.
    - **Bundles:** Make.com's term for a JSON or object that stores structured data. When a module outputs multiple bundles, the subsequent module will process each bundle separately.
    - **Collections:** Make.com's term for an array of objects (a list of JSONs).
- **Data Types and Structures (Crucial for Debugging and Understanding):**
    
    - **Strings:** Text values, identified by double quotation marks in raw data (e.g., "new age digital").
    - **Numbers:** Numerical values, appear without quotation marks in raw data (e.g., 5).
    - **Dates:** Specific date formats required by some APIs or modules. Make.com provides an easy interface to input dates.
    - **Booleans:** True or false conditions, presented as checkboxes in make.com (e.g., `true` or `false` in raw data, without quotation marks).
    - **Binary Data:** Used for files or audio (e.g., passing a document to Google Drive).
    - **Array (List):** A list of values (e.g., a list of emails). Identified by **square brackets** `[]` in raw data, with values separated by commas. Lists store multiple values.
    - **JSON (Object/Bundle):** A structured way to store and transfer data, highly common in modern APIs. Represents multiple data points for one entity (e.g., email, name, company for a person). Identified by **curly brackets** `{}` in raw data, with key-value pairs separated by commas.
    - **Array of Objects (Collection):** A list of JSONs (e.g., multiple persons with multiple data points). Combines square and curly brackets, indicating multiple structured objects within a list.
    - **Nested Objects:** Structured data inside of structured data (e.g., a company JSON within a person JSON).
- **Essential Modules and Skills:**
    
    - **Native APIs/Connections:** Make.com has pre-set connections with thousands of third-party software, offering common actions.
    - **HTTP Requests (Custom APIs):** Used when a software lacks native integration, an action isn't listed, or for scraping.
        - **API Concepts:** Endpoints (specific addresses/URLs for actions), HTTP methods (GET, POST, PUT/PATCH, DELETE), Headers (authorisation, content type), and Request Body (data sent to API).
        - **Example (YouTube transcript scraping):** Using RapidAPI to get video transcripts via HTTP GET request.
    - **Scraping:** Extremely important for gathering data from external sources.
        - **Simple Page Scraping:** HTTP GET requests (most straightforward, but may fail with anti-scraping or JavaScript rendering), or third-party scrapers like Apify, RapidAPI, and Firecrawl.
        - **Sitemap Scraping:** Retrieves all URLs from a domain, useful for finding specific pages like a 'team' or 'blog' page.
        - **Web Crawling:** Scrapes all content from all pages of a website (e.g., for building an AI assistant trained on documentation).
        - **Social Media Scraping & Google Scraping:** Often done via specialized APIs (e.g., Apify for LinkedIn, Serper API for Google search results) due to anti-scraping measures.
        - **Complex Page Scraping:** For websites with heavy anti-scraping protection (e.g., e-commerce), services like Ninjascraper or ScraperAPI (Scrape.ly/Scraperfly) are used to bypass defenses.
    - **Iterators and Aggregators:**
        - **Iterators:** Process multiple items within a list/array separately by converting one bundle with an array into multiple bundles.
        - **Aggregators:** Combine multiple bundles into a single bundle (e.g., Array Aggregator, Text Aggregator).
    - **Built-in Tools:**
        - **Set Variable:** Create new variables or transform data using functions.
        - **Sleep Module:** Introduces a delay in the workflow, useful when waiting for API responses or to simulate non-automated processes.
    - **Error Handlers:** Crucial for production workflows to prevent data loss and ensure reliability.
        - **Break Module:** Retries an API call after a delay if an error occurs, resolving most transient issues.
        - **Ignore Module:** Ignores errors, useful if an API returns an error but the process was successful, to prevent deactivation.
        - **Allow storing of incomplete executions:** A setting that enables make.com to store data from failed executions, preventing data loss.
- **AI Integration:**
    
    - AI makes automations 10 times more powerful, allowing complex systems and workflows to be automated.
    - **make.com AI Tools:** Built-in AI modules for common use cases like sentiment analysis, text categorisation, language identification, summarisation, and translation. These are pre-prompted and don't require external AI connections.
    - **Types of LLMs:**
        - **Non-reasoning LLMs:** Faster, cheaper, better for simpler tasks (e.g., GPT-4o, Claude 3.5, Gemini Flash).
        - **Reasoning LLMs:** Slower, more expensive, better for complex tasks requiring planning and reasoning (e.g., GPT-4, Gemini 2.0).
    - **LLM Use Cases:** Extracting data, generation (content creation), classification/categorisation, evaluation (sentiment analysis), data transformation (code generation, JSON output), and decision-making (in AI agents).
    - **Prompting Frameworks:** Essential for reliable, consistent output in automation systems, unlike conversational prompting in tools like ChatGPT.
        - **Short Structured Prompting Framework (for non-reasoning LLMs, simpler tasks):** Includes Role & Objective, Instructions/Rules (with output formats and error handling), Examples (input/output pairs), and Variables. Markdown formatting (e.g., H1 headers) can be used to structure prompts.
        - **Long Structured Prompting Framework (for non-reasoning LLMs, complex tasks):** More detailed, includes Role, Objective, Context, Instructions, Examples, Variables, and Notes (for important rules).
        - **Prompting Reasoning LLMs:** Requires less guidance, more direct prompts work best (Objective, Instructions, Context/Variables).
    - **Choosing LLMs & Frameworks:** General guidelines suggest non-reasoning models with short frameworks for extraction, classification, and simple data transformation. Reasoning models or non-reasoning models with long frameworks are recommended for evaluation, generation, and decision-making.
    - **Prompt Chaining:** Breaking down complex tasks into multiple, smaller AI steps, where the output of one module feeds into the next. This significantly increases consistency and reliability.
- **Advanced Skills and Techniques:**
    
    - **Functions:** Built-in ways to work with/transform data, common for filtering, cleaning up, and working with conditions.
        - Categories: General, Math, Text & Binary, Date & Time, Array.
        - Examples: `length()` (checks string length), `trim()` (removes spaces), `substring()` (limits characters), `split()` (creates arrays from strings), `contains()` (checks for specific words), `get()` (gets value from array), `if()` (conditional output), `now()` (current date), `addDays()` (adds days to date), `join()` (converts array to string), `map()` (picks specific values from an array), `flatten()` (simplifies nested arrays). Functions do not cost operations.
    - **Text Parsers (Match Pattern/Regex):** Helps match specific patterns in text for extraction, identification, replacement, or cleanup.
        - Can extract data like emails, numbers, dates, or specific formats.
        - More efficient than AI for consistent data extraction, as they don't use AI tokens.
        - AI (e.g., ChatGPT) can be used to generate the necessary regular expressions.

The document concludes by stating that mastering these concepts enables users to build almost any automation on make.com.