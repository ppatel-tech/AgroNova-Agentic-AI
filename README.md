AgroNova: Agentic AI Layer
The Intelligent Brain Behind Smart Farming
This repository contains the core Agentic AI Workflows for AgroNova, built using n8n and Google Gemini (LLM). These agents transform raw data (images, weather, market prices, and soil reports) into actionable farming intelligence.


Agentic Architecture
The AI layer is built on an Event-Driven Architecture. Each agent is triggered via a Webhook and follows a "Think-Act-Verify" loop:
	1. Perception: Webhooks receive data (Images, JSON, or Binary files).
	2. Reasoning: Gemini LLMs analyze context (e.g., Identifying a pest or calculating market trends).
	3. Execution: Nodes perform API calls, database updates, or trigger notifications.


🛠️ Detailed Agent Breakdown
1. Crop Recommendation Agent
	• Workflow: AI_Crop_Recommendation_Agent.json
	• Function: Recommends the top 5 most profitable crops based on real-time factors.
	• Intelligence: Combines OpenWeather API data with OCR-extracted soil reports (pH, NPK levels) and historical seasonality logic.
	• Output: Crop name, justification, seed quantity required, and estimated profit per acre.
2. Pest & Weed Detection Agent
	• Workflow: pest_weed_detection_agent.json
	• Function: Performs multi-stage image analysis to identify threats and suggest cures.
	• Logic: * Identifies the specific pest/weed using Computer Vision.
		○ Ranks treatments (Organic vs. Chemical) based on severity.
		○ Suggests the top 2 pesticides for the fastest crop recovery.
3. Fertilizer & OCR Advisory
	• Workflow: fertilizer_agent.json
	• Function: Automates nutrient management.
	• Key Feature: Uses Gemini to perform OCR on soil health cards. It calculates the Total Quantity of fertilizer needed for the specific farm size to prevent over-fertilization.
4. Market Intelligence & Prediction
	• Workflows: market_prediction.json, mandy_timing.json
	• Function: Decides the best time and location for a farmer to sell.
	• Intelligence: * Analyzes 3 years of historical Mandi data from Data.gov.in.
		○ Logistics Logic: Calculates "Effective Profit" by subtracting estimated transport costs (based on distance) from the market price.
		○ Provides a 10-day price forecast with a confidence level.
5. Emergency SOS Alert System
	• Workflow: sos alert.json
	• Function: Provides a community safety net.
	• Logic: Uses a JavaScript-based Haversine Formula to calculate the distance between a distressed farmer and nearby users. If a user is within a 5 KM radius, it triggers a real-time Firebase Cloud Message (FCM) alert.
6. Weather & Spray Advisory
	• Workflows: spay advisory.json, 7_days_weather_prediction.json
	• Function: Protects chemical investments.
	• Logic: Analyzes wind speed, rain probability, and humidity to generate a "Safe Spray Window" (e.g., 08:00 AM - 11:00 AM).


Technology Stack
	• Orchestration: n8n (Self-hosted/Cloud)
	• LLMs: Google Gemini 2.5 Flash, Gemini 3.1 Flash Lite
	• External APIs: * OpenWeather API (Climate data)
		○ Data.gov.in (Mandi prices)
		○ Nominatim (OSM) (Geocoding)
		○ FCM (Push Notifications)
	• Languages: JavaScript (Node.js) for custom logic nodes.


📥 How to Use
	1. Install n8n on your local machine or server.
	2. Import the .json files from this repository into your n8n dashboard.
	3. Configure your Credentials (Google API for Gemini, OpenWeather API Key, Data.gov.in API Key).
	4. Activate the Workflows.
	5. Use the Webhook URL provided in each trigger node to integrate with your mobile or web application.


🛡️ License
Developed by Team Agrotitens for the 2026 Agentic AI Hackathon. Backend & Agent Logic Lead: Purushottam Patel

⚠️ Security Note: All sensitive API keys and credentials have been removed from the workflow JSON files for security reasons. Users should replace placeholders with their own valid API keys (Gemini, OpenWeather, etc.) to run the workflows.