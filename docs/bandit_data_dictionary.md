# Bandit Data Dictionary

## Purpose

This document describes the datasets used for the contextual-bandit
recommendation component of Voice2Venture.

## recommendation_actions.csv

| Column | Description |
|---|---|
| action_id | Unique identifier for a recommendation action |
| recommendation | Recommendation text |
| category | Recommendation category |
| evidence_based_trigger | Trigger/rule associated with the action |

## context_action_mapping.csv

| Column | Description |
|---|---|
| context_rule | Rule describing when an action is relevant |
| action_id | Recommendation action identifier |
| priority | Priority assigned to the recommendation |
| rationale | Reason for recommending the action |

## train_bandit_interactions.csv / test_bandit_interactions.csv

| Column | Description |
|---|---|
| interaction_id | Unique interaction identifier |
| round | Sequential bandit round |
| business_id | Business identifier |
| city | Business city |
| sector | Business sector |
| employee_count | Number of employees |
| digital_adoption_score | Digital adoption context variable |
| finance_constraint | Finance constraint indicator |
| customer_reach_constraint | Customer reach constraint indicator |
| management_constraint | Management constraint indicator |
| profit_last_month | Profit indicator/value used by the interaction data |
| action_id | Action selected/evaluated |
| context_action_fit | Simulated fit between context and action |
| accepted | Whether the recommendation was accepted |
| simulated_outcome | Simulated outcome value |
| roi_proxy | Proxy for return on investment |
| reward | Reward received by the interaction |

## Important Note

The interaction dataset contains simulated feedback variables.
`roi_proxy` represents a proxy measure and should not be interpreted
as verified real-world ROI.