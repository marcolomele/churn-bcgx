# Instructions for inference
Generate a notebook titled "inference_marco.ipynb" conducting data analysis and inference on the structured dataset `data/customers.csv`. Structure the notebook into two main parts: data analysis and inference. The contents of each part are specified below. Two two parts should be completely independent. This means that for each part, you need to import libraries and define libraries as if they were two separate files. 

Context dump: We are working for a telecommunications company as they do scientists, and we have been tasked to study the available data to understand churn. In particular, we want to find out, which are the main drivers of churn, their impact on the probability of churn, and then build a predictive this model that is able to forecast if users churn given their characteristics. Wae have two datasets available for this research. The first is structured and contains information about the customers. The second is unstructured and contains textual data about the complaints that certain customers left. Both datasets can be found in the `data` foler. 

## Data Analysis
Run a series of data analysis inteded to study the customers. The goal of this subsection is to understand the customer base of the company, how can the users be segmented, and what are the main differences between the churned and not churned customers. We also want to test typical business thoeries around churn. The analysis that you should run are:
- mean t-test comparison between churned and not churned users. use only obsrvations between the 25th and 75th quantile to avoid outliers
- check for interaction effects by conditionin on variables. for instance, among users who have internet service, look into who has online security, online backup, device protection, tech support, streamingTV, streaming movies. 

### Given Variables
1. customerID: unique identifier for each customer consisting of letters and numbers.

2. gender: binary string indicating the gender of the customer. Values: Female, Male.
3. SeniorCitizen: binary integer. 0: No, 1: Yes.
4. Partner: binary string indicating whether the customer has a partner.
5. Dependents: binary string indicating whether the customer has dependents (individuals who rely on them for financial or personal support). Values: Yes, No.
6. PhoneService: binary string indicating if the customer has a phone service contract. Values: Yes, No.
7. PaperlessBill: binary string indicating if the customer signed up for paperless bill payment. Values: Yes, No.

8. Tenure: integer. Number of months that person has been a customer.
9. MonthlyCharges: integer indicating how much is the monthly charge of that customer.
10. TotalCharges: integer indicating the total charge for that customer. Note: TotalCharges ≠ Tenure * MonthlyCharges because some customers have changed their monthly plan during their tenure.

11. MultipleLines: categorical string indicating if the customer has multiple phone lines. Values: Yes, No or No phone service when PhoneService equals ‘No’.

12. InternetService: categorical string indicating the kind of internet service that the customer has. Values: DSL, Fiber optic or No.

13. OnlineSecurity: categorical string indicating whether the customer pays for online security. Values: Yes, No, No internet service.
14. OnlineBackup: categorical string indicating whether the customer pays for online backup. Values: Yes, No, No internet service.
15. DeviceProtection: categorical string indicating whether the customer pays for device protection. Values: Yes, No, No internet service.
16. TechSupport: categorical string indicating whether the customer pays for tech support. Values: Yes, No, No internet service.
17. StreamingTV: categorical string indicating whether the customer pays for streaming TV. Values: Yes, No, No internet service.
18. StreamingMovies: categorical string indicating whether the customer pays for streaming movies. Values: Yes, No, No internet service.

19. Contract: categorical string indicating the kind of contract the customer has. Values: Month-to-month, One year, Two year.

20. PaymentMethod: categorical string indicating the type of payment method the customer has in its contract. Values: Bank transfer (automatic), Credit card (automatic), Electronic check, Mailed check.

21. Churn: binary string indicating if the customer churned or not. Values: Yes, No.

