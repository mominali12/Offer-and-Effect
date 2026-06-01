# Literature Review

Approaches or solutions that have been tried before on similar projects.

**Summary of Each Work**:

- **Source 1: CAUSAL MACHINE LEARNING IN MARKETING**

  *   **Link:** [https://doi.org/10.56734/ijbms.v5n7a1](https://doi.org/10.56734/ijbms.v5n7a1)
  *   **Objective:** The study reviews the three primary purposes of **Causal Machine Learning (CML)** in marketing: performing more credible **impact evaluations** of interventions, detecting **effect heterogeneity** (moderation analysis) across customer segments, and learning **optimal policies** for customer targeting to maximize business outcomes.
  *   **Methods:**
      *   **Double Machine Learning (DML):** Combines predictive ML with doubly robust (DR) statistical functions to control for confounders in a data-driven way.
      *   **Causal Forests:** An algorithm used to assess treatment effects and identify which covariates most strongly predict effect size.
      *   **Optimal Policy Trees:** A method to create a decision tree that segments customers and assigns interventions (like coupons) to maximize overall effectiveness.
      *   **Causal Graphs:** Used to represent the relationships between variables and identify potential selection bias.
  *   **Outcomes:**
      *   CML provides a more precise impact evaluation than traditional methods like matching by reducing variance through data-driven covariate selection.
      *   It successfully identifies specific customer segments (e.g., leisure vs. business travelers or high vs. low-income groups) that respond differently to marketing efforts.
      *   While powerful, the study notes that CML's accuracy depends heavily on **data quality**; without high-quality data to satisfy the "selection-on-observables" assumption, CML can still overestimate impacts compared to experimental results.
  *   **Relation to the Project:**
      *   **Treatment Evaluation:** We can use CML to determine the causal effect of the `initial_offer` or `special_offer` on the final `purchase` decision.
      *   **Controlling for Confounders:** Variables like `tenure_months`, `base_engagement`, and `region` can be treated as **covariates** (confounders) that CML will control for to ensure that the estimated effect of an offer isn't biased by customer characteristics.
      *   **Effect Heterogeneity:** We can identify if certain segments—such as customers in a specific `region` or those with high `tenure_months` are more responsive to the `special_offer`.
      *   **Policy Learning:** We can develop an **optimal policy tree** to decide which customers should receive the `special_offer` based on their `base_engagement` and `tenure` to maximize the total number of purchases.
      *   **Handling Noise:** The `noise_factor` in our data mimics real-world observational data challenges. CML can help us navigate these "big data" contexts where it is unclear which variables are the most crucial to control.

  **Source 2: How causal machine learning can leverage marketing strategies: Assessing and improving the performance of a coupon campaign**

    **Link:** [https://doi.org/10.1371/journal.pone.0278937](https://doi.org/10.1371/journal.pone.0278937)

    **Objective:**
    The primary goal of the study is to demonstrate how **causal machine learning (ML)** can be used to assess the impact of marketing interventions—specifically a coupon campaign—on a retailer's sales. Unlike predictive ML, which focuses on identifying patterns for forecasting, this research aims to answer **"what if" questions** to determine the actual causal effect of coupons on customer behavior and to identify **optimal targeting strategies** that maximize sales.

    **Methods:**
    *   **Causal Forest:** The researchers utilized the causal forest algorithm to estimate **Conditional Average Treatment Effects (CATEs)**, allowing them to isolate the impact of coupons from other confounding background characteristics like income or age.
    *   **Optimal Policy Learning:** This data-driven approach was used to determine which specific customer segments should be targeted to maximize the campaign's effectiveness.
    *   **AIPW Estimator:** An Augmented Inverse Probability Weighting (AIPW) estimator was used to identify the **Average Treatment Effect (ATE)** across the entire customer base.
    *   **Honest Trees:** The study employed "honest" trees, where the data is split to ensure that the structure of the tree is built on one subsample while the treatment effects are estimated on another, preventing **overfitting bias**.

    **Outcomes:**
    *   **Category-Specific Success:** Only two of the five coupon categories—**drugstore items and "other food"**—had a statistically significant positive effect on sales.
    *   **Effect Heterogeneity:** The impact of coupons varied significantly across customer groups. For example, **drugstore coupons** were particularly effective for customers with **high prior purchases**, whereas **food coupons** were more effective for **reactivating dormant or low-purchase customers**.
    *   **Negative Effects:** Surprisingly, coupons for "other non-food products" were found to **significantly reduce** expected daily spending in the short term, possibly because customers used them for items they would have bought anyway.
    *   **Sustainability:** The study found that positive effects for certain categories (like drugstore items) were sustainable and even increased in subsequent periods.

    **Relation to the Project:**
    The features in your dataset align closely with the variables and concepts explored in the source:
    *   **`tenure_months` & `base_engagement`**: These map to the source's use of **prior purchasing behavior** and **pre-campaign spending** as critical covariates to control for selection bias.
    *   **`initial_offer` & `special_offer`**: These represent the **"treatments" (D)** analyzed in the study to determine their causal impact on the final outcome.
    *   **`followup_engagement` & `purchase`**: These correspond to the **outcome variables (Y)**, such as purchasing behavior during and after the campaign validity periods.
    *   **`region`**: This aligns with the source's discussion of **geographic information** as a factor in defining customer segments for optimal targeting.
    *   **`noise_factor`**: The source explicitly addresses **random noise** and the necessity of using "honest" causal ML models to ensure the findings represent true causal relationships rather than accidental patterns in messy data.

  **Source 3: Estimating Marketing Component Effects: Double Machine Learning from Targeted Digital Promotions**

    **Link:** [https://doi.org/10.1287/mksc.2022.1401](https://doi.org/10.1287/mksc.2022.1401)

    **Objective:**
    The primary objective of the study is to **estimate the causal effects of individual components** within complex, targeted digital marketing interventions. Specifically, the authors seek to "unbundle" the separate impacts of promotional offers (e.g., discounts, free shipping) and semantic choices (e.g., personalization, word choice) on consumer behavior across the entire conversion funnel, from opening an email to making a final purchase.

    **Methods:**
    *   **Doubly Robust Machine Learning (DML):** The authors synthesize and extend DML techniques to handle **endogenous targeting bias** (e.g. High-propensity customers got the offer AND were going to buy anyway) and high-dimensional treatment components.
    *   **Two-Stage Analysis:** 
        1.  **First Stage:** They use **Random Forests** to estimate propensity scores and outcome equations, recovering "orthogonalized signals" (individual treatment effect signals) for pairwise comparisons between promotions.
        2.  **Second Stage:** These signals are **projected onto a low-dimensional set of covariates**—the specific treatment components and consumer characteristics—to identify marginal average treatment effects (MATE) for each component.
    *   **Off-Policy Evaluation (OPE):** They employ OPE to predict how revenue would change under alternative targeting strategies based on their causal estimates.

    **Outcomes:**
    *   **Framing Matters:** The study found that **discounts framed as "clearance" events significantly outperform** the same discounts tied to specific products.
    *   **Funnel Disconnects:** Components that drive engagement at the top of the funnel (like opening an email) do not always lead to conversions at the bottom. For example, adding an exclamation point may increase open rates but suppress actual purchases.
    *   **Engagement as a Moderator:** The efficacy of marketing components is **significantly moderated by the prior engagement levels** of the consumers; highly engaged consumers often respond more strongly to both positive and negative cues.
    *   **Profitability Gains:** By leveraging these insights for improved targeting, the authors demonstrate a potential **increase in revenue of approximately 11%**.

    **Relation to the Project:**
    The methodology and findings in the source are directly applicable to your dataset features:
    *   **Targeting and Confounding:** Your features like `tenure_months`, `region`, and `base_engagement` are "pretreatment covariates" that likely influenced which `initial_offer` a customer received. The DML approach described in the paper is specifically designed to **correct for this targeting bias** to find the true causal effect of the offers.
    *   **Unbundling Offers:** The `initial_offer` and `special_offer` columns represent the "compound treatments" the paper analyzes. You can use the paper's projection method to **decompose these offers into specific attributes** (e.g., price vs. non-price) to see what truly drives the `purchase` outcome.
    *   **Conversion Funnel Analysis:** Your data tracks a sequence (`base_engagement` → `initial_offer` → `followup_engagement` → `special_offer` → `purchase`). This mirrors the paper's **funnel-based approach**, allowing you to identify if certain offers drive "followup" engagement but fail to lead to a final "purchase".
    *   **Segmentation:** The paper’s finding that **engagement level is a key moderator** suggests that `base_engagement` will be one of your most important variables for predicting how a customer will react to a `special_offer`.
