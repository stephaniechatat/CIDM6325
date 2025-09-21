# Product Requirements Document (PRD)


## 1. Document Information
- Product/Feature Name: Smart Pantry Tracker
- Author(s): Stephanie Chattat
- Date Created: 2025-09-20
- Last Updated: 2025-09-20
- Version: 0.1 (Draft)

## 2. Overview

### Summary
Smart Pantry Tracker is a web application that is designed to minimize food waste and streamline meal planning by connecting pantry visibility with recipe intelligence. It empowers users to reduce waste by using ingredients before expiration, discover immediate **Cook Now** recipes, and receive **Near Match** suggestions backed by credible substitutions. By combining practicality with decision support, it improves usability, reduces waste, and delivers
transparent substitution guidance that builds confidence in everyday cooking.

### Problem Statement
Many households face persistent challenges with food waste and daily meal planning. Ingredients often expire before use, 
and recipes are abandoned due to one or two missing items. Existing pantry apps emphasize inventory tracking but fall short of turning that data into
actionable cooking decisions. On the other hand, recipe platforms assume perfect ingredient availability
and offer very limited substitution options. Smart Pantry Tracker closes this gap 
with digital pantry tracking, intelligent recipe matching, and systematic substitution logic.

### Goals & Objectives
- Provide clear ingredients visibility with experation dates and quantity tracking.
- Deliver recipe suggestions categorized as **Cook Now** (100% match) or **Near Match** (≤2 items missing with substitutions).
- Improve decision clarity by incorporating evidence-based substitutions supported by authoritative sources.
- Reduce food waste and household costs by maximizing ingredient use.

### Non-Goals
- Barcode scanning or automated grocery ingestion. 
- Personalized nutrition or diet planning. 
- Grocery delivery or shopping list integrations. 
- User accounts, profiles, or authentication.

## 3. Context & Background

### Business Context
In the United States, households are the leading source of food waste, contributing to nearly one-third of food supply that goes unused each year, creating significant economic and sustainability costs (ReFED, 2025). Ambiguity in expiration and date labels leads many consumers to dispose of safe ingredients too early (USDA, 2024; Harvard Food Law & Policy Clinic, 2025).Minimizing waste contributes to broader sustainability goals and provides immediate financial benefits to households. Smart Pantry Tracker supports these objectives by combining pantry visibility
with recipe intelligence to maximize ingredient use, minimize waste, and improve everyday
decision-making.


### Market and Customer Insights
Research shows that households discard large amounts of edible food due to confusion around date
labeling (Harvard Food Law & Policy Clinic, 2025). Most pantry apps stop at inventory management, while recipe platforms expect full ingredient lists, leaving little support for real-world cooking situations.

The target users(personas) include:
- **Individual home cooks:** seek straightforward meal options from on-hand ingredients.  
- **Families/households:** aim to reduce waste and streamline shared meal planning.  
- **Budget-conscious users:** maximize grocery value through efficient ingredient use.  
- **Recipe contributors:** share adaptable recipes with substitution guidance.  
- **Culinary learners:** build skills by experimenting with substitutions and pantry-driven meals.  
- **Time-pressed professionals:** need fast, reliable recipe suggestions with minimal planning effort.


Despite their differences, these personas highlight similar requirements such as: clearer expiration guidance, practical substitution support, and recipe recommendations that adapt to real-time pantry conditions. Smart Pantry Tracker is designed to meet these requirements directly.


### Competitive and Benchmark References

- **Out of Milk / Pantry Check:** Pantry-focused apps that track inventory but rarely integrate 
recipe matching or substitution guidance.  
- **AllRecipes / Tasty:** Recipe platforms offering breadth of meal options but assuming perfect 
ingredient availability, with minimal substitution support.  
- **SuperCook / Cooklist:** Hybrid tools that suggest recipes from available ingredients, but generally 
lack systematic substitution logic, transparent evidence sources, or expiration-driven prioritization. 

Unlike these existing tools, Smart Pantry Tracker integrates multiple missing elements such as expiration tracking, evidence-backed substitutions, and a lightweight AI summarizer. This one integtrated workflow creates a unique, end-to-end system that reduces waste and supports confident meal choices.

