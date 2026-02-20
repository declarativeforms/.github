## 1. Objective

Create a complete, structured set of product documentation pages that clearly explain the product, demonstrate its value, and encourage adoption.

The documentation must:

* Be **clear, concise, and intuitive**
* Be **structured for readability and usability**
* Emphasize **ease of use and developer workflow advantages**
* Reflect a **modern, declarative, LLM-friendly approach**
* Be grounded only in **verifiable information from provided sources**

---

## 2. Product Context (Facts Only)

* The product is a **form-building system**
* Unlike traditional tools (e.g. Google Forms, Jotform, Tally), it:

  * Does **not rely on a UI-based builder workflow**
  * Uses a **declarative approach (code-based)**
  * Aligns with **modern developer workflows (e.g. Git-based workflows)**
* Key advantages to highlight (only where supported by repo analysis):

  * Works without traditional UI friction
  * Enables versioning and change tracking
  * Supports structured workflows similar to software development

---

## 3. Source Material

The agent MUST analyze the following repositories before writing:

* `/Users/barenderasmus/development/examples/api`
* `/Users/barenderasmus/development/examples/core`
* `/Users/barenderasmus/development/examples/examples`

### Requirements:

* Extract **only factual capabilities and patterns**
* Do **not infer features that are not explicitly present**
* Use examples grounded in actual repo structures

---

## 4. Required Output Pages

The agent must generate the following documentation pages:

### 4.1 Introduction

Purpose:

* First-touch page for users

Must include:

* What the product is
* What problem it solves
* Why it is different from traditional tools
* Core value proposition
* High-level explanation of how it works

---

### 4.2 Quickstart

Purpose:

* Provide the fastest way to understand and use the product

Requirements:

* Minimal explanation
* One simple working example
* Demonstrates:

  * Core concept
  * Ease of use
* Avoid complexity

---

### 4.3 Guides

#### 4.3.1 Multiple Sections

* Demonstrate adding more than one section
* Keep scope limited strictly to:

  * Adding and structuring multiple sections
* Avoid introducing unrelated features

#### 4.3.2 Conditional Routing of Sections

* Focus on the `next` property
* Cover:

  * All supported ways `next` can be used
* Must include:

  * Clear examples
  * Explanation of behavior

---

### 4.4 Reference

Purpose:

* Technical, complete, and precise
* No marketing language

General rules:

* Use **YAML examples only**
* Do **not use tables**
* Keep descriptions minimal and exact

#### Sections:

* Short Text Field
* Long Text Field

Each must:

* Show full configuration possibilities
* Be example-driven

---

## 5. Writing Process (MANDATORY)

The agent must follow this exact workflow:

### Step 1: Task Analysis

* Break down the task into components
* Identify missing information
* Ask **comprehensive clarifying questions** before proceeding

---

### Step 2: Define Writing Style

Explicitly define:

* Tone (e.g. technical, friendly, minimal, etc.)
* Voice (e.g. authoritative, instructional)
* Level of detail

This must be done **before writing begins**

---

### Step 3: Generate 5 Distinct Angles

Create **5 different approaches** to positioning the documentation.

Each angle must differ in:

* Framing of the product
* Emphasis (e.g. developer-first, speed, flexibility, etc.)
* Narrative style

---

### Step 4: Evaluate Angles

Analyze all 5 angles based on:

* Clarity
* Accuracy
* Appeal
* Alignment with product reality

Select **1 best approach**

---

### Step 5: Draft Documentation

* Write a **complete first draft** for all pages
* Prioritize completeness over perfection

---

### Step 6: Iterative Refinement

Perform multiple review cycles:

* Improve clarity
* Remove ambiguity
* Tighten structure
* Ensure consistency across pages

Repeat until:

* Documentation is **clear, cohesive, and polished**

---

## 6. Constraints

The agent MUST:

* ❌ Not invent features

* ❌ Not assume behavior not present in repos

* ❌ Not use vague or generic explanations

* ❌ Not skip the structured workflow

* ✅ Only use verifiable facts

* ✅ Keep explanations grounded in examples

* ✅ Optimize for clarity and usability

* ✅ Maintain consistent structure

---

## 7. Output Requirements

The final output must:

* Include all pages listed
* Follow a **clean, structured format**
* Be ready for direct use in documentation
* Reflect the selected best angle consistently across all pages

---

## 8. Success Criteria

The output is successful if:

* A developer can understand the product **without prior context**
* The Quickstart can be followed **without confusion**
* The Guides clearly demonstrate specific features
* The Reference is **precise and exhaustive**
* The documentation clearly communicates **why this product is better than UI-based alternatives**