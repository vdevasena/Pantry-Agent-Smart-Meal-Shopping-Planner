# PantryPilot: Multi-Agent Meal Planning, Pantry Intelligence & Smart Grocery Assistant

> **PantryPilot** is a multi-agent system that turns a single natural-language request into:
> - A 5-day healthy meal plan (breakfast, lunch, snack, dinner)  
> - An estimated pantry inventory (what you likely have vs what you need)  
> - A categorized shopping list  
> - Weather-aware shopping advice (walk vs delivery)  
> - 2–3 nearby stores that likely carry your ingredients  


## 1. Problem & Motivation

Weekly meal planning is deceptively hard. A single "What should I eat this week?" question hides many sub-problems:

- *What ingredients do I already have in my pantry?*  
- *What healthy meals can I cook using those ingredients?*  
- *What exactly do I need to buy, and where should I buy it?*  
- *Is the weather good enough to walk, or should I get delivery?*  
- *How do I make this efficient and not spend hours planning?*

For students, busy professionals, or anyone without a car, this becomes stressful and often leads to:

- Food waste  
- Unnecessary grocery runs  
- Poor nutritional choices  
- Decision fatigue  

## 2. Solution Overview

**PantryPilot** is an **Multi-agent system** that automates the entire cooking workflow from your message:

> _"I need to buy milk, eggs, rice, tomatoes, ginger, and chicken from my apartment in Jersey City. I don't have a car and want everything in 2 days."

PantryPilot responds with:

- A **5-day healthy meal plan** (Mon–Fri, with breakfast, lunch, snack, dinner)  
- A **pantry estimate** (staples you likely already have vs perishables you must buy)  
- A **shopping list**, grouped by category (Produce, Protein, Dairy, Pantry)  
- A **weather-aware recommendation** (walk vs delivery)  
- **2–3 nearby grocery stores** that likely carry those ingredients  
- Practical tips (batch-boiling eggs, storing ginger, scheduling shopping, etc.)

## 3. Architecture

```mermaid
flowchart TD

    U[User Message] --> SG[ShoppingGoalAgent<br/>shopping_info]

    SG --> PW[ParallelAgent<br/>Inventory + Weather]

    PW --> INV[InventoryAgent<br/>inventory]
    PW --> WEA[WeatherAgent<br/>weather]

    INV --> REC[RecipeAgent<br/>recipes]
    WEA --> REC

    REC --> MP[MealPlanAgent<br/>meal_plan]

    MP --> SL[ShoppingListAgent<br/>shopping_list]

    SL --> ST[StoreLocatorAgent<br/>stores]

    ST --> SUM[SummaryAgent<br/>final_plan]

    SUM --> OUT[Final Summary]
