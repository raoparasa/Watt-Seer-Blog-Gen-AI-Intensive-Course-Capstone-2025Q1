---
title: "Is Your Energy Bill Normal? AI Finds Your Household's Energy Twins" 
description: "Stop comparing apples to oranges. Watt-Seer-Compare uses AI embeddings and LLM analysis on home data to benchmark your energy use against similar homes."
author: Harshitha Srinivas
layout: default
---

# 💡 Watt-Seer-Compare

You stare at your energy bill. The numbers fluctuate month to month, but one question always lingers: **"*Is this normal*?"**  
You check the usage – hundreds, maybe thousands of kilowatt-hours (kWh). But what does that really mean? Compared to whom? Is your home an energy guzzler, a model of efficiency, or just... average?

It's a question millions ask, often met with frustratingly little context. Raw smart meter data is overwhelming, and simple monthly totals hide the real story. 

What if you could see how your home truly stacks up against others just like it? Maybe you live in a neighborhood with similar houses, but you don't know your neighbors' habits. Maybe the weather was weird last month. How does your specific energy usage pattern – driven by your appliances, your schedule, and your household size – compare to others like you?

That's the quest behind Watt-Seer-Compare. We're moving beyond simple averages to provide personalized, AI-powered energy benchmarking. Using detailed smart home data and the nuanced understanding of Google Gemini, this project finds your household's **"Energy Twins"** and tells you why your usage patterns are similar or different.

## 👥 Team Members