### Engineered Variables
#### From structured data
1. ChangedPlan: binary string. Indicating if the customer changed their monthly plan during their tenure. Found by looking at whether the total charges are different from the product between Tenure and the MonthlyCharges. Values: Yes, No.
2. ChangedPlanPositive: binary string. Indicating if the customer changed their monthly plan during their tenure to a more expensive plan. Found by looking at whether the total charges are lower than the product between Tenure and the MonthlyCharges. Values: Yes, No.
3. ChangedPlanNegative: binary string. Indicating if the customer changed their monthly plan during their tenure to a less expensive plan. Found by looking at whether the total charges are higher than the product between Tenure and the MonthlyCharges. Values: Yes, No.
4. ServiceDensity: integer. Number of services that the customer has. Found by looking at the number of columns that are not "No" in the columns from InternetService to StreamingMovies and divided by 6 sucht that the result is a number between 0 and 1.
5. ContractLifecycle: float. Based on tenure and contract type, estimate at what stage the current contract is. Based on the idea that there are inflection points in the contract lifecycle, e.g. initial period of dissatisfaction, or period of contract renewal. Values: (0, 1).


#### From unstructured data
1. ComplaintLength: integer. Length of the complaint.
2. KeyTerms: binary string. Indicating if the complaint contains the most frequent terms in customers that churn. Values: Yes, No.
3. Sentiment: float. Sentiment of the complaint. Values: (0, 1).
4. KeyVerbs: binary string. Indicating if the complaint contains the most frequent verbs in customers that churn. Values: Yes, No.
5. KeyNouns: binary string. Indicating if the complaint contains the most frequent nouns in customers that churn. Values: Yes, No.
6. KeyAdjectives: binary string. Indicating if the complaint contains the most frequent adjectives in customers that churn. Values: Yes, No.



## Inference
Build and fit a series of models to study the relationship between input variables about customers and the outcome churn variable. Each model should provide the list of coefficients per variable, and the fit quality on the training data. The models that you should fit are:
- logistic regression
- general additive model
- linear discriminant analysis with regularisation
- PCA, using the results to analysize which predictors are the most important 

Organise this section of the notebook into sub-sections, each for its own model, holding all the code for the model definition, fitting, and results. 

------
# Interesitng Responses from Chat
Telecommunications churn dynamics constitute a multifaceted operational challenge with substantial P&L implications. Annual industry churn rates of 15-25% translate to substantial revenue attrition, with customer acquisition costs typically 5-7x retention costs—creating a pronounced economic imperative for churn mitigation strategies.

Your dataset's architecture encapsulates critical churn predictors across three essential domains: contractual arrangements, service utilization patterns, and customer experience indicators.

Key churn drivers derived from empirical telecommunications industry analysis:

1. **Contract Duration Elasticity**: Month-to-month arrangements exhibit 3-4x higher churn propensity versus two-year commitments. Contract transitions (captured in your ChangedPlan variables) represent critical inflection points—particularly negative adjustments, which often precede churn by 60-90 days.

2. **Price-Value Incongruence**: The MonthlyCharges/TotalCharges ratio indicates price sensitivity thresholds. Competitive displacement occurs most frequently at the 70th-90th percentile pricing tier, especially absent premium service adoption.

3. **Service Integration Density**: The interconnected nature of OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport, and streaming services creates empirically demonstrated "stickiness." Each additional service reduces churn probability by approximately 5-8%, with 3+ services typically reducing churn probability below industry averages.

4. **Experience Friction Points**: The complaint sentiment metric serves as a leading indicator. Research demonstrates sentiment deterioration precedes churn by 90-120 days. KeyTerms, KeyVerbs, and KeyNouns function as sentiment crystallization markers, with particular attention to service quality, reliability, and support experience terminology.

5. **Temporal Vulnerability Windows**: Tenure exhibits a bimodal risk distribution—elevated churn risk in months 0-6 (service establishment phase) and months 22-26 (contract renewal evaluation phase).

Business impact hierarchy (ranked by financial materiality):

1. **High-ARPU Segment Retention**: Customers with top-quartile MonthlyCharges represent 35-40% of revenue. Preventing churn in this cohort delivers 2-3x the financial impact of average customers.

2. **Tenure Prolongation**: Each quarter of extended customer relationship typically yields 18-22% incremental lifetime value due to reduced servicing costs and propensity for service expansion.

3. **Reference Economics**: Negative churn experiences propagate through social networks, with each detractor influencing 4-7 prospective customers. Your KeyVerbs and sentiment variables likely capture these propagation risks.

