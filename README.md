# LLM-shopping_agent_thesis
# Evaluating Product Attribute Sensitivity in LLM-Based Shopping Agents

Code and data for a master's thesis (MSc Data Science, GISMA University of Applied Sciences, Berlin).

**Status:** work in progress. Stage 1 (product data and choice sets) is complete.

## About the project

AI shopping agents increasingly choose and buy products on behalf of customers. This project measures, in **controlled product-selection tasks**, how strongly large language models (LLMs) acting as shopping agents react to product attributes such as price, rating, review count, badges ("Best seller", "Sponsored") and description style. It also tests whether persuasive cues make agents break a customer's stated requirements, such as a budget or a required feature.

Three instruction-tuned open-weight models with similar parameter counts (about 7–8 billion) act as agents. Each trial shows one agent a customer request and four real product listings, and the agent picks one product.

**Research questions**

- **RQ1:** To what extent do product attributes change the probability that an agent selects a product?
- **RQ2:** How does this sensitivity differ between open-weight models with similar parameter counts?
- **RQ3:** How well do the agents perform the task (task success, constraint compliance, efficiency, substitution for unavailable products), and does adding a persuasive cue to a product that breaks the customer's constraint make the agent more likely to choose it?

## Pipeline

| Stage | Notebook | What it does | Status |
|---|---|---|---|
| 1 | `01_product_data_and_choice_sets.ipynb` | Selects real products and builds choice sets of four | ✅ Done |
| 2 | `02_rewrites.ipynb` | Creates and checks emotional rewrites of the descriptions | Planned |
| 3 | `03_trial_builder.ipynb` | Randomises price, rating, reviews, badge and position; builds requests and paired cue trials | Planned |
| 4 | `04_mini_test.ipynb` | Small test of prompts and answer format | Planned |
| 5 | `05_run_agents.ipynb` | Pilot and main experiment with the three agents | Planned |
| 6 | `06_analysis.ipynb` | Evaluation metrics, conditional and mixed logit, price premiums, paired cue test | Planned |

## Repository structure

```
llm-shopping-agents-thesis/
├── README.md
├── notebooks/
│   └── 01_product_data_and_choice_sets.ipynb
└── data/
    ├── choice_sets.csv              # 50 choice sets: which 4 products belong together
    ├── products_selected.csv        # the 200 selected products with their attributes and feature flags
    └── data_preparation_log.json    # settings and product counts after each filtering step
```

## Data

Product metadata comes from the **Amazon Reviews 2023** dataset (Hou et al., 2024), categories *Electronics* and *Home and Kitchen*. Only product metadata is used (title, price, rating, number of ratings, features, description); no review texts and no reviewer information.

**Final selection:** 200 products in 50 choice sets, 25 sets of headphones and 25 sets of electric drip coffee makers. Each set contains four products from the same sub-category, from four different brands, with prices within 25% of the set's median, and at least one required feature that some products have and others lack. Prices are in US dollars.

| Step | Headphones | Coffee makers |
|---|---|---|
| Listings in the source category file | 1,610,012 | 3,735,584 |
| In the headphone or coffee-maker category branch | 102,057 | 8,559 |
