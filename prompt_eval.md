# Prompt Evaluation: College Canteen Plan

## Overall Score

| Parameter | Score |
|---|---:|
| Prompt Clarity | 86 / 100 |
| Output Quality | 56 / 100 |
| Efficiency | 36 / 50 |
| **Total** | **178 / 250** |

## Executive Summary

The prompt gives the model a concrete role, a bounded one-week task, affordability and vegetarian requirements, and a clear five-part response structure. Those elements should elicit a relevant plan. Its main risk is financial ambiguity: it does not define how many students are served, which expenses count against the ₹10,000, or whether profit is calculated from purchased stock or stock actually consumed. As a result, different answers can appear internally consistent while using incompatible assumptions. There are no examples or explicit rules for grounding local prices and presenting uncertainty.

## Evaluated Prompt Analysis

**Target:** `Quick_prompt.md`  
**Length:** 360 whitespace-separated words, approximately 470–520 tokens (rough estimate; exact count depends on tokenizer).  
**Structure:** Role, context, numbered task list, constraints, output headings, and an instruction to state assumptions. The prompt is a single fixed scenario rather than a reusable template with separately defined inputs.

### Prompt Text Evaluated

> **Role:**  
> Act as an experienced college-canteen management and food-service specialist with expertise in menu planning, pricing, inventory management, and demand forecasting.
>
> **Context:**  
> I have a budget of exactly **₹10,000** to improve a college canteen for **one week**. The goal is to create an affordable and attractive menu while using the limited budget efficiently and minimizing food wastage.
>
> **Task:**  
> Design a complete one-week canteen plan. Decide:
>
> 1. **Menu:** What food and beverages should be offered each day?
> 2. **Pricing:** What should be the selling price of each item?
> 3. **Quantities:** How many units of each item should be prepared or stocked?
> 4. **Budget:** How should the ₹10,000 budget be allocated across ingredients, food items, beverages, and other necessary costs?
> 5. **Demand management:** How should the canteen handle high demand, shortages, peak hours, and unsold food?
> 6. **Profit/Sustainability:** Aim to make the canteen financially sustainable while keeping prices affordable for college students.
>
> **Constraints:**  
> - Total budget: **₹10,000**
> - Duration: **7 days**
> - Prices should be realistic for a college canteen in India.
> - Prioritize affordable, popular, and easy-to-prepare items.
> - Avoid unnecessarily complicated or expensive dishes.
> - Include vegetarian options.
> - Account for different levels of demand on weekdays and weekends, if relevant.
> - Clearly distinguish between **estimated cost** and **selling price**.
> - Do not exceed the ₹10,000 budget.
>
> **Output format:**  
> Present the solution in the following structure:
>
> ### 1. Weekly Menu
> Create a table with:
> **Day | Item | Quantity | Cost per unit | Selling price | Expected demand | Expected revenue**
>
> ### 2. Budget Breakdown
> Show how the entire **₹10,000** is allocated.
>
> ### 3. Demand Management Strategy
> Explain how to handle:
> - Peak-hour demand
> - Unexpectedly high demand
> - Low demand
> - Food shortages
> - Unsold food and wastage
>
> ### 4. Financial Summary
> Calculate:
> - Total estimated cost
> - Total expected revenue
> - Expected profit/loss
> - Approximate profit margin
>
> ### 5. Final Recommendation
> Briefly explain why this menu and pricing strategy would work for a college canteen and what could be adjusted based on actual demand during the week.
>
> **Important:** Make reasonable assumptions where information is missing, clearly state those assumptions, and ensure that all calculations are internally consistent.

## Detailed Parameter Breakdown

### 1. Prompt Clarity: 86 / 100

| Criterion | Score | Assessment |
|---|---:|---|
| Role and persona definition | 18 / 20 | “Experienced college-canteen management and food-service specialist” gives useful domain context and names relevant expertise. The role's decision-making perspective (e.g., owner/operator versus advisor) is not specified. |
| Task specificity and negative constraints | 22 / 25 | Six concrete decisions and constraints like “Avoid unnecessarily complicated or expensive dishes” establish scope. It does not define whether existing equipment, labor, or facilities are available. |
| Instruction structure and delimiters | 18 / 20 | Headings, numbered tasks, and a prescribed output structure make the request easy to parse. No distinct input fields separate fixed scenario values from assumptions. |
| Tone and target audience | 12 / 15 | Affordability “for college students” establishes the customer, and “Briefly explain” guides part of the response. The overall tone and expected level of detail are not consistently defined. |
| Unambiguous language | 16 / 20 | The seven-day duration and ₹10,000 ceiling are explicit. “Exactly” and “entire ₹10,000 is allocated” do not clarify whether the budget must be spent, merely assigned, or include contingency and capital costs. |

**Strengths:** The fixed budget and duration are prominent. The role and desired customer outcome are concrete. The instruction to “clearly state those assumptions” usefully acknowledges missing information.

**Gaps:** “One week” is given as 7 days but whether the canteen is open every day is not stated. “Improve a college canteen” could imply setup or upgrade costs, whereas the task mostly describes a weekly operating plan. Demand, capacity, location-specific prices, and cost coverage are left open.

### 2. Output Quality: 56 / 100

| Criterion | Score | Assessment |
|---|---:|---|
| Output format and schema enforcement | 24 / 30 | Five required sections and a table header provide a strong format. The menu table does not require units/currency, forecast units sold, total rows, or formulas; the budget and financial summary could therefore fail to reconcile. |
| Few-shot examples and demonstrations | 0 / 25 | No sample menu row or example calculation demonstrates the intended granularity or arithmetic. |
| Edge cases and fallback instructions | 18 / 25 | Peak demand, shortages, low demand, unsold food, weekends, and missing information are covered. There is no rule for uncertainty, inconsistent inputs, closed days, dietary/allergen needs, or a plan that cannot meet the assumed demand within budget. |
| Factuality and hallucination prevention | 14 / 20 | The prompt asks for realistic Indian prices and internally consistent calculations, but does not require a location, price basis, date/source, or explicit labeling of estimates. The model could present invented costs and demand as facts. |

