---
title: "Comprehensive Assessment of Jailbreak Attacks Against LLMs"
---

# Overview

<div align="center">
  <img src="https://github.com/Junjie-Chu/Best_Jailbreak_Way_Public/assets/65893273/42ea7acf-1aa4-46b3-9aeb-de9b614f8b4b" alt="Overview_JB_thick" width="55%">
</div>

# Abstract
*Jailbreak attacks* aim to bypass the safeguards of LLMs.
While researchers have studied different jailbreak attacks in depth, they have done so in isolation - either with unaligned experiment settings or comparing a limited range of methods.
To fill this gap, we present the first large-scale measurement of various jailbreak attack methods. 
We collect 14 cutting-edge jailbreak methods and establish a jailbreak attack taxonomy.
We then conduct a unified and impartial assessment of attack effectiveness based on six popular censored LLMs and 160 questions from 16 violation categories.
Our extensive experimental results demonstrate that all the jailbreak attacks have a powerful effect on the LLMs.
The optimized-based jailbreak attacks consistently achieve the best attack performance, as well as exhibit robustness across different LLMs.
Some jailbreak prompts available from the Internet can also achieve high attack success rates on many LLMs, such as Vicuna, ChatGLM3, GPT-3.5, and PaLM2. 
Despite the claims from many organizations regarding the coverage of violation categories in their policies, the attack success rates from these categories remain high, indicating the challenges of effectively aligning LLM policies and countering jailbreak attacks.
Furthermore, we conduct a comprehensive ablation study to analyze different aspects of jailbreak attack performance.
Based on the experimental results, we discuss the trade-off between attack performance and efficiency. 
We also show that the transferability of the jailbreak prompts is still viable, becoming an option for black-box models.
Results of our longitudinal test on continuously updated LLMs show good attack stability over time of optimization-based methods.
Additionally, we test jailbreak attacks under four advanced external defenses and find none of the defenses could mitigate the jailbreak attacks entirely.
We hope our study can provide insights for future research on jailbreak attacks and serve as a benchmark tool for researchers and practitioners to evaluate them.

# Jailbreak Taxonomy

| Jailbreak Taxonomy |     Jailbreak Method    | Require White-Box Access? | Modify the Original Question?  |
|:------------------:|:-----------------------:|:-------------------------:|:------------------------------:|
|     Human-Based    |           AIM           |             ✗             |                ✓               |
|     Human-Based    |       Devmoderanti      |             ✗             |                ✓               |
|     Human-Based    |        Devmodev2        |             ✗             |                ✓               |
|  Obfuscation-Based |          Base64         |             ✗             |                ✓               |
|  Obfuscation-Based |       Combination       |             ✗             |                ✓               |
|  Obfuscation-Based |           Zulu          |             ✗             |                ✓               |
| Optimization-Based |         AutoDAN         |             ✓             |                ✓               |
| Optimization-Based |           GCG           |             ✓             |                ✓               |
| Optimization-Based |           COLD          |             ✓             |                ✓               |
| Optimization-Based |         GPTfuzz         |             ✗             |                ✓               |
| Optimization-Based |           PAIR          |             ✗             |                ✓               |
| Optimization-Based |           TAP           |             ✗             |                ✓               |
| Optimization-Based |        Masterkey        |             ✗             |                ✓               |
|   Parameter-Based  | Generation Exploitation |             ✓             |                ✗               |

# Unified Usage Policy

here

# Leaderboard

here

# Ablation Study

here

## Time
## Token

# Defenses

here