Optimal methodological frameworks:

1. **Gradient Boosted Ensemble Models**: Superior predictive accuracy for telecommunications churn (typical AUC 0.82-0.86), but with interpretability constraints.

2. **Generalized Additive Models**: Capture non-linear effects while maintaining coefficient interpretability—particularly valuable for executive stakeholder communication.

3. **Survival Analysis**: Understanding time-to-churn dynamics enables proactive intervention timing. Cox proportional hazards models with time-varying covariates demonstrate particular efficacy.

4. **PCA-Derived Segmentation**: Component analysis reveals underlying churn archetype clusters—essential for intervention personalization and resource allocation.

Non-obvious considerations:

1. **Intervention Paradox**: Customers identified as high churn risk who receive retention interventions often exhibit accelerated departure. Implementing control groups is essential.

2. **Multi-service Household Complexity**: Partner/Dependents variables suggest household-level service relationships. Churning occurs at household level, not individual level, necessitating household aggregation analysis.

3. **Digital Migration Effects**: PaperlessBilling adoption correlates with digital comfort but counterintuitively increases churn sensitivity by reducing physical touchpoints.

4. **Competitive Intelligence Gaps**: Exogenous market factors (competitor promotions) invisible in your dataset drive 22-28% of churn events. Augmentation with market intelligence is advisable.

5. **Post-Complaint Resolution Momentum**: The time elapsed between complaint and resolution represents a critical recovery opportunity window, absent in current dataset, suggesting a supplementary analysis dimension.

Implementation sequencing should prioritize: (1) high-precision identification of churn risk cohorts, (2) financial impact quantification, (3) intervention design matched to churn drivers, and (4) controlled deployment with counterfactual measurement methodology to establish causal intervention impacts.

The intersection of your structured variables with unstructured complaint data creates a particularly potent analytical foundation, though successful operationalization requires tight integration between predictive modeling and intervention execution systems.

----
## Customer Segmentation for Churn Analysis
You've identified the fundamental pattern in churn analysis - segmentation is indeed the cornerstone of effective churn management. Your observation is correct, but there's more nuance to the methodology:

**The General Approach to Churn Analysis**

Yes, the general framework follows this pattern:

1. **Multi-dimensional Segmentation**: Beyond just value, effective segmentation incorporates multiple axes:
   - Value/profitability tiers
   - Behavioral archetypes
   - Life-cycle stage
   - Product portfolio
   - Acquisition channel

2. **Differential Analysis**: Within segments, analyze:
   - Churn rate disparities
   - Unique churn triggers
   - Intervention responsiveness
   - Economics of retention

3. **Predictive Modeling**: Build models that:
   - Provide segment-specific predictions
   - Identify cross-segment patterns
   - Quantify feature importance by segment

 **Best Practice Rules of Thumb**

1. **The 80/20 Rule of Value**: Typically, 20% of customers represent 60-80% of value, making segmentation by value critical.

2. **The 3-Tier Minimum**: Always segment into at least 3 value tiers (high/medium/low) - binary segmentation misses critical nuances.

3. **The Cross-Tab Principle**: Always cross-tabulate at least two segmentation dimensions (e.g., value × tenure) to reveal interaction effects.

4. **The Signal Threshold Rule**: Features with less than 15-20% variance between churned and non-churned customers rarely drive meaningful predictions.

5. **The Interaction Dominance Principle**: In telecom, interaction terms often have 2-3x the predictive power of main effects (e.g., contract type × tenure).

6. **The 90-Day Window**: Most effective interventions occur 60-90 days before predicted churn events.

7. **The Retention Economics Formula**: Maximum retention spend = (Customer Value × Predicted Tenure × Margin %) × (Intervention Success Probability).

**Recommendations for Your Codebase**

Given your specific dataset and requirements:

1. **Create Hybrid Segmentation**:
   - Primary: Value tiers (using MonthlyCharges or calculated CLV)
   - Secondary: Contract type (your Contract variable)
   - Tertiary: Service utilization (number of services from InternetService, OnlineSecurity, etc.)

