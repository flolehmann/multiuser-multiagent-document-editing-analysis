# Collaborative Document Editing with Multiple Users and AI Agents — Analysis Code

This repository contains the analysis code for the paper:

> **Collaborative Document Editing with Multiple Users and AI Agents**
> [arXiv:2509.11826](https://arxiv.org/abs/2509.11826)
> 
> Florian Lehmann, Krystsina Shauchenka, Daniel Buschek

## Overview

This paper investigates how AI agents can be integrated directly into collaborative writing environments, addressing a key limitation of current AI writing tools — they are designed for individual use, which disrupts co-writing workflows.

This repository provides the code used to process interaction logs and conduct the quantitative analysis reported in the paper.

Attention: some logs and a document have been removed for privacy purpose. Thus, the results will vary slightly from those reported in our paper.

## Citation

If you use this code in your research, please cite:

```bibtex
@article{arxiv2509.11826,
  title   = {Collaborative Document Editing with Multiple Users and AI Agents},
  journal = {arXiv preprint arXiv:2509.11826},
  year    = {2025}
}
```

## Input data

Input data should be added to input folder in order to get results. It includes: survey responses, database collections, logdata, and codings.

You can find the analysis_input-data.zip file in our OSF: https://osf.io/2gavd/files/osfstorage


## 01_intro_questionnaire

Processes data from introduction survey

## 02_final_questionnaire

Processes data from the final survey

## 03_interaction_data

Prepares the data for further analyses

## 03_01_agent_analysis

Analyzes agent related results

## 03_02_task_analysis

Analyzes task related results

## 03_03_comment_analysis

Analyzes comment related results

## 03_04_final_texts

Analyzes the final texts 

## 03_05_codings

Analyzes our codings of agents, comments, and tasks

## 03_06_collaboration

Analyzes collaboration measures, e.g. interaction switches



Metrics used for analysis, WIP:

**RQ1: How can users define AI agents?**

1. How many agents per document were created? agents in database per document
2. How often did users update agents? AGENT_UPDATE
3. How often did users use suggestions for AI agent definition? AGENT_CV_SECTION_GENERATE for generation request, AGENT_CV_SECTION_GENERATED_VALUE_ADD for actual suggestion usage
4. How often did users use presets? AGENT_PRESET_USE for preset use and AGENT_PRESET_VIEW for preset view

**RQ2: What tasks would users delegate to AI agents?**

1. How often did users create tasks? number of tasks in database
2. How often did users create manual/autnomous tasks? check task.interaction_type
3. How often did users change the task type? TASK_EDITED (new_interaction_type, old_interaction_type difference)
4. Which tasks did users create the most? check task descriptions in database
5. How often did users created each type of trigger? TASK_CREATED task.advanced_settings.interaction_trigger in database

**RQ3: How do users interact with AI agents?**

1. Did users use agents of other collaborators and how often? AGENT_UPDATE (agent.author_id, user_id) to check who updated agent, TASK_CREATED (task.assignee_ids, user_id -> then check if agent from assignee_ids has author_id == user_id), TASK_EDITED (task.assignee_ids, user_id -> then check if agent from assignee_ids has author_id == user_id)
2. Did users use tasks of others? TASK_RUN/TASK_SHORTCUT_RUN for running (task.author_id, user_id)
3. Did users assigned agents to task or used autoselection? TASK_CREATED (task.assignee_ids)
4. How often did users open activity tab and specific task activity? AGENT_TASK_ACTIVITY_VIEW, AGENT_TASK_ACTIVITY_TASK_REVIEW
5. How often did users use comments to communicate with each other and AI? COMMENT_POST, REPLY_POST (check users field)
6. How often did users approve the suggestions? SUGGESTION_INSERT_AFTER, SUGGESTION_TAKE_OVER, card text in document text
7. Average comments history length? For each card check replies length
