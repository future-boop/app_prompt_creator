Lesson 2: Prompt Engineering & AI-Assisted Development

# **Learning Objectives**

By the end of this session, you'll be able to:  
   
·        Explain why context engineering matters more than prompt wordsmithing — and apply the distinction  
·        Write a production-quality system message (the behind-the-scenes instructions that tell the AI how to behave) with role, output format, and boundaries  
·        Use few-shot examples (showing the AI what you want instead of just describing it) and structured outputs (guaranteeing the AI returns data in a specific format, not free-form text) to control model behavior reliably  
·        Execute the 4-step pre-prompting workflow (Define → Database → Features/UI → Master Prompt) to go from idea to buildable spec — no technical background required  
·        Use vibe coding tools (Lovable) to turn a master prompt into a working application  
 

|  |  |
| :---- | :---- |
|  |  |

 

# **Context Engineering — The Real Game**

Consider two prompts for the same task:  
 

### **Prompt A (Vague):**

Build a tip calculator

 

### **Prompt B (Effective):**

   
Build a tip calculator with bill input, service quality dropdown,  
displays 15/18/20% options with totals, clean mobile UI, blue/white colors

   
Same goal. Completely different results. That gap is what prompt engineering is about — but the field has evolved significantly.

A lot of common "prompt engineering tips" are now outdated. "Act as a senior developer." "Take a deep breath before answering." These were tricks that worked with earlier models. With today's AI, they don't move the needle.

What actually matters now is the distinction between **prompt engineering** and **context engineering**:

·        **Prompt Engineering** \= crafting the instruction (the words you use)

·        **Context Engineering** \= curating everything the model sees (system message, examples, reference docs, conversation history, output format)

You can spend 30 minutes wordsmithing the perfect question. Or you can spend 30 seconds on a decent question — but include the right background information, the right examples, the right output format. A decent prompt with great context wins every single time.

Models got smarter — Claude 4.5, Gemini 3, GPT-5 understand instructions well. The exact wording of your prompt matters less than what information you include alongside it. **Stop optimizing words. Start optimizing information.**

# **The Fundamentals — Through the Context Engineering Lens**

### **1\.**  **Be Specific, Not Exhaustive**

|  |  |
| :---- | :---- |
|  |  |

 

Too Vague

"Make me a website"

   
Good         	"Portfolio website with hero, about, and contact form"

 

Too Detailed

"Create a website with a hero section using flexbox with justify-content center and…"

   
                    	Better        	"Portfolio website with centered hero, about section, contact form. Modern, minimal design."

 **Key insight:** Specify *what* you want — let AI figure out *how*.                                                                                                                                    	  
 

### **2\.**  **Front-Load Context**

   
Structure your prompts:  
   
