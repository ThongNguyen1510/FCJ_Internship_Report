---
title: "Event 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# FCAJ Community Day - Conference Call

### Event Information
*   **Event Name:** FCAJ Community Day - Conference Call
*   **Date & Time:** Saturday, May 23, 9:00 AM - 12:00 PM (GMT+7)
*   **Location:** Bitexco Financial Tower, Ho Chi Minh City (Floor 36)
*   **Objective:** Deep dive into context-driven AI, hackathon execution, edge cloud infrastructure, LLM determinism limits, and multi-agent systems for enterprise applications.

---

### Detailed Agenda & Highlights

#### ☁️ 8:30 - 9:00 AM | Check-in & Settle in
*   Attendees gathered at Floor 36 of Bitexco Financial Tower, networking and setting up local environments.

#### ☁️ 09:00 - 09:30 AM | Context Is Everything: Making AI Actually Work for You
*   **Defining Context:** Explored why AI models generate hallucinations without adequate context and what "true context" means for transformer architectures.
*   **Second AI Brain:** Discussed the evolution from stateless prompt engineering to vector-based semantic memory.
*   **Practical Mindsets:** Actionable strategies on how adding context (via RAG or specialized metadata) improves AI reasoning accuracy.
*   **Q&A:** Guidance for students on how to build context-aware AI projects.

#### ☁️ 09:30 - 10:00 AM | 36 hrs with LotusHacks – Building UTMorpho from Idea to Reality
*   **Hackathon Overview:** Shared the journey of joining **LotusHacks**, a fast-paced 36-hour hackathon.
*   **The Brainstorming Journey:** Moving from zero to a structured idea, defining the target problem, and scoping **UTMorpho**.
*   **36-Hour Sprint:** Insights into rapid prototype development under intense time constraints, managing team blockages, and managing failures.
*   **Demo & Future Work:** A live demonstration of the UTMorpho MVP, followed by key technical lessons and next-phase scaling plans.

#### ☁️ 10:00 - 10:40 AM | From Edge To Origin: CloudFront as Your Foundation
*   **Amazon CloudFront Workloads:** Detailed configuration strategies for hosting static single-page apps (SPAs) and secure, dynamic backend APIs globally.
*   **Edge Optimization:** Using CloudFront caching, Gzip/Brotli compression, and custom header forwarding to minimize API response times.
*   **Edge Security & Performance:** Implementing AWS Shield and AWS WAF at the edge to block malicious traffic before it reaches the origin.

#### ☁️ 10:40 - 10:55 AM | Friendly AI Assistant with Amazon Quick
*   **Quick Chat Agent:** Interactive natural language interfaces that allow users to query databases and extract analytics in real time.
*   **Quick Flows:** Build complex automated workflows using natural language commands, removing the need for manual backend coding.
*   **Quick Spaces:** Collaborative shared hubs that aggregate individual insights into team-wide knowledge repositories.
*   **Quick Sight:** Transform raw business metrics into charts and dashboards using conversational AI instructions.

#### ☕ 10:55 - 11:00 AM | Break

#### ☁️ 11:00 - 11:30 AM | Non-Determinism of "Deterministic" LLM Settings
*   **Token Selection Logic:** How foundation models predict the next token based on probability distributions.
*   **The Determinism Myth:** Clarified that setting `Temperature=0` does not guarantee identical outputs in production systems.
*   **Inference Realities:** Analyzed how hardware-level inference optimizations (GPU floating-point math, thread scheduling, and batching) induce minor variances in token probabilities.
*   **Mitigation Strategies:** Best practices for handling non-determinism using structured output validation (e.g., JSON schemas) and retry loops.

#### ☁️ 11:30 AM - 12:00 PM | Enterprise Multi-Agent System: Startup Credit Scoring
*   **The Problem:** The disconnect between rigid, historical banking metrics and the dynamic data patterns of high-growth startups.
*   **Single Agent vs. Multi-Agent:** Discussed why single-agent setups fail in complex regulatory domains due to context limitations.
*   **Virtual Credit Committee:** Presented a multi-agent architecture where distinct specialized agents (Analyst, Risk Officer, Compliance Auditor) collaborate to evaluate credit profiles.
*   **Compliance & ROI:** Implementing validation guardrails to ensure regulatory compliance, alongside a deployment roadmap.

---

### Key Takeaways
1.  **Context is King:** Prompting alone is insufficient; production AI systems must use retrieval architectures (like RAG) to supply domain context.
2.  **Edge Infrastructure:** Using CloudFront as a front-line defense reduces origin server load and increases security posture.
3.  **LLM Variances:** System engineers must design LLM workflows assuming outputs are non-deterministic, using validation parsers to enforce structure.
4.  **Multi-Agent Coordination:** Complex decision-making workflows (like credit underwriting) are best solved by breaking tasks down among multiple specialized AI agents.

### Applying to Work
*   **Monitoring Design:** Apply CloudFront edge caching configurations to optimize API delivery for telemetry backends.
*   **AI Integration:** Use structured JSON outputs and validate response formatting when writing AI-assisted monitoring tools.
*   **Workflow Automation:** Utilize multi-agent blueprints to model complex cloud alert classifications.
