BRD | Cost Control

Background & Problem

The fundamental barrier to Enterprise AI adoption is not performance, but unexpected variable costs. In a traditional SaaS model, costs are predictable (servers, seats). In the era of agentic AI a single recursive loop or a spiral caused by hallucination creates a black hole straight from the customer's bank account to the LLM provider. This paralyzes our customers from scaling their agents. Our customers are afraid to scale quickly because they fear the bill they might receive due to a singular mistake. There is currently no kill-switch in the industry that acts as fast as the agent thinks, before our customer already incurs the financial hit.

Current solutions fail due to:

- Latency of Information: LLM provider alerts often have major delays. By the time that a usage alert does out, a thousand dollar bill has already shown up for the customer to pay.
- Lack of Granularity: Existing tools provide account-level spending. They cannot distinguish between a premium user and a free tier user, forcing them to set limits that may not make sense to everyone.

Customer Story

Risks

We have received many rejection responses from CTOs at seed-staged companies suggesting that their LLM usage & volume’s too low to justify 3rd-party cost control tools. Also, many suggested that they’d build cost control internally since it’s critical and not hard to build.

Risk: As companies scale their LLM volume and usage, they tend to build cost control internally more since it’s more controlled, flexible, and secure.

Opportunity: For companies with a lot of LLM volume and usage currently, the need for cost control is imminent therefore might explore 3rd-party solutions that can place speed bumps immediately. But this tool needs to be mature, reliable, and low-risk.

Based on market feedback, cost control is a strong feature for companies with high-usage, high-volume LLMs that see immediate ROI. However, it may not serve as a compelling go-to-market product for seed-stage companies, as it fails to address their top concerns (e.g. sales, raising money, product traction).

Solution Proposal

Our solution leverages the raw data that we collect to build a Budget Enforcement system. We move from observing spending to governing it. By collecting token consumptions and having real-time model cost, we can accurately trigger actions with minimal latency to stop the spending before the next API call is made.

We have four actions:

Notify: We have soft limits that will send an email to our customer whenever a soft limit is hit in a certain Budget. Automatically created to trigger at 80% and 100% of the budget.

Throttle: We can artificially introduce waiting states between agent actions and LLM API calls to slow the burn rate while still allowing processes to be completed. This throttle can be set by Customers so they can decide how much they want to affect their own product experience.

Degrade: When a Budget is hit, the degrade action would switch the model to a less expensive model from the same provider. Our Customer would select a fallback model, which allows for minimal product experience change while still allowing Customers to save.

Block: This is the most severe action, causing the process to immediately be halted. This is the most effective cost cutting action and stops the bleed right away.

We have a granular categorization system that allows Customers to attach budgets to their customers, agents, features, their own custom tags, as well having a global budget. This transforms their LLM bill from a single usage number into a granular balance sheet allowing Customers to know exactly where their money is going.

Docs & SDKs

Docs: https://docs.adenhq.com/sdk/typescript/cost-control
SDKs: https://github.com/adenhq/aden-analytics-agent

Product Design & Prototyping

Lovable: https://lovable.dev/projects/6347456c-9f0b-4959-9a06-e93169c55613

Testing

For a completed MVP, these criteria must be met during testing:
Enforcement Latency: The decision made by our Monarch must return an Allow/Block in < 100ms when usage >= 80% of budget to avoid degrading the user experience during normal operation
Overage: The total overage that we allow should not exceed 5% of the total budget

Testing Scenarios:

Set a Budget and calls made in succession until the agent is blocked locally
Two agents sharing the same budget hitting the limit simultaneously should not exceed budget
Budget hitting 100% with Degrade option should swap models successfully without crashing the agent
Budget hitting 80% should trigger the email within 30s
A $10 Customer budget should stop the agent even if the global budget is $100
If agent is mid-sentence when budget hits $0, we should still allow agent to finish before action
If our Price Table API is down, our system should fail open, not blocking user’s agent calls

Technical Design & Scope

https://www.notion.so/adenhq/25a70fed5af280369d9ceb59ff97c309?v=25a70fed5af280a3b25e000c55ce46d5&p=2d570fed5af280198457fd07f30e2d0f&pm=s