## 4. Scope

### In Scope
- **Digital pantry (CRUD):** add, edit, delete ingredients with quantity and expiration date.  
- **Recipe suggestion engine:**  
  - **Cook Now**: 100% match with available ingredients.  
  - **Near Match**: 1-2 items missing with substitution suggestions.  
- **Substitution rules module:** curated dataset of common ingredient swaps.  
- **Recipe data:** seeded set of recipes in the database (no scraping required).  
- **AI summarizer (lightweight):** generates 2-3 sentence user-friendly plans for Near Match results,
using only curated substitutions and citations.  
- **Evidence Drawer:** panel that discloses substitution sources, expiration guidance, and matching
assumptions.  
- **Documentation in `/docs/`:** captures assumptions (substitution rules, expiration logic),
formulas (matching algorithm), and iteration notes.

### Out of Scope
- Barcode scanning or automated grocery ingestion. 
- Personalized nutrition or diet planning. 
- Grocery delivery or shopping list integrations. 
- User accounts, profiles, or authentication.

## 5. User Stories & Use Cases

### Primary User Personas
- **Individual home cooks** seeking straightforward meal options from on-hand ingredients.  
- **Families/households** looking to reduce waste and streamline shared meal planning.  
- **Budget-conscious users** maximizing grocery value through efficient ingredient use.  
- **Recipe contributors** sharing adaptable recipes with substitution guidance.  
- **Culinary learners** experimenting with substitutions to build cooking skills.  
- **Time-pressed professionals** wanting fast, reliable recipe suggestions with minimal planning. 

### User Stories
- As an **individual home cook**, I want to see recipes that match my pantry, so that I can make meals without last-minute shopping.
- As a **family household member**, I want to view ingredients nearing expiration, so that we can plan shared meals that reduce food waste.
- As a **budget-conscious user**, I want Near Match recipes with credible substitutions, so that I can avoid extra grocery trips and stretch my budget.  
- As a **recipe contributor**, I can add adaptable recipes with substitution notes, so that others can benefit from my cooking knowledge.  
- As a **culinary learner**, I want substitution sources explained, so that I can gain confidence in experimenting with pantry-driven meals.  
- As a **time-pressed professional**, I can instantly filter for Cook Now recipes, so that I can make a fast decision and start cooking quickly.


### Use Case Scenarios

**Happy Path**
1. User opens the app and adds pantry items with quantities and expiration dates.  
2. User requests recipe suggestions.  
3. System displays **Cook Now** recipes (100% match) and **Near Match** recipes (≤2 items missing with substitutions).  
4. User selects a Near Match recipe, reviews the AI-generated summary (2–3 sentence plan), and checks the Evidence Drawer for substitution sources.  
5. User saves the recipe to cook later or uses it immediately. 

**Edge Case 1: No Matching Recipes Available**
- The items don’t overlap with seeded recipes or the pentry is nearly empty
- System displays: *"No Cook Now or Near Match recipes available."*  
- Suggests adding more pantry items or expanding recipe filters.

**Edge Case 2: Expired Ingredient Conflict**
- A recipe requires itema that exists in the pantry but one or more are already past expiration.
- System flags expired ingredients and excludes the recipe from **Cook Now** or **Near Match**.  
- Evidence Drawer explains why the recipe was excluded.

## 6. Functional Requirements

**FR-001: Pantry Item Management**
The system must allow users to create, read, update, and delete pantry items, including name, quantity, unit, and expiration date.

**FR-002: Recipe Matching Engine** 
The system must filter recipes into **Cook Now** (100% match) and **Near Match** (≤2 items missing with substitutions).

**FR-003: Substitution Rules Module** 
The system must apply a curated set of substitution rules when ≤2 items are missing.  

**FR-004: Evidence Drawer** 
Each substitution must display supporting source(s) and assumptions in a user-accessible panel.  

**FR-005: AI Summarizer (Lightweight)**
The system must generate a 2–3 sentence summary for Near Match results using only curated substitutions and citations.

**FR-006: Error Handling**
The system must handle common edge cases, including no matching recipes and expired ingredients in recipes.

## 7. Non-Functional Requirements

