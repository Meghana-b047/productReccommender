# productReccommender

 🛍️ Product Recommendation App

An AI-powered **product recommendation system** that uses an LLM and real-time web search to find, evaluate, rank, and recommend products based on a user's requirements, budget, quantity, and use case.

## 🚀 Overview

The application acts as an intelligent shopping assistant. Users provide:

* Product description
* Product category
* Total budget
* Required quantity

The system searches the web for relevant products, evaluates the results using an LLM, applies strict budget constraints, and returns the **top 5 product recommendations** with pricing, ratings, platforms, links, and reasons for recommendation.

## 🧠 How It Works

The application follows a multi-step AI recommendation pipeline:

1. **User Input**

   * Accepts product description, category, budget, and quantity through a FastAPI endpoint.

2. **Query Generation**

   * The LLM analyzes the user's request and expands vague descriptions into more specific search requirements.
   * Example: `"Good phone for photography"` can be expanded into requirements such as high-resolution cameras, OIS, night mode, and good camera sensors.

3. **Real-Time Web Search**

   * Uses the **Serper API** to retrieve current product information and search results from the web.

4. **Product Evaluation**

   * The LLM evaluates retrieved products based on:

     * Budget
     * Use case
     * Durability
     * Reviews
     * Product relevance

5. **Budget Enforcement**

   * Calculates the maximum allowed price per item:

   `Per-item budget = Total budget / Quantity`

   * Products exceeding the calculated per-item budget are rejected.

6. **Ranking & Recommendation**

   * Relevant products are ranked and the top 5 are returned.

7. **Structured Output**

   * Recommendations are returned in JSON format containing product name, category, price, platform, rating, product link, and recommendation reason.

## ✨ Features

* 🤖 LLM-powered product recommendations
* 🔎 Real-time web search using Serper API
* 💰 Strict per-item budget enforcement
* 📊 Product ranking and comparison
* 🎯 Use-case based recommendations
* ⭐ Rating and review-based evaluation
* 🔗 Exact product page links
* 📦 Quantity-aware budget calculation
* ⚡ REST API built with FastAPI
* 🔐 API credentials managed using environment variables
* 🧾 Structured JSON responses

## 🏗️ Architecture

```text
User Request
     │
     ▼
 FastAPI API
     │
     ▼
 SearchAgent
     │
     ├──► Groq LLM
     │       │
     │       └── Generate optimized search query
     │
     ▼
 Serper Web Search
     │
     ▼
 Search Results
     │
     ▼
 Groq LLM
     │
     ├── Budget filtering
     ├── Relevance evaluation
     ├── Product ranking
     └── Top 5 selection
     │
     ▼
 JSON Recommendations
```

## 🛠️ Tech Stack

* **Python**
* **FastAPI** — REST API framework
* **Groq API** — LLM inference
* **Llama 3.3 70B** — recommendation and ranking model
* **Serper API** — real-time Google search
* **Pydantic** — request validation
* **Requests** — API communication
* **python-dotenv** — environment variable management

## 📂 Project Structure

```text
product-recommendation/
│
├── server.py          # FastAPI application and API endpoints
├── agent.py           # Search agent, LLM integration and web search
├── .env               # API credentials
├── requirements.txt   # Python dependencies
└── README.md
```

## 📦 Installation

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd product-recommendation
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure API keys

Create a `.env` file:

```env
GROQ_API_KEY=your_groq_api_key
SERPER_API_KEY=your_serper_api_key
```

### 4. Start the server

```bash
python server.py
```

Or using Uvicorn:

```bash
uvicorn server:app --reload
```

The API will be available at:

```text
http://localhost:8000
```

FastAPI's interactive API documentation can be accessed at:

```text
http://localhost:8000/docs
```

## 🔌 API Usage

### `GET /`

Returns a welcome message.

### `POST /recommend`

Generates product recommendations.

#### Request

```json
{
    "Product_Description": "Best phone for photography",
    "category": "Electronics",
    "budget": 40000,
    "quantity": 1
}
```

#### Response

```json
{
    "product_name": "Example Phone",
    "category": "Electronics",
    "price": "₹39,999",
    "platform": "Example Platform",
    "rating": "9.2",
    "product link": "https://example.com/product",
    "reason": "Excellent camera performance within the specified budget."
}
```

## 📋 Supported Categories

* Fashion
* Electronics
* Food
* Apps
* Games
* Books
* Beauty
* Cosmetics

## 💡 Example

### Input

```text
Product Description: Good wireless headphones for studying
Category: Electronics
Budget: ₹10,000
Quantity: 2
```

The system calculates:

```text
Per-item budget = ₹10,000 / 2
                = ₹5,000
```

Only products priced at **₹5,000 or below** are eligible for recommendation.

The LLM then ranks eligible products based on relevance, durability, reviews, and intended use.

## 🔮 Future Improvements

* Add a frontend using React or Streamlit
* Support multiple search providers
* Add price comparison across e-commerce platforms
* Add product image extraction
* Implement product caching
* Add user preference history
* Improve structured output validation
* Add asynchronous API calls for faster responses
* Introduce evaluation metrics for recommendation quality

## 👩‍💻 Author

**Meghana**

Built as an AI-powered recommendation system demonstrating LLM integration, web search, API development, and constraint-based product ranking.
