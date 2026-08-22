VOICE2VENTURE FINAL DATA PACKAGE

WHAT YOU CAN USE NOW
1. master_business_context.csv
   - 998 synthetic business profiles.
   - Calibrated to real World Bank 2022 aggregate indicator distributions for 8 Indian cities.
   - Use as the contextual feature dataset.

2. recommendation_actions.csv
   - 10 recommendation actions (contextual-bandit arms).

3. context_action_mapping.csv
   - Evidence-based context-to-action rules.

4. bandit_interactions.csv
   - 79,840 simulated contextual-bandit interactions.
   - Use for offline training/evaluation of LinUCB, Thompson Sampling, epsilon-greedy, and static baselines.

5. train_* and test_* files
   - Ready 80/20 split by business profile.

SOURCE AND METHODOLOGY
The real source used for calibration is the uploaded World Bank Informal Sector Enterprise Surveys India 2022 aggregate custom-query file.
Because respondent-level microdata was access-restricted at generation time, individual profiles were not claimed to be real survey respondents.
All generated rows are explicitly synthetic/simulated and reproducible with random seed 20260822.

FOR YOUR PRESENTATION
Say:
"Real World Bank 2022 enterprise-survey indicators were used to calibrate a synthetic business-context and sequential interaction layer. The synthetic layer is explicitly labelled and used only because public aggregate indicators do not provide the repeated recommendation-feedback trajectories required for contextual-bandit experimentation."

DO NOT SAY
"We collected 998 real respondents."

Instead say
"We generated 998 synthetic business profiles calibrated to real World Bank enterprise-survey indicator distributions."