**Performance:** 
- Pantry CRUD operations (add, edit, delete) should apply immediately and reflect in the UI without noticeable delay. 
- ≥90% of recipe match requests should return results within 2 seconds for a typical pantry (≤200 items) and a seeded recipe set (≤500 recipes).
- The system should maintain acceptable performance as pantry size, recipe data, and substitution rules grow during testing. 

**Scalability:**
- Designed initially for single-household use with a modest recipe library.  
- Architecture should allow gradual growth in pantry size, recipe data, and substitution rules without major redesign.
- Pantry CRUD, recipe matching, and substitution logic should remain high-performing as data sets grow.
- The architecture should allow for future growth, including multi-household support, expanded recipe libraries, and integrations, without introducing architectural constraints.

**Accessibility:**
- Application must meet WCAG guidelines, including keyboard navigation, sufficient color contrast, and alt text for icons/images.

**Security/Compliance:**
- The system must store only minimal data needed for pantry items and seeded recipes.  
- No personal identifying information (PII) is collected in the MVA.  
- Data handling must prevent unauthorized access or loss during development and testing.

**Reliability/Availability:**
- Pantry CRUD and recipe matching must continue to function even if external evidence sources are temporarily unavailable.
- In degraded mode, the system should fall back to cached substitution rules and display a warning to the user.

## 8. Dependencies

**Internal System Dependencies** 
- Django API layer for handling pantry CRUD operations and recipe matching logic.  
- PostgreSQL database for storing pantry items, recipes, substitution rules, and evidence sources.  
- AI summarizer service (lightweight module) for formatting Near Match results into user-friendly plans.

**External APIs / Third-Party Services**
- Authoritative food safety and substitution references (USDA, FDA, ReFED, Harvard FLPC, NDSU Extension) for evidence sources.  
- GitHub for code hosting, version control, and documentation.  
- Markdown/PDF tooling for documentations and sharing deliverables. 

**Cross-team deliverables**
- Seed recipe dataset curated by project team for initial implementation.  
- Substitution rules dataset sourced and documented by team members.  
- System sketch and documentation maintained in `/docs/` for alignment across iterations.

## 9. Risks & Assumptions

### Risks
- **Incomplete recipe or ingredient coverage:** If the seeded dataset is too limited, users may not see meaningful Cook Now or Near Match results.  
*Mitigation:* Seed the database with common recipes and expand the library incrementally.  

- **Inaccurate or unhelpful substitutions:** Low quality or incomplete substitution rules could lead to confusing or unhelpful recipe suggestions.  
*Mitigation:* Use curated substitutions from trusted sources, collect user feedback, and show evidence in the drawer.  

- **Evidence Drawer lacks clarity or citations:** If explanations are unclear or missing citations, users may not trust substitution guidance.  
*Mitigation:* Require each substitution and expiration rule to include source metadata; conduct usability testing for clarity.  

- **Scope creep relative to MVA:** Risk of adding new features and scope expension beyond MVA may pull resources away from core deliverables.  
*Mitigation:* Use review gates to confirm or defer features; keep out-of-scope items documented in `/docs/`.  

- **User adoption challenges:** If the interface feels too complex, first-time users may fail to complete key flows.  
*Mitigation:* Conduct usability checks; refine UI to ensure ≥70% success on first use.


### Assumptions

- Data input for pantry items will be manually logged by Users.  
- A seeded recipe dataset is sufficient to demonstrate Cook Now and Near Match flows.  
- Substitution rules from USDA, FDA, NDSU Extension, and similar sources are reliable and applicable.  
- Internet access is available for linking to external evidence sources and cached copies will be provided where possible if offline.  
- Single-household usage is assumed for the MVA.

## 10. Acceptance Criteria

- **FR-001: Pantry Item Management** passes when a user can add, edit, delete and view items and the "Use-First" list accurately orders the data by closest expiration dates.

- **FR-002: Recipe Matching Engine** passes when the system consistently separates 
recipes into **Cook Now** (100% match) and **Near Match** (≤2 items missing with substitutions).

- **FR-003: Substitution Rules Module** passes when Near Match suggestions use only curated rules, and ≥80% of substitutions are judged helpful in user testing.  

- **FR-004: Evidence Drawer** passes when ≥80% of substitution and expiration explanations display at least one authoritative source link.  

