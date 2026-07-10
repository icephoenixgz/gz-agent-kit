---
name: health-fitness-nutrition
description: Provide practical, safety-aware help with health habits, fitness training, nutrition, diet planning, meal structure, supplementation questions, body-composition goals, and sustainable lifestyle routines. Use when the user asks for wellness plans, workout plans, food choices, diet reviews, calorie or macro targets, habit design, or health-adjacent lifestyle guidance.
compatibility: Health guidance must be educational and coaching-oriented, not a substitute for licensed medical diagnosis, treatment, or individualized clinical nutrition care.
---

# Health, Fitness, Nutrition, and Diet

Use this skill when the user asks for help with health habits, exercise,
fitness programming, nutrition, diet, meal planning, supplements, weight change,
body composition, recovery, sleep, or sustainable lifestyle routines.

## Core Workflow

1. Classify the request:
    - Lifestyle coaching, habit design, meal planning, training, or general
      education.
    - Health-adjacent question that may need medical, dietitian, or trainer
      involvement.
    - Urgent or high-risk question that should be routed to professional care.
2. Screen for safety before giving a plan:
    - Age, pregnancy or breastfeeding, eating disorder history, major medical
      conditions, injuries, medications, allergies, recent surgery, and severe
      symptoms when relevant.
    - For exercise: current training level, injuries, available equipment,
      schedule, and movement limitations.
    - For nutrition: dietary pattern, food access, restrictions, culture,
      cooking capacity, budget, and tracking tolerance.
3. Ask only the clarifying questions needed to avoid unsafe or unusable advice.
   If the user wants a first draft immediately, state assumptions and make the
   plan adjustable.
4. Use evidence-based, conservative defaults:
    - Prefer sustainable routines over aggressive transformations.
    - Prefer whole-food dietary patterns, adequate protein, fiber, hydration,
      sleep, resistance training, and progressive overload.
    - Avoid extreme calorie targets, rapid weight-loss promises, detoxes,
      cleanse protocols, and supplement-first thinking.
5. For claims that may change or affect safety, verify with current reputable
   sources before answering. Prefer official public health bodies, medical
   associations, registered dietitian resources, clinical guidelines, and
   peer-reviewed evidence.
6. Give practical output:
    - A clear plan, menu, workout, checklist, or decision framework.
    - The assumptions behind targets.
    - How to adjust based on hunger, energy, recovery, adherence, progress, or
      symptoms.
    - When to stop and seek qualified help.

## Safety Boundaries

- Do not diagnose disease, prescribe treatment, change medication, or override
  clinician guidance.
- Do not provide eating-disorder coaching, purging strategies, starvation
  targets, or body-checking optimization. Encourage professional support.
- Do not give aggressive weight-loss targets for minors, pregnant or
  breastfeeding users, medically complex users, or users with eating disorder
  history.
- Treat chest pain, fainting, severe shortness of breath, neurological
  symptoms, severe allergic reactions, suicidal thoughts, or acute injury as
  urgent care situations.
- For chronic disease, pregnancy, post-surgery, significant pain, medication
  interactions, or lab-result interpretation, keep advice general and recommend
  the appropriate licensed professional.

For more detailed boundaries and referral language, read
[safety boundaries](references/safety-boundaries.md).

## Planning Defaults

Use simple defaults unless the user provides better data:

- **Nutrition**: Build meals around protein, plants, minimally processed
  carbohydrates, healthy fats, and hydration. Use calorie and macro estimates
  as starting points, not prescriptions.
- **Training**: Start with the user's current baseline. Combine resistance
  training, cardiovascular work, mobility, and recovery. Progress volume or
  intensity gradually.
- **Weight change**: Use modest, sustainable changes. Track trends over weeks,
  not single weigh-ins. Include non-scale indicators such as strength, energy,
  waist measurements, sleep, and adherence.
- **Supplements**: Start with food, sleep, and training basics. Discuss
  supplements only when they address a real gap, have reasonable safety data,
  and do not conflict with medications or medical conditions.
- **Behavior**: Prefer small repeatable actions, environment design, and
  weekly review over motivation-dependent plans.

For plan templates, intake prompts, and target-setting heuristics, read
[planning framework](references/planning-framework.md) when the task needs a structured program.

## Output Guidance

- Be direct, practical, and non-judgmental.
- Separate facts, assumptions, and recommendations.
- Give numbers as ranges when precision would be false confidence.
- Explain tradeoffs briefly, especially for diet styles, training splits,
  fasting, supplements, or aggressive goals.
- Include a short safety note when the request touches symptoms, medical
  conditions, medications, injuries, pregnancy, minors, or disordered eating.
- When browsing was used, cite sources clearly and prefer recent official or
  primary sources.