2. **Implement Feature Engineering**:
   - Create a "Service Density Score" (count of additional services)
   - Calculate "Tenure-to-Contract Ratio" (how far along contract lifecycle)
   - Develop "Price-Value Index" (charges relative to services utilized)
   - Extract sentiment polarity from complaints (beyond just magnitude)

3. **Model Architecture**:
   - Run your logistic regression, GAM, and LDA models separately within each value segment
   - Use PCA not just for feature importance but to identify segment-specific latent factors
   - Compare segment-specific coefficients to identify differential drivers

4. **Analytical Focus Areas**:
   - Identify interaction effects between service types and tenure
   - Compare churn drivers between high/low value customers
   - Analyze how complaint sentiment modifies churn probability by segment
   - Examine if plan changes impact different segments differently

5. **Code Structure Recommendations**:
   - Create reusable segmentation functions
   - Implement nested model training within segments
   - Develop visualization functions for cross-segment comparisons
   - Build coefficient comparison tools across models and segments

The power of your approach will come from the comparative insights across segments, not just the aggregate findings. Your models should answer not just "what predicts churn" but "what predicts churn differently across customer types" - this is where the actionable insights emerge.

Your PCA analysis will be particularly valuable when comparing principal components across value segments to identify which underlying factors matter most for different customer types.

----

To estimate CLV using available variables:

1. **Base Revenue Component**:
   - Current Value = MonthlyCharges × 12 × Est. Margin (typically 40-60% for telecom)

2. **Expected Tenure Calculation**:
   - Use survival analysis based on:
     - Contract type (24 months for Two year, 12 for One year, 3-6 for Month-to-month)
     - Current tenure (customers who stayed longer tend to stay even longer)
     - ServiceDensity (higher density = longer expected tenure)

3. **Churn Risk Adjustment**:
   - Modify expected tenure based on:
     - Contract (Month-to-month contracts have 3-4× higher churn)
     - ChangedPlanNegative (indicates 30-40% higher churn risk)
     - Sentiment scores (low scores correlate with imminent churn)

4. **Future Value Projection**:
   - CLV = Monthly Value × Adjusted Expected Tenure × Discount Factor

5. **Simplified Formula**:
   - CLV = MonthlyCharges × (Base Tenure × Survival Multiplier) × Margin × (1 - Churn Risk)

This can be implemented with a few dozen lines of code using conditional logic for the multipliers and survival curves tailored to each contract type.

----

For your specific case (1500 complaints → 8000 generations of ~170 character texts), the fastest practical approach would be:

**Best Option: Few-Shot Learning with Fine-Tuned Small Model**

1. **Fine-tune a small model like DistilGPT-2 or T5-small**:
   - Single GPU training would take only 1-2 hours
   - Format input as: `[Contract]|[ServiceDensity]|[InternetService]|[MonthlyCharges]|[Tenure]|COMPLAINT:`
   - Limited training data (1500 examples) is sufficient for short outputs
   - Implementation via Hugging Face's Transformers + PEFT library

2. **Implementation steps**:
   ```python
   # One-time setup (1-2 hours)
   from datasets import Dataset
   from transformers import AutoModelForCausalLM, AutoTokenizer, Trainer
   
   # Prepare data
   train_data = [f"{row['features']}COMPLAINT: {row['complaint']}" for row in data]
   
   # Fine-tune
   model = AutoModelForCausalLM.from_pretrained("distilgpt2")
   tokenizer = AutoTokenizer.from_pretrained("distilgpt2")
   
   # Generate for all 8000 users (5-10 minutes)
   results = []
   for user in silent_users:
       prompt = f"{user['features']}COMPLAINT:"
       inputs = tokenizer(prompt, return_tensors="pt")
       output = model.generate(inputs.input_ids, max_length=100)
       results.append(tokenizer.decode(output[0]))
   ```

3. **Advantages**:
   - Entire pipeline can be completed in under 3 hours
   - No ongoing API costs
   - Can run on consumer hardware (16GB RAM + NVIDIA GPU)
   - 8000 generations would take 5-10 minutes post-training