**Strengths:** It explicitly requests demand-management coverage, distinguishes “estimated cost” from “selling price,” and calls for assumptions and consistent arithmetic.

**Gaps:** “Expected revenue” is not tied to units sold, so the model might multiply price by prepared quantity even when expected demand is lower. It also does not distinguish procurement cash outlay, cost of ingredients consumed, and unsold inventory, or define profit margin. No example validates the required calculations.

### 3. Efficiency: 36 / 50

| Criterion | Score | Assessment |
|---|---:|---|
| Conciseness and fluff elimination | 12 / 15 | The prompt is compact at 360 words. Several requirements recur across the task, constraints, and output sections, especially the budget and demand-management needs. |
| Token economy and context footprint | 12 / 15 | Most content is actionable. Some repetition could be consolidated without losing emphasis. |
| Dynamic parameterization | 4 / 10 | The budget and duration are fixed values rather than clearly replaceable inputs; no fields are provided for location, operating days, or customers served. |
| Signal-to-noise ratio | 8 / 10 | The headings prioritize the main deliverables. Critical accounting definitions are not emphasized because they are absent. |

**Strengths:** Dense, scannable structure; limited narrative filler.

**Gaps:** Inputs that strongly affect feasibility are not parameterized. Repeated constraints use tokens that could instead establish calculation conventions and assumptions.

## Actionable Recommendations

1. **Define the operating scenario:** State the location or instruct the model to label local-price estimates, specify open days, and provide or assume a daily customer count and service capacity.
2. **Define the budget boundary:** List included expense categories and explicitly exclude or include labor, rent, utilities, equipment, transport, packaging, and contingency. Treat the ₹10,000 as a ceiling and show any unspent reserve instead of forcing unnecessary purchases.
3. **Make quantities and arithmetic auditable:** Require units, prepared quantity, expected units sold, per-serving cost, revenue formula, totals, and a reconciliation check. Calculate revenue from expected sales, not preparation quantity.
4. **Separate cash and operating results:** Show procurement outlay, consumed ingredient cost, other operating costs, leftover usable stock, and operating surplus separately; define the profit-margin denominator.
5. **Constrain uncertainty:** Require estimates and assumptions to be labeled, prohibit unsupported claims of current supplier prices, and provide a lower-demand or sensitivity scenario.
6. **Add a minimal demonstration:** Include one illustrative row or equation so table granularity and revenue calculations are consistent throughout.

## Optimized Prompt Rewrite (Production-Ready)

```text
<role>
You are a practical college-canteen planner in India. Build an affordable, low-waste, financially transparent one-week plan.
</role>

<inputs>
<budget>INR 10,000 maximum for the week</budget>
<location>{city/state; if unknown, say so and use clearly labeled illustrative prices}</location>
<open_days>{7 calendar days; list any closed days}</open_days>
<customers_per_day>{if unknown, state a realistic planning assumption}</customers_per_day>
<budget_includes>{ingredients, beverages, packaging, fuel, transport, labor, utilities, equipment; mark each included/excluded/unknown}</budget_includes>
<dietary_requirements>{vegetarian options required; note other known requirements}</dietary_requirements>
</inputs>

<instructions>
Create a practical menu and operating plan for each open day. Prefer affordable, popular, easy-to-prepare items; include vegetarian choices and account for lower or different weekend demand when relevant.

If an input is missing, do not silently invent it. State a reasonable assumption and label all prices and demand figures as estimates. Do not claim supplier quotes or precise local demand without supplied evidence. If the assumed customer volume is not feasible within budget, say so and show a lower-volume plan.

Keep total planned cash outlay at or below the budget. Separate purchases from costs consumed: identify opening stock purchases, expected ingredient cost of items sold, other included operating expenses, usable leftover stock, and any unspent contingency. Do not count leftover usable stock as food waste or as consumed cost.

For every menu row, use one serving as the unit and show preparation quantity, forecast units sold, estimated unit cost, selling price, and expected revenue. Forecast sales cannot exceed prepared quantity. Calculate expected revenue as forecast units sold multiplied by selling price. Make all currency values INR and show totals.

Calculate:
- Total planned cash outlay and remaining budget.
- Expected revenue.
- Expected operating surplus = revenue minus estimated cost of items sold and included operating expenses. Exclude capital purchases and any excluded costs, and name exclusions.
- Approximate operating margin = operating surplus / revenue x 100; if revenue is zero, mark not applicable.

Add a brief lower-demand check (for example, 20% fewer sales) and explain how to reduce preparation or purchasing to limit waste. Avoid false precision; round estimates sensibly. Check that table totals reconcile with the budget and financial summary before answering.
</instructions>

<output_format>
1. Assumptions and budget scope
2. Weekly menu table with columns:
   Day | Item | Prepared servings | Forecast sold | Unit cost (INR) | Selling price (INR) | Expected revenue (INR)
3. Budget table with category, planned cash outlay, and notes; include contingency and remaining budget.
4. Demand and waste plan covering peak periods, unexpected demand, shortages, low demand, safe handling of unsold food, and daily forecast updates.
5. Financial summary with the formulas and totals defined above, plus the lower-demand check.
6. Brief recommendation and key assumptions to revise using actual sales.
</output_format>

<calculation_example>
If 30 servings are prepared, 24 are forecast sold, and the selling price is INR 20, expected revenue is 24 x 20 = INR 480, not 30 x 20.
</calculation_example>
```
