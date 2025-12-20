# AI-Powered Product Recommendation API  
Semantic search, ranking, and reordering over 40,000+ SKUs

Backend service that powers **AI-driven product recommendations** for promotional products.  
Built for scale and low latency using **Pinecone**, **OpenAI embeddings**, and **Cloudflare Workers**.

This API replaces manual product curation and rule-heavy filters with **intent-aware ranking** that understands what the buyer is actually trying to do.

---

## What this solves

Traditional product search breaks down at scale:
- Keyword matching fails on vague intent (“welcome kit”, “client gifts”, “eco swag”)
- Manual filters don’t capture context (event, industry, budget, urgency)
- Sales teams waste time curating product lists by hand

This service:
- Understands **natural-language intent**
- Searches across **40K+ SKUs**
- **Reorders results intelligently**, not just filters them
- Works in real time at storefront speed

---

## Architecture

- **Cloudflare Workers**
  - Edge-deployed API (low latency globally)
  - Handles request orchestration and response shaping

- **OpenAI API**
  - Generates embeddings for user intent and queries
  - Optional LLM reasoning for re-ranking and explanation

- **Pinecone**
  - Vector index of 40,000+ products
  - Fast semantic similarity search
  - Metadata filtering (price, brand, category, supplier, etc.)

---

## Core concept

Instead of:
> “Filter by category → price → brand → sort”

We do:
> “Understand intent → retrieve candidates → re-rank intelligently”

---

## Main endpoint

### `POST /v1/recommend`

Returns a **ranked list of products** based on intent, constraints, and context.

### Example request

```json
{
  "intent": "Eco-friendly welcome kits for new hires",
  "limit": 12,

  "constraints": {
    "min_qty": 50,
    "max_price_per_item": 15,
    "eco": true,
    "rush": false
  },

  "context": {
    "industry": "SaaS",
    "event": "New employee onboarding",
    "brand_tone": "Modern",
    "ship_by": "2025-03-20"
  }
}
