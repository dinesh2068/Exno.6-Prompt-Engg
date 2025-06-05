# Exno.6-Prompt-Engg
# Date:
# Register no: 212223220021
# Aim: Development of Python Code Compatible with Multiple AI Tools

# Algorithm: Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights.

1. Import required libraries: google.generativeai and requests
2. Define API keys for Gemini and Hugging Face.
3. Create a function query_gemini() to interact with Google Gemini model.
4. Create a function query_huggingface() to interact with Hugging Face's Falcon model.
5. Create a function compare_outputs() to compare response lengths from both APIs.
6. In main(), take user input as the prompt.
7. Fetch responses from both APIs.
8. Print both responses and display a comparison insight.
9. Execute the main() function.

# Program:
```
import google.generativeai as genai
import requests

# Replace with your actual API keys
genai.configure(api_key="your_gemini_api_key")
huggingface_api_key = "your_huggingface_api_key"

def query_gemini(prompt):
    model = genai.GenerativeModel("gemini-pro")
    response = model.generate_content(prompt)
    return response.text.strip()

def query_huggingface(prompt):
    url = "https://api-inference.huggingface.co/models/tiiuae/falcon-7b-instruct"
    headers = {
        "Authorization": f"Bearer {huggingface_api_key}"
    }
    payload = {
        "inputs": prompt,
        "options": {"wait_for_model": True}
    }
    response = requests.post(url, headers=headers, json=payload)
    result = response.json()
    return result[0]["generated_text"].strip()

def compare_outputs(output1, output2):
    len1 = len(output1)
    len2 = len(output2)
    if len1 > len2:
        return "Gemini gave a longer response."
    elif len2 > len1:
        return "Hugging Face gave a longer response."
    else:
        return "Both gave responses of the same length."

def main():
    prompt = input("Enter your question for the AI tools: ")
    print("\nQuerying Gemini (Google)...")
    gemini_response = query_gemini(prompt)
    print("\nQuerying Hugging Face...")
    hf_response = query_huggingface(prompt)
    print("\n--- AI Tool Outputs ---")
    print("\nGemini Response:\n", gemini_response)
    print("\nHugging Face Response:\n", hf_response)
    print("\n--- Comparison ---")
    result = compare_outputs(gemini_response, hf_response)
    print("Insight:", result)

if __name__ == "__main__":
    main()

```

# OUTPUT:

```

Enter your question for the AI tools: Explain the importance of AI in healthcare.

Querying Gemini (Google)...

Querying Hugging Face...

--- AI Tool Outputs ---

Gemini Response:
Artificial Intelligence (AI) is revolutionizing healthcare by improving diagnostics, treatment planning, and patient care. AI algorithms can analyze vast amounts of medical data to identify patterns and assist doctors in making more accurate diagnoses. It enhances efficiency in hospitals, helps predict disease outbreaks, and enables personalized medicine. Additionally, AI-powered tools support medical imaging, drug discovery, and virtual health assistants, ultimately leading to better outcomes and reduced costs.

Hugging Face Response:
AI is important in healthcare because it can process large amounts of data quickly. It helps in diagnosing diseases, monitoring patients, and improving overall healthcare services. AI tools assist doctors and researchers in making decisions and discovering new treatments more efficiently.

--- Comparison ---
Insight: Gemini gave a longer response.


```
# Result: The corresponding Prompt is executed successfully
