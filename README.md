# AI-business-assistant
An AI Business Assistant helps translate business questions into insightful answers. Rather than writing SQL queries or analyzing data manually, the user can ask the question in natural language. The AI-driven assistant translates the query into a SQL query, analyzes the answer, visualizes the data and explains the insight.

Business Question – Why is the 10 minute delivery promise being missed, and where should operations act first?

Dataset Overview -
- 10,000 order records
- 10,000 delivery records
- 1,000 return records
- 51 product records
- 5,100 inventory records
- 100 stores across 7 cities
- Data period: 21 January – 21 February 2025

Approach - Project Workflow -    
1) Data Loading & Cleaning (Scripts 01-05): Loaded CSV files into SQLite, standardized column names, transformed timestamps into datetime data type, and converted delivery time field from mm:ss to seconds.
2) Context of Schema & API Integration (Scripts 06-07): Described the structure of database tables, columns, relationships, and data properties to give context to the LLM regarding the database schema. Tested connectivity with Gemini API.
3) Natural Language to SQL (Script 08): Integrated Google Gemini to transform natural language business questions into SQL queries with SELECT validation only, restricted dangerous actions, and provided read-only database access.
4) Query Analysis & Insights (Scripts 09–10): Executed generated SQL queries, summarized results through statistics and data samples, and generated business-oriented explanations based on the results.
5) Automatic Visualizations (Script 11): Developed automatic visualization generation to identify suitable dimensions and metrics in the query results and  create relevant visualizations.
6) Streamlit Application (Script 12): Built an interactive application that included natural language questions, generated SQL queries, query results, visualizations, AI-based insights, and raw data previews.

Key Insights - 
1) Delivery: Only 20.1% orders fulfilled the delivery promise of 10 mins. Average time taken for delivery was 16.41 minutes which means that there was a deviation of 6.41 minutes and 79.9% orders were late in delivery.
2) Consistent Across Delivery Partner: Rates of delivery being late across all 10 delivery partners vary from only 78.46% to 82.85% and average delivery times ranging from 16.17 to 16.87 minutes. 
3) Consistent Across Stores: Late delivery rates across all 100 stores vary from 66.95% to 88.42% and average delivery times varied from 14.97 minutes to 17.55 minutes. All stores were falling short of the promise in most orders.
4) Returns and Refund: 10% of the orders were returned with refunding of Rs 4.79 lakh (9.6% of revenue). The most common reason for returns was stale product.

Business Recommendations –
1) Late deliveries to be treated as a process issue for the whole company - Almost 80% orders are late. Late rates are fairly even among all 100 stores (67%-88%) and all 10 delivery partners (78%-83%). Looking at dispatch and rider assignment as a whole, not at individual stores or riders.
2) Collect more detailed delivery data - At the moment there is only information on the placement and delivery times, but not on how much time is spent in-between (assigned, picked up, waiting). Tracking each of the stages is necessary for identification of the root cause.
3) Reduce returns of the stale product - Approximately 10% orders are returns (₹4.79 lakh, 9.6% of revenue). Most frequent reason for the returns is the stale product. Inspect freshness and expiration dates before dispatch.
4) Monitor a weekly numbers - Track on-time rate, average delivery time, return rate and refund amount.

AI Assistant - AI Assistant - Users can formulate queries in natural language English to ask business questions like “What stores have the most items at or below their reorder levels? " or "What is the rate of returns, total refund amounts and the most frequent reason of returns?" The AI formulates SQL queries with Google Gemini, checks and runs them, creates visuals, and writes down business insights. Utilizing database schema context, SELECT-only query validation, read-only access and summarization of the queries' results allows maintaining security of the process and sticking to the data.

Tech Stack –
Programming: Python
Database: SQLite
Data Processing: Pandas
LLM: Google Gemini API
Visualisation: Plotly
Dashboard: Streamlit

Usage -
pip install -r requirements.txt
# Mac / Linux
export GOOGLE_API_KEY="your-api-key"
# Windows (PowerShell)
$env:GOOGLE_API_KEY="your-api-key"
streamlit run 12.app.py