CONTEXT: \[1 sentence about what this is for\] GOAL: \[What you're building\]  
KEY FEATURES: \[3-5 bullet points\] DESIGN: \[1 sentence on look/feel\]

 

### **3\.**  **Iterate, Don't Perfect**

You won't nail it first try. That's not failure — that's the process. Even experienced pros iterate. It's how AI-assisted building works.

The iteration cycle:  
   
1\. 	Start with a clear prompt (aim for 80% of what you want)  
2\. 	Generate  
3\.     Review the result  
4\.     Refine: "Change X to Y" or "Add Z feature"  
5\.     Repeat until you're happy with it  
 

|  |  |
| :---- | :---- |
|  |  |

 

# **AI-Assisted Learning**

The ability to learn with AI is the meta-skill that accelerates everything else in this course. Understanding it shapes how you approach every lesson.

### **The Old Way:**

Problem / Question  
↓  
Google Search  
↓  
Scan 10-20 Articles (half are outdated)  
↓  
Read Stack Overflow Threads (answers from 2019\)  
↓  
Parse Documentation (written for experts)  
↓  
Trial and Error  
↓  
Solution (after hours... or days)

 

### **The New Way:**

   
Problem / Question  
↓  
Ask AI with Context (Claude / ChatGPT)  
↓  
Get Synthesized Answer  
↓  
Ask Follow-up Questions  
↓  
Iterate and Refine  
↓  
Solution (within minutes)

 

## **Example 1: Learning n8n**

**Old Way:** Search documentation (generic, assumes prior knowledge) → watch a 45-minute tutorial (only 5 minutes relevant) → trial and error. Total: 2–3 hours.  
 

### **New Way:**

You: "I'm new to n8n. I want to build a workflow that sends a Slack message whenever someone submits a form. Walk me through this step-by-step."  
   
Claude: \[Provides tailored step-by-step guide for your exact use case\] You: "How do I handle errors if Slack is down?"  
Claude: \[Explains error handling specific to your workflow\]

   
Total time: 15 minutes.  
 

## **Example 2: Debugging**

**Old Way:** Google the error → find Stack Overflow answers from 2019 → try fixes that don't work with current versions → wait hours for a response. Total: hours to days.  
 

### **New Way:**

   
You: \[Paste error message \+ your code\]  
"This workflow is throwing an error. What's wrong and how do I fix it?" ChatGPT: \[Identifies the issue, explains WHY, provides the fixed code\] You: "Why did that error happen? I want to understand it."  
ChatGPT: \[Explains the underlying cause so you learn, not just copy-paste\]

   
Total time: 5 minutes.  
 

## **Why This Matters for Prompt Engineering**

The quality of your questions directly determines the quality of your answers. A vague question gets a vague answer. A specific question with context gets a precise, actionable answer.

The advantages of AI-assisted learning:  
   
·        **Instant synthesis** — no scanning 20 articles  
·        **Conversational clarification** — confused? Just ask a follow-up  
·        **Tailored to your context** — not generic documentation  
·        **No judgment** — ask "basic" questions freely, iterate without embarrassment  
·        **Built-in refinement** — each follow-up sharpens the answer  
 

|  |  |
| :---- | :---- |
|  |  |

 

# **System Messages, Examples & Structured Outputs**

## **System Messages: Your Primary Control Surface**

A system message is the behind-the-scenes instruction that tells the AI how to behave — before the user ever says anything. It's the most important part of any AI call in automation. Not the user prompt. The system message.  
   
A good system message does exactly three things:  
   
1\. 	**Defines role and constraints** — specific operational boundaries  
2\. 	**Specifies output format** — exactly what information comes back, and how it's structured  
3\. 	**Sets boundaries** — what to do with unexpected input Here's a real production system message for email classification: You are an email classifier for an e-commerce support team.  
TASK: Classify incoming emails into exactly one category and extract key fields.  
   
CATEGORIES:  
\-  order\_status: Questions about where an order is  
\-  return\_request: Customer wants to return something  
\-  product\_question: Questions about products before purchase  
\-  billing: Payment issues, refund requests, charge disputes  
\-  complaint: General complaints or negative feedback  
\-  other: Anything that doesn't fit above categories  
   
OUTPUT FORMAT (strict JSON):  
{  
"category": "\<category\>", "urgency": \<1-5\>,  
"customer\_name": "\<extracted or null\>", "order\_number": "\<extracted or null\>", "summary": "\<one sentence\>"  
}  
   
RULES:  
\-  Always return valid JSON. No markdown, no explanation.  
\-  Urgency 5 \= mentions legal action, regulatory complaint, or social media threat  
\-  Urgency 1 \= general inquiry with no time pressure  
\-  If you cannot determine a field, use null

   
A note on **JSON** (pronounced "jay-son") — it's the data format that apps use to talk to each other. Think of it like a standardized form: specific fields, specific values, always in the same structure. You'll see it constantly in automation.  
   
Notice what this system message is *not*: there's no "Act as a senior support engineer," no "Please think carefully." It's a clear specification. The model knows exactly what success looks like.

## **Structured Prompts: Use XML Tags or Headings**

When your prompt is longer than a paragraph, structure it. Use XML tags (especially with Claude) or markdown headings to separate instructions from data. XML tags are labels wrapped

in angle brackets — like \<task\> and \</task\> — that help the AI distinguish your instructions from the content it's working with.

\<task\>Extract action items from the meeting transcript.\</task\>  
\<format\>JSON array: {action, owner, deadline}\</format\>  
\<rules\>  
\-  Only include items with a clear owner  
\-  If no deadline mentioned, use null  
\</rules\>  
\<transcript\>{transcript\_text}\</transcript\>

   
Without structure, the model might treat parts of your document as instructions.  
 

## **Few-Shot Examples: The Fastest Lever**

If you want to change how a model behaves, forget writing more instructions. Show it examples. This is the single highest-return technique in prompt engineering.

Classify these customer messages:

Input: "I ordered a blue sweater but got a red one. I need the right one ASAP."  
Output: {"category": "return\_request", "urgency": 3, "summary": "Wrong item color received"}  
   
Input: "DO NOT CHARGE MY CARD AGAIN. I am contacting my lawyer."  
Output: {"category": "billing", "urgency": 5, "summary": "Disputed charge, legal threat"}  
   
Input: "Hey, do you guys have the wireless headphones in black?"  
Output: {"category": "product\_question", "urgency": 1, "summary": "Product color availability inquiry"}  
   
Now classify this message:  
Input: "{actual\_customer\_message}"

   
Three examples — that's usually enough. The model now understands your classification scheme, your urgency scale, and your summary style better than any written instruction could convey. Start with 2–3 examples; more than 5 uses up context space for diminishing returns.  
 

## **Structured Outputs: Getting Reliable Data Back**

In automation, you need machine-readable output — always. Both OpenAI and Anthropic offer structured output modes at the API level (the programming interface that lets apps communicate with AI models), meaning near-perfect adherence to your specified format. Both are available through n8n's AI nodes.  
   
**Practical rule: always use structured outputs in automation workflows.** Never rely on "just return JSON please" in a prompt. It works 95% of the time — which means it breaks several times a day when you're running workflows at scale.  
 

## **Context Window Strategy: Stuff vs Retrieve**

A **context window** is how much information the AI can "see" at once — think of it as the AI's working memory. A **token** is roughly ¾ of a word, so 200K tokens is about 150,000 words (2–3 novels).

In 2026, if your total context is under 200K tokens, just include it all. Don't build a complex retrieval system. Prompt caching makes this economical: a large context costs about $0.30 on the first call, then $0.03 on repeat calls — 90% savings. Only invest in more complex retrieval setups when your knowledge base gets truly massive.

|  |  |
| :---- | :---- |
|  |  |

 

# **Vibe Coding Tools**

"Vibe coding" is using AI to build actual applications from natural language descriptions. The workflow:  
1\. 	Write a PRD (Product Requirements Document) — which is essentially what the 4-step pre-prompt produces  
2\.     Feed it to an AI-powered builder  
3\.     Get a functional application  
4\.     Iterate with plain English  
 

## **The Tools**

**Lovable** — Takes a PRD and generates a full-stack web app. Best for dashboards, internal tools, admin panels.

**Bolt (StackBlitz)** — Similar concept, runs in the browser. Great for quick prototypes and client demos.

**Cursor** — Code editor with deep AI integration. Best when working inside an existing codebase.

### **When to vibe code vs. when NOT to:**

   
 Internal tools, dashboards, prototypes, MVPs, admin interfaces

   
 Complex business logic, strict security requirements, performance-critical systems

   
The sweet spot for automation developers: build front-end interfaces using vibe coding. Build the actual automation logic in n8n.

In Lesson 4, you'll go beyond vibe coding into agentic coding — AI that doesn't just build on command, but reads your codebase, runs tests, and iterates on its own. For now, focus on mastering the pre-prompting workflow.

 

# **The 4-Step Pre-Prompting Workflow**

Pre-prompting means using AI to *prepare* before you build — like getting blueprints before construction. Most beginners jump straight into a building tool and wonder why results are messy. This workflow is different, and anyone can follow it.  
 

### **The concept:**

·        Use Claude/ChatGPT to think through your project first  
·        Define requirements clearly  
·        Design data structure  
·        Create a master prompt  
·        *Then* go to Lovable  
 

### **Why it works:**

   
·        Catches problems before building  
·        Creates documentation automatically  
·        Makes iterations faster  
·        Results in cleaner, more maintainable code  
 

## **Step 1: Define the Project**

Single prompt to start — fill in the bracket:  
   
"I'm building a \[Marketing Agency Dashboard / AI Service Platform Dashboard\] for a course project. Help me define:  
\-  What problem it solves  
\-  Who uses it  
\-  Must-have features for MVP  
\-  What to skip for now"

   
One prompt, and you have clarity. This takes 30 seconds. Now you're not guessing what to build.  
 

## **Step 2: Design Data Structure**

"Design a simple data structure for this. ONE main entity for MVP. Include: entity name, fields with types, and 5-6 rows of sample data.  
We'll use hard-coded data for now and connect a real database in a later lesson. Consider that I'll add \[future features\] in later modules."

   
A **data structure** is a blueprint for how your information is organized — what you're storing and how it's structured. Think of it like designing a spreadsheet: you decide the columns before you start entering rows.  
 

### **Why database first?**

·        Everything else depends on data structure  
·        Mistakes here cascade to the entire app  
·        Much harder to fix later  
·        AI helps catch structural issues early Example output:  
TABLE: clients FIELDS:  
\-  id: uuid (auto)  
\-  name: text (required)  
\-  industry: text (required)  
\-  contact\_email: text (required, unique)  
\-  phone: text (optional)  
\-  status: text (Active/Inactive/Prospect)  
\-  created\_at: timestamp (auto)  
\-  updated\_at: timestamp (auto)

 

### **Common mistake to avoid:**

   
·         "Give me a complete database design with 10 tables"

·         "One table for MVP, designed to expand later"

 

## **Step 3: Define Features & UI**

"For this dashboard, list:  
MUST HAVE: Core CRUD features  
UI LAYOUT: Main sections and components DESIGN: Color scheme and style  
Keep it simple \- this is MVP."

   
**CRUD** means the four basic things you do with data: Create, Read, Update, Delete. If you can add a contact, view it, edit it, and remove it — that's CRUD.

This step becomes your checklist. When you prompt Lovable, you'll reference this. When testing, you verify each item.  
 

## **Step 4: Generate the Master Lovable Prompt**

"Based on everything we discussed (problem, database, features, UI), write ONE comprehensive prompt I can give Lovable to build this. Include all requirements but keep it concise."

   
The AI compiles all your previous thinking into one ready-to-use prompt you can copy directly into Lovable.

### **Example output:**

   
Build a Marketing Agency Dashboard with these specs: DATA (hard-coded for now):

Entity 'clients' with fields: id, name, industry, contact\_email, phone, status (Active/Inactive/Prospect), created\_at, updated\_at Include 5-6 sample rows of realistic data in the app  
   
FEATURES:  
\-  Display clients in responsive grid  
\-  Add/Edit client via modal form (name, industry, email, phone, status)  
\-  Delete with confirmation  
\-  Filter by status dropdown  
\-  Real-time search by name  
\-  Stats cards: Total/Active/Prospect counts  
   
UI:  
\-  Top nav: "Agency Dashboard" title, "Add Client" button  
\-  Left sidebar: Filter dropdown, search bar  
\-  Main area: Stats row, client grid below  
\-  Each card shows: name, industry, email, status badge  
\-  Colors: Primary blue (\#2563EB), white cards with shadows  
\-  Mobile: Stack grid to single column, move sidebar to top  
   
TECHNICAL:  
\-  React with TypeScript  
\-  Hard-coded sample data (no external database)  
\-  Form validation (email format, required fields)  
\-  Loading states, error handling  
\-  Success toasts for actions

   
Four prompts. That's all it took. Now you have a complete blueprint. Compare this to jumping straight into Lovable with "build a dashboard" — the pre-prompting approach consistently produces better, faster results.  
 

|  |  |
| :---- | :---- |
|  |  |

 

# **Homework Assignment**

## **Choose Your Path**

·        Marketing Agency Dashboard, OR  
·        AI Service Platform Dashboard  
 

## **The 4-Prompt Workflow**

Use these copy-paste-ready prompts (fill in the brackets):  
   
Prompt 1: "I'm building a \[your choice\] for my course. Help me define: problem, users, must-have features, what to skip"

Prompt 2: "Design ONE table schema for this. Include fields, types, sample data. Consider future expansion to projects/services"  
   
Prompt 3: "List MUST HAVE features, UI layout sections, and design preferences. Keep it MVP-focused"

Prompt 4: "Write a comprehensive but concise Lovable prompt based on everything above"

 

## **Build in Lovable**

·        Paste your master prompt (it includes hard-coded sample data)  
·        Test all features  
·        Refine as needed  
 

## **Document**

·        Save all 4 pre-prompts and responses  
·        Write a reflection on the process  
·        Screenshot key features  
 

## **What to Submit**

1\. 	Pre-Prompting Document (all 4 prompts \+ AI responses)  
2\. 	Data Structure  
3\.     Working Application (link)  
4\.     Reflection (what worked, what didn't, what you'd change)  
 

## **Time Estimates**

·        Pre-prompting: 60–90 minutes (most important part)  
·        Building in Lovable: 30–60 minutes  
·        Testing & refinement: 30 minutes  
·        Documentation: 30 minutes  
·        **Total: 2.5–3.5 hours**  
 

## **Bonus Challenge**

Try writing a system message for an automation task relevant to your work — use the email classifier format from today as a template. This will be used in the n8n lesson.

|  |  |
| :---- | :---- |
|  |  |

 

# **Lesson 3 Preview**

Next session covers n8n in depth — nodes, expressions, error handling, APIs, webhooks, and authentication. The platform mastery that makes everything from today actually work in production.  
 

|  |  |
| :---- | :---- |
|  |  |

 

# **Appendix: The 4-Prompt Quick Reference**

### **PROMPT 1: Define Project**

   
"I'm building \[type\] for \[purpose\]. Help me define:  
problem, users, must-have features, what to skip"

 

### **PROMPT 2: Design Data Structure**

   
"Design ONE main entity for this. Include fields,  
types, and 5-6 rows of sample data. Hard-coded for now. Consider future \[features\]"

 

### **PROMPT 3: Features & UI**

   
"List MUST HAVE features, UI layout sections, design preferences. Keep MVP-focused"

 

### **PROMPT 4: Master Lovable Prompt**

   
"Write a comprehensive but concise Lovable prompt based on everything above"

|  |  |
| :---- | :---- |
|  |  |

 

# **Best Practices & Pre-Prompting Checklist**

## **The Do's**

 Start with one clear prompt per step

   
 Build on previous responses (reference earlier answers)

   
 Ask "why" when AI makes suggestions — understanding beats copying  Keep master prompt under 400 words

 Test data structure before building UI

   
 Use structured outputs in automation workflows

   
 Show examples instead of writing more instructions

 

## **The Don'ts**

 Write 1000-word prompts with every detail  Skip data structure planning

 Try to perfect everything in one prompt

 Jump to Lovable without pre-prompting

   
 Rely on "please return JSON" — use structured output schemas  Use "Act as..." prompt tricks from 2023

 Forget to save your prompts (you'll reuse patterns)

## **The Pre-Prompting Checklist**

Before going to Lovable, make sure you have:  
   
·        \[ \] Clear problem statement  
·        \[ \] Database schema documented  
·        \[ \] Feature list prioritized  
·        \[ \] UI preferences defined  
·        \[ \] Master prompt generated  
   
If you skip any step, stop and pre-prompt it.  
