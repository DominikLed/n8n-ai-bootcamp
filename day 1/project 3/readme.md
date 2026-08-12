# P3 – Simple Evaluations

## Overview

Simple workflow to **demo n8n’s Evaluation nodes**: it pulls rows from a dataset (users upload `evals.csv` into an n8n Data Table), runs an LLM classification, then records metrics + outputs back to the evaluation run.  

## Setup

* In n8n, create a **Data Table** (e.g. “evals”) and **upload `evals.csv`** as the dataset. 

## Workflow

1. **Select 'Evaluations'** from the top of your n8n workflow. Select **Add evaluation trigger**

2. **When fetching a dataset row** (Evaluation Trigger)

   * n8n feeds one row at a time from the uploaded Data Table.

3. **Add 'Check if evaluating' node**

   * Ensures the workflow is running in evaluation context.

4. **Add 'Set Metric' – 'Categorization'**

   * Compares **expected_output** (from the dataset row) vs the model’s actual label and stores a `categorization` metric.

5. **Set Outputs**

   * Writes outputs back to the evaluation run (model output + metric fields).
   
   - Name: `Categorization`
   - Value: `{{ $json.Categorization }}`
   
6. **Run Evaluation**

   * Select **Evaluations** from the top and select **Run Evaluation**
   * Things to try out: 
   		- Modify the system prompt.
   		- Try a different model.