- **FR-005: AI Summarizer (Lightweight)** passes when Near Match results include a 2–3 sentence summary that references available substitutions without introducing any unsupported rules.

- **FR-006: Error Handling** passes when the system:  
1) Displays a clear and user-friendly message if no Cook Now or Near Match recipes are available.  
2) Excludes recipes containing expired ingredients and clearly explains why in the Evidence Drawer.

## 11. Success Metrics

- **Usability:** ≥70% of first-time users can add ingredients, view expiration status, and receive at least one recipe suggestion without guidance.
- **Decision clarity:** At least 60% of sessions result in one recipe being viewed or saved (“Cook Now” or “Near Match”).
- **Substitution helpfulness:** >60% of Near Match substitutions are rated “helpful” by users.
- **Evidence transparency:** ≥80% of substitution explanations show linked 
authoritative sources in the Evidence Drawer.

## 12. Rollout & Release Plan

### Phasing
**MVP:**
- Pantry CRUD with expiration and quantity tracking. 
- Recipe matching engine with Cook Now and Near Match categories.  
- Substitution rules module (curated dataset).  
- Evidence Drawer with citations.  
- AI summarizer producing 2–3 sentence Near Match guidance.

**Future Iterations:**
- Expanded recipe library and substitution rules.
- Barcode scanning integrations.
- Multi-household support and shared planning features.
- Authentication and authorization for user accounts and household sharing. 
- Enhanced reporting and analytics.
- Expanded help guides, FAQs, and onboarding materials as functionality (auth,integrations, personalization) grows.

### Release Channels
- **Beta:** Initial release will be in the Github repository, shared with the team and test users for feedback
- **Staged Rollout:** Incremental improvements to expand recipe library, refine substitution rules and UI enhancements to be released in staged versions
- **General Availability:** Production ready release of the MVA that includes pantry CRUD, recipe matching, evidence drawer and AI summarizer.

### Training and Documentation
- **Internal Documentation:** `/docs/` folder will capture assumptions, substitution rules, matching logic, and iteration notes.
- **Support Guides:** A well structured and clear README that holds setup instructions, usage examples and quick links to deliverables.
- **User Education:** Clear Evidence Drawer explanations and guidance to help users 
better understand substitutions and expiration logic without external training.

## 13. Open Questions

- How shouldd the system handle ambigious data entry such as units or quantities?
- Can users overide expired items with a warning message or should these items always be excluded from recipe matching?
- What's the volume of data needed to efficatevely showcase Cook Now and Near Match flows?
- What is the minimum set of authoritative sources required for each substitution in the Evidence Drawer?  


## 14. References

- 📄 **Memo (PDF):** [week1/docs/memo.pdf](week1/docs/memo.pdf)
- 🖼️ **System Sketch:** [week1/docs/system_sketch.png](week1/docs/system_sketch.png)
- 📚 **Evidence Base:** [week1/docs/evidence_base.md](week1/docs/evidence_base.md)
- ⚠️ **Risk Register:** [week1/docs/risk_register.md](week1/docs/risk_register.md)

**Competitor References**  
- Out of Milk: <https://www.outofmilk.com/>  
- Pantry Check: <https://pantrycheck.com/>  
- AllRecipes: <https://www.allrecipes.com/>  
- Tasty: <https://tasty.co/>  
- SuperCook: <https://www.supercook.com/>  
- Cooklist: <https://www.cooklist.com/>  

**Evidence Base:**
U.S. Department of Agriculture (2024). Food Product Dating. 
<https://www.fsis.usda.gov/food-labeling/food-product-dating> 
U.S. Food and Drug Administration & USDA (2024). Proposed rule on food date 
labeling. <https://www.federalregister.gov/> 
ReFED (2025). Food Waste Insights Engine. <https://refed.org/>
Harvard Food Law & Policy Clinic (2025). Consumer perceptions of date labels and 
food waste. <https://chlpi.org/> 
North Dakota State University Extension (2024). Ingredient Substitutions. 
<https://www.ndsu.edu/agriculture/extension>
U.S. Department of Agriculture (2025). FoodData Central. <https://fdc.nal.usda.gov/>