- Harshitha Srinivas [Kaggle Profile](https://www.kaggle.com/harshithasrini)
- Praveen G [Kaggle Profile](https://www.kaggle.com/praveengv)
- Naga Vishnu Kanth Irukulapati [Kaggle Profile](https://www.kaggle.com/nagavishnukanthi)

---

## 🔍 The Problem: Drowning in Data, Starving for Context

Smart meters promise granular insights, tracking energy use down to the hour or minute. We get data points enriched with details:   

- 🔌 Appliance Type: Fridge, Heater, AC, Oven...
- ⚡ Energy Consumption (kWh): The precise usage.
- 📅 Date + Time: When energy was used.
- 🌡️ Outdoor Temperature: A key driver for heating/cooling.   
- ☀️ Season: Context for usage patterns.
- 👨‍👩‍👧‍👦 Household Size: A major factor in demand.   

But, rows upon rows of this data often lead to more confusion than clarity. How do you know if your AC usage on a hot August day was typical for a family of four in your climate zone? 

Traditional comparisons often rely on crude filters (e.g., same month), missing the subtle interplay of factors that define a household's energy signature.

<p align=center>
<img src="https://github.com/user-attachments/assets/a76dde97-9931-4739-83cb-0b6fdb9cf19e" />
</p>

---

## 🤖 Solution: Finding Your "Energy Twins" with AI

**Watt-Seer-Compare** tackles this challenge head-on. It doesn't just filter data; it understands it. Here’s how:

<img width="830" alt="Screenshot 2025-04-19 at 3 23 27 PM" src="https://github.com/user-attachments/assets/f64f7356-7ced-4606-bbdf-52afc2226d4e" />
 
**1. *Smart Summaries:*** We first distill the flood of raw data into concise, informative monthly summaries for each home, capturing total usage, temperature context, seasonality, household size, and key appliance contributions.

**2. *Semantic Understanding (Gemini Embeddings):*** This is where the magic happens. We use Google Gemini's text-embedding-004 model to convert these textual summaries into rich numerical representations (embeddings). These aren't just numbers; they capture the semantic meaning and context of each household's monthly energy story.

**3. *Finding Your Peers (Cosine Similarity):*** With embeddings, we can mathematically compare how "alike" different households are based on their entire energy profile for the month using cosine similarity. This allows us to find the homes that are most similar to yours – your **"Energy Twins"**

**4. *Visual Comparisons and AI Explanation (Gemini LLM):*** We generate clear, intuitive plots. Here numbers and plots are great, but why are you similar or different? We feed your summary and your Twins' summaries into Gemini (gemini-2.0-flash), prompting it to analyze the nuances and generate a plain-English explanation comparing your profile to your closest peers.

<p align=center>
<img width="450" alt="Screenshot 2025-04-20 at 8 05 35 AM" src="https://github.com/user-attachments/assets/81f79215-3d44-4f71-84f4-83fca4916b91" />
</p>

---

## 📊 Example Output: 
### Gain Unprecedented Clarity With Visual Insights!

Let's follow Home 34's journey in June 2023. After inputting the ID and month, Watt-Seer-Compare gets to work and presents...

1. First, let's look at target home's individual profile and Total usage vs. the average of its Energy Twins:

<table>
  <tr>
    <td align="center" valign="top"> <img src="https://github.com/user-attachments/assets/dbecd19d-6dba-48ba-9877-14a7dfded733" alt="Pie Chart"><br><em>Caption: Target Appliance Breakdown</em> </td>
    <td align="center" valign="top"> <img src="https://github.com/user-attachments/assets/f41fb619-612f-4759-8162-c28f2db4f336" alt="Avg Comparison"><br><em>Caption: Target vs Avg Similar</em> </td>
  </tr>
 </table>

 2. Comparison Context: 

 <table>
  <tr>
    <td align="center" valign="top"> <img src="https://github.com/user-attachments/assets/0c53651f-48f4-49f8-94e3-b41bd538e103" alt="Individual Comparison"><br><em>Caption: Target vs Individual Similar</em> </td>
    <td align="center" valign="top"> <img src="https://github.com/user-attachments/assets/32455602-2fd0-4e95-b224-d61a8320cd38" alt="Appliance Comparison"><br><em>Caption: Top Appliance Comparison</em> </td>
  </tr>
</table>


3. The AI Analyst's Take:

*LLM Comparison Summary:*

Home 34's energy consumption profile for June 2023 is highly similar to several other homes, primarily due to similar household sizes, seasonal context, and reliance on both heating and air conditioning. These homes exhibit total energy consumption within a relatively narrow range of 30 to 37 kWh. While the overall patterns are alike, variations in average temperature lead to differences in the specific usage of heating and cooling appliances. Furthermore, lifestyle differences are reflected in the varying consumption of appliances like lights, washing machines, and ovens, contributing to subtle distinctions between the homes despite their high similarity scores. The lower similarity homes have different household sizes, some being smaller and one being larger, and also have a wider range of temperatures and total consumption, contributing to their lower similarity scores.

Suddenly, your energy usage isn't just a number; it's a narrative placed within the context of genuinely comparable households.

---

## 🧪 Code Highlight: Generating the Embeddings

The core of finding "Energy Twins" lies in creating meaningful embeddings from the monthly summaries. Here's a snippet of how we prepare the data and call the embedding model (using helper functions defined in the notebook):

**1. Generating Monthly Text Summaries:**

```python
# (Inside create_monthly_summaries function)
summary_text = (
    f"Home ID {home_id} for Month {period}:\n"
    f"- Total Consumption: {total_kwh:.1f} kWh\n"
    f"- Household Size: {household_size}\n"
    f"- Average Temperature: {avg_temp}°C\n"
    f"- Season: {season}\n"
    f"- Appliance Breakdown: {appliance_summary}"
)
summary_records.append({..., "Summary Text": summary_text})
```
**2. Finding Similar Homes via Embeddings:**

```python
# (Inside run_energy_comparison_analysis)
# Get embeddings for the month
embeddings, summaries = generate_embeddings_efficiently(...)

# Calculate similarity
top_similar, bottom_similar = get_embedding_similarities(
    target_home_id=target_home_id,
    all_embeddings=embeddings,
    k=k_similar
)
```
**3. Prompting the LLM for Explanation:**

```python
# (Inside generate_llm_comparison)
prompt = f"""
**Context:** You are an expert energy analyst...
**Input Data:**
* **Target Home (ID: {target_home_id}) Summary:**\n    ```{target_summary}```
* **Most Similar Homes (Top {homes_added}):**\n{similar_homes_text}
**Task:** Analyze the provided summaries. **Think step-by-step**...
**Output:** Provide the final synthesized comparison summary...
"""
response = client.models.generate_content(model=model_name, contents=prompt, ...)
```
---

## ✨ Why This Matters: Beyond Simple Filters
### This approach offers significant advantages:

- **Deep Contextual Similarity:** Embeddings capture complex relationships between factors (temperature, appliance use, household size) that simple filters miss. An "Energy Twin" found this way shares a more holistic usage pattern.   

- **Semantic Understanding:** The LLM doesn't just state facts; it synthesizes information from multiple summaries, not just isolated numbers to explain why similarities or differences exist, providing actionable context.

- **Data-Driven Discovery:** You might find your home is similar to others for unexpected reasons, uncovering potential inefficiencies or validating your energy-saving efforts.

---

## 🔮 Limitations & Future Directions..

Watt-Seer-Compare provides powerful context, but like any analysis, it has boundaries:

- **Data Dependency:** Accuracy hinges on detailed, reliable smart meter data.

- **Dataset Scope:** Comparisons are limited to the homes within the dataset.

- **Dataset Realism:** The current dataset demonstrates the AI methodology but may not perfectly capture the full complexity and real-time variations of actual household energy consumption. 

- **Model Evolution:** AI models change; prompts and interpretations may need adjustments over time.

What's Next?
- Integrating real-time data streams. Adjusting for temperature variations for even fairer comparisons.

- Adding energy cost analysis and prediction.

- Incorporating user feedback to refine similarity.

- Generating personalized energy-saving recommendations based on comparison insights.

- Expanding to use multimodal inputs (like scanned bills, similar to the original Watt-Seer concept).

---

## 🤝 From Numbers to Narratives: 
### Understand Your Energy Story

Stop wondering in the dark. By finding your "Energy Twins", combining detailed data, semantic AI, visualizations, and natural language explanations, Watt-Seer-Compare demonstrates how AI can transform rows of energy data into a meaningful conversation about consumption patterns and empowers you to understand your unique energy story.

Ready to see how you stack up and meet your Energy Twins?

---

## 🚀 Dive Deeper: Explore the Code & Watch the Demo!

Explore the code, run it with the sample data, and imagine plugging in your own smart meter readings. Discover your own "Energy Twins" and gain clarity on your consumption.

![image](https://github.com/user-attachments/assets/84b8affa-0da9-4d92-a8c2-e206eac92064)

### 🔗 Click on the links below to try Watt-Seer-Compare Yourself!

**👉 [View the Watt-Seer-Compare Kaggle Notebook](https://www.kaggle.com/code/praveengv/capstone-watt-seer-compare)**

**📺 [Watch our video walkthrough for a quick overview!](https://youtu.be/FThWDAUClWs)**

Your energy data holds insights waiting to be revealed. Let AI help you listen.

---

## 📚 Sources and Related Content

**Dataset:** [Smart Home Energy Consumption Dataset on Kaggle](https://www.kaggle.com/datasets/mexwell/smart-home-energy-consumption)

**Concepts:**
- Embeddings, Vector Search and Cosine Similarity Explained - [Check out](https://www.kaggle.com/code/markishere/day-2-embeddings-and-similarity-scores)
- Long Context Understanding - [Check out](https://www.kaggle.com/code/markishere/day-1-evaluation-and-structured-output)
- Prompting - [Check out](https://www.kaggle.com/code/markishere/day-2-embeddings-and-similarity-scores)
- Retrieval Augmented Generation(RAG) - [Check out](https://www.kaggle.com/code/markishere/day-2-document-q-a-with-rag)

---

Questions/Feedback? Post your questions via [Kaggle Comments](https://www.kaggle.com/code/praveengv/capstone-watt-seer-compare/comments) or open an issue on our <a href="https://github.com/suresh-srinivas/Watt-Seer-Blog-Gen-AI-Intensive-Course-Capstone-2025Q1/issues" style="display: inline-flex; align-items: center; text-decoration: none;"><img src="https://github.githubassets.com/assets/GitHub-Mark-ea2971cee799.png" alt="GitHub" width="16" height="16" style="vertical-align: middle; margin-right: 4px;"/>GitHub Issues</a>
