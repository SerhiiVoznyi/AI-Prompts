Image 1

Question:
Your extraction pipeline processes contracts that frequently include amendments. When a contract contains both original terms and later amendments (e.g., original clause specifies "30-day payment terms" while Amendment 1 changes this to "45 days"), the model inconsistently extracts one value or the other with no indication of which applies. What’s the most effective approach to improve extraction accuracy for documents with amendments?

Options:
A. Preprocess documents with a classifier that identifies and removes superseded sections before the main extraction step.
B. Redesign the schema so amended fields capture multiple values, each with source location and effective date.
C. Implement post-extraction validation using pattern matching to detect amendments and flag those extractions for manual review.
D. Add prompt instructions to always extract the most recent amendment value and ignore superseded original terms.

Image 2

Question:
After the web search agent finds 25 sources (120K tokens of raw content), the document analysis agent extracts key insights (15K tokens), and the synthesis agent produces a coherent narrative draft (3K tokens), the coordinator must pass context to the report generation agent for the final output with proper source citations. What context-passing strategy provides the best balance of completeness and efficiency?

Options:
A. Pass a condensed summary of all prior stages that preserves the main findings and attributes them to sources by name only.
B. Pass the synthesis draft along with a structured source index that maps key claims to their source URLs and relevant excerpts.
C. Pass the full accumulated context from all prior agents.
D. Pass only the synthesis draft and have a separate post-processing pipeline match claims to sources and insert citations after the report is generated.

Image 3

Question:
Users report that final reports sometimes lack depth on specific subtopics. Investigation shows that the document analysis agent frequently identifies gaps—for instance, noting "the retrieved sources discuss API authentication but lack details on token refresh patterns"—but under the current strict pipeline, this insight isn’t actionable since search has already completed. What’s the most effective architectural change?

Options:
A. Have the synthesis agent attach confidence scores to each section and flag areas with insufficient coverage for manual review.
B. Have the coordinator review analysis output for gap indicators and re-invoke search with gap-informed queries when gaps are detected.
C. Have the analysis agent report specific gaps to the coordinator, which triggers targeted searches and re-invokes analysis until sufficient.
D. Add a research planning agent before the search phase that decomposes topics into specific sub-questions.

Image 4

Question:
After the web search and document analysis subagents complete their tasks, the coordinator needs to spawn the synthesis subagent to synthesize the findings. What is the correct approach for providing the synthesis subagent with the information it needs?

Options:
A. Pass reference identifiers and configure the subagent with read access to a shared memory store where other subagents deposited their results.
B. Include the complete findings from both subagents directly in the synthesis subagent's prompt.
C. Spawn the subagent with only a brief task description, relying on automatic context inheritance from the coordinator.
D. Provide the subagent with tool definitions that allow it to request outputs from other subagents via callbacks.

Image 5

Question:
The synthesis agent receives summarized findings from the web search and document analysis agents, then passes a consolidated summary to the report generator. During testing, you discover the generated reports make factual claims without proper citations—the report generator cannot attribute statements to their original sources because that metadata was lost during the summarization steps. What’s the most effective approach to ensure proper source attribution in the final reports?

Options:
A. Have each agent output structured data separating content summaries from source metadata (URLs, document names, page numbers).
B. Skip summarization and pass full raw outputs from web search and document analysis directly to the report generator.
C. Instruct the synthesis agent to embed source references inline within its summary text using a consistent citation format.
D. Have the report generator query the web search agent to re-locate sources for claims in the final report.

Image 6

Question:
The synthesis agent completes its initial pass but flags that three key research questions remain unanswered because the web search and document analysis agents didn’t find relevant information on those specific subtopics. The coordinator currently proceeds directly to report generation, producing reports with incomplete coverage. What change would most effectively improve research completeness?

Options:
A. Give the synthesis agent direct access to web search tools so it can autonomously fill knowledge gaps without returning control to the coordinator.
B. Have the coordinator evaluate synthesis output for gaps, then re-delegate to web search and document analysis with targeted queries before invoking synthesis again.
C. Have the report generation agent note which research questions couldn’t be answered, so users understand the limitations of the final output.
D. Increase the initial breadth of queries sent to web search and document analysis to reduce the probability of missing relevant information.

Image 7

Question:
The document analysis agent has a single analyze_document tool that takes a document and a free-text instruction parameter. During evaluation, requests like "extract the key financial metrics" often return narrative summaries, while "summarize the methodology" sometimes returns raw data tables. The synthesis agent reports that 35% of analysis results require re-requests with clarified instructions. What’s the most effective way to improve reliability?

Options:
A. Keep the single tool but add an analysis_type enum parameter requiring explicit selection between extraction, summarization, and verification modes
B. Have the coordinator pre-classify each analysis request before passing instructions to the document analysis agent
C. Enhance the tool description with detailed examples showing how different instruction phrasings should map to different output formats
D. Split the generic tool into purpose-specific tools—extract_data_points, summarize_content, verify_claim_against_source—each with defined input/output contracts

Image 8

Question:
In production, final reports frequently contain claims without proper source attribution. Investigation shows that while the web search and document analysis agents correctly attach citations to their outputs, the synthesis agent loses track of which sources support which conclusions when combining findings. What’s the most effective architectural change?

Options:
A. Add a verification step where the report generator uses semantic similarity matching against original sources to reconstruct which claims came from which documents.
B. Have the coordinator inject source identifier prefixes into text before each handoff, then parse these prefixes at report generation to reconstruct citations.
C. Require all subagents to output structured claim-source mappings that the synthesis agent must preserve and merge when combining findings from multiple sources.
D. Maintain complete transcripts of all subagent interactions and add a citation-resolution agent to analyze logs and determine attributions before report generation.

Image 9

Question:
Production monitoring shows that follow-up queries like "summarize what we learned about market trends" consistently take 40+ seconds. Investigation reveals the coordinator spawns the synthesis subagent for each summarization request, passing 80K+ tokens of accumulated findings. The coordinator already has these findings in its context from orchestrating the research. What’s the most effective way to improve response time for these follow-up summaries?

Options:
A. Have the coordinator handle straightforward summarization requests directly using its existing context, reserving subagent spawning for complex analysis.
B. Pre-generate and cache summaries at multiple granularities whenever new findings accumulate.
C. Spawn the synthesis subagent with reduced context and have it request specific findings from the coordinator on-demand.
D. Enable prompt caching on the synthesis subagent to reduce the overhead of repeatedly transferring the same research findings.

Image 10

Question:
Production reviews reveal inconsistent handling of uncertainty in final reports. Sometimes conflicting subagent findings are synthesized into a single confident statement (losing nuance), while other times reports over-hedge with excessive qualifications (becoming unhelpful). When the web search agent returns "industry analysts estimate $50B market size (methodology varies)" and the document analysis agent returns "peer-reviewed study estimates $35B (±$7B, 95% CI)," the coordinator either picks one arbitrarily or produces vague statements like "the market may be $35B-$50B depending on factors." What systematic approach best addresses this?

Options:
A. Implement a confidence calibration layer that normalizes subagent uncertainty expressions to standardized probability scores (0.0-1.0), then weight-average findings by their calibrated confidence.
B. Configure subagents to only report findings meeting a high-confidence threshold, filtering uncertain information before it reaches the coordinator.
C. Add a verification subagent that cross-references findings across sources, only passing claims to synthesis that are corroborated by at least two independent sources.
D. Instruct the synthesis agent to structure reports with explicit sections distinguishing well-established findings from contested ones, preserving original source characterizations and methodological context.

Image 11

Question:
When researching "renewable energy adoption," the web search agent returns recent statistics (2024: 35% adoption) while the document analysis agent extracts data from internal reports (2021: 18% adoption). The synthesis agent incorrectly flags these as contradictory sources rather than recognizing the data shows growth over time. What change would best enable the synthesis agent to correctly interpret such temporal differences?

Options:
A. Instruct the synthesis agent to always treat the most recent data as authoritative and place older findings in a separate historical appendix.
B. Configure the web search agent to only return results from the past 6 months.
C. Add a conflict resolution agent that automatically discards older data when newer data exists for the same metric.
D. Require subagents to include publication or data collection dates in their structured outputs.

Image 12

Question:
The web search agent has gathered several relevant sources for a research topic. The document analysis agent now needs to examine these sources. How does information typically flow between these two specialized subagents?

Options:
A. The coordinator agent receives the web search agent's output and includes relevant findings in the prompt when invoking the document analysis agent.
B. The web search agent directly invokes the document analysis agent, passing the discovered sources as parameters.
C. The agents communicate through an event-driven message queue, with the document analysis agent subscribing to web search completion events.
D. Both agents access a shared memory store where the web search agent writes findings and the document analysis agent reads them.

Image 13

Question:
The coordinator agent has AgentDefinitions configured for all four specialized subagents, each with appropriate descriptions, prompts, and tool restrictions. During testing, you notice the coordinator correctly reasons about when to delegate—it generates messages like "I'll ask the web search agent to find sources on this topic"—but no subagent execution ever occurs. The coordinator then proceeds as if the delegation happened and continues with incomplete information. Logs show no errors. What is the most likely cause?

Options:
A. Subagent context isolation means task descriptions from the coordinator don't automatically reach subagents; you need to configure explicit context forwarding in ClaudeAgentOptions.
B. The coordinator's allowedTools configuration doesn't include "Task", so while it can reason about delegation, it cannot invoke the tool required to spawn subagents.
C. The coordinator's max_tokens setting is too low, causing the Task tool invocation to be truncated before the subagent type parameter can be specified.
D. The AgentDefinitions are configured correctly, but the coordinator's system prompt doesn't explicitly list the available subagent types, preventing the model from knowing they can be invoked.

Image 14

Question:
In production, you observe that simple fact-checking queries (e.g., "What year was the Paris Climate Agreement signed?") traverse all four subagents sequentially, consuming 40+ seconds and significant tokens per query. Complex comparative research benefits from the full pipeline. Your query distribution is diverse and evolving as users discover new applications. What's the most effective approach to optimize for varying query complexity?

Options:
A. Train a query complexity classifier on labeled historical data to predict optimal subagent combinations, retraining periodically as query patterns evolve.
B. Create a fast-path for factual questions that bypasses subagents entirely, routing all other queries through the complete pipeline to ensure research thoroughness.
C. Implement pattern-based routing that categorizes queries by structure (single-fact vs. comparative vs. analytical) and maps each category to a predefined subagent combination.
D. Have the coordinator analyze each query and dynamically decide which subagents to invoke based on its assessment of query requirements.

Image 15

Question:
When analyzing complex legal cases that cite multiple precedents, the document analysis subagent processes each sequentially. A landmark case citing 12 precedents takes over 3 minutes to analyze completely. What's the most effective way to reduce this latency while preserving the coordinator's ability to monitor and debug the system?

Options:
A. Implement a message queue where precedent analysis tasks are processed asynchronously by a pool of worker agents
B. Have the coordinator spawn parallel document analysis subagents, each handling a subset of precedents, then aggregate results before synthesis
C. Enable the document analysis subagent to spawn its own specialized subagents dynamically when it encounters cases with many citations
D. Create a recursive agent hierarchy where analysis agents subdivide work among child agents until reaching single-precedent granularity

Image 16

Question:
The agent verifies customer identity through a multi-step process before resetting passwords. During testing, you notice that after the customer answers the third verification question, the agent asks them to provide their name again, as if the earlier exchange never happened. What's the most likely cause of this behavior?

Options:
A. The verification tool is clearing the agent's internal state after each successful validation step.
B. Claude's memory retention is limited to two conversational turns by default, requiring explicit configuration to extend it.
C. The prompt lacks instructions telling Claude to remember information across multiple exchanges.
D. The conversation history isn't being passed in subsequent API requests.

Image 17

Question:
Your agent has called lookup_order multiple times while investigating a customer's return requests. Each response includes 40+ fields (items, shipping details, payment info, status history). Tool outputs now represent the majority of the conversation's context. The customer mentions two more orders they want to discuss. What's the most effective approach before making additional lookups?

Options:
A. Have the model generate a natural language summary of each order's key details, replacing structured responses with prose descriptions
B. Move all tool responses to a vector database with semantic indexing, retrieving relevant portions as the conversation continues
C. Proceed with additional lookups without modifying the existing tool output context
D. Extract only return-relevant fields (items, purchase date, return window, status) from each existing order response, removing verbose details

Image 18

Question:
A customer returns 4 hours after their initial session about the same billing dispute. The previous 32-turn session contains lookup_order results showing "Status: PENDING, Expected resolution: 24-48 hours." In testing, you observe that when resuming sessions with stale tool results, the agent often references the outdated data in responses even after subsequent fresh tool calls return different information. What approach most reliably handles returning customers?

Options:
A. Resume with full history and add a system prompt instruction telling the agent to always prefer the most recent tool results when multiple calls to the same tool exist in context.
B. Resume with full history but filter out previous tool_result messages before resuming, keeping only the human/assistant turns so the agent must re-fetch needed data.
C. Resume with full history and configure the agent to automatically re-call all previously-used tools at session start to ensure data freshness.
D. Start a new session, inject a structured summary of the previous interaction (issue type, actions taken, resolution status), then make fresh tool calls before engaging.

Image 19

Question:
You're implementing the escalation logic for when the agent should call escalate_to_human. Your team proposes four different approaches for triggering escalation. Which approach will most reliably identify cases that genuinely require human intervention?

Options:
A. Implement sentiment analysis that monitors for frustration indicators (negative language, repeated questions, exclamation marks) and trigger escalation when the frustration score exceeds a configured threshold.
B. Instruct the agent to escalate when the customer requests a human, when the issue requires policy exceptions, or when the agent cannot make meaningful progress.
C. Build a rules engine that maps specific issue types, customer segments, and product categories to escalation decisions, removing the need for model judgment calls.
D. Configure the agent to escalate after three consecutive tool calls that fail to resolve the customer's stated issue, ensuring a reasonable attempt before involving a human.

Image 20

Question:
Your agent is handling a billing dispute. After calling get_customer and lookup_order, it identifies that the dispute involves a promotional pricing error requiring manager approval—beyond the agent's authorization level. How should the workflow handle this mid-process escalation?

Options:
A. Persist the complete conversation and tool response history to a database, then call escalate_to_human with a reference ID.
B. Attempt the refund with process_refund anyway, escalating only if the system rejects the transaction.
C. Compile a structured handoff with customer details, order info, and the identified issue before calling escalate_to_human.
D. Call escalate_to_human passing only the customer's original message.

Image 21

Question:
After investigating a billing dispute over 25+ turns, you've identified that duplicate charges occurred due to a payment gateway timeout triggering retry logic. The required refund ($847) exceeds your $500 authorization limit. You need to call escalate_to_human, and the human agent won't have access to your conversation transcript. What context should you pass to enable effective resolution?

Options:
A. A structured summary: customer ID, root cause, refund amount, and recommended action.
B. The complete conversation transcript with all tool results.
C. The customer's original complaint verbatim plus the tool result excerpts showing duplicate transactions.
D. Your diagnosis and the refund amount only.

Image 22

Question:
A customer sends: "This is frustrating. I've explained my issue twice and nothing is being resolved. I want to talk to a real person NOW." The agent has not yet called any tools to investigate their account. What should the agent do?

Options:
A. Immediately call escalate_to_human with the conversation history.
B. Briefly explain what the agent can help with and offer to resolve the issue quickly, escalating only if the customer repeats their request.
C. First call get_customer and lookup_order to gather account context, then escalate to a human agent.
D. Acknowledge the frustration and ask one targeted question to understand the specific issue before escalating.

Image 23

Question:
Compliance requires that refunds exceeding $500 must automatically escalate to a human agent—this rule cannot be left to model discretion. Despite clear system prompt instructions, production logs show the agent occasionally processes high-value refunds directly (3% failure rate). How should you achieve guaranteed compliance?

Options:
A. Modify the refund tool to return an error with message "Amount exceeds policy limit—please escalate" when threshold is exceeded.
B. Add few-shot examples to the prompt showing correct escalation behavior at various refund amounts ($400, $500, $600).
C. Implement a hook to intercept tool calls; when the refund process amount exceeds $500, block it and invoke human escalation.
D. Strengthen the system prompt with emphatic language: "CRITICAL POLICY: Refunds over $500 MUST trigger human escalation. NEVER process these directly."

Image 24

Question:
When implementing your lookup_order MCP tool, the backend sometimes returns errors (e.g., "Order not found" or temporary database failures). What is the correct pattern for communicating these errors back to the agent?

Options:
A. Return the error message in the tool result content with the isError flag set to true
B. Return a success response with a "status" field indicating the error type
C. Log the error server-side and return an empty result to avoid confusing the model
D. Throw an exception from the tool handler so the agent framework can catch and log it

Image 25

Question:
A customer raises three separate issues during one session: a refund inquiry (turns 1–15), a subscription question (turns 16–30), and a payment method update (turns 31–45). At turn 48, the customer asks "What happened with my refund?" The conversation is approaching context limits. What strategy best maintains the agent's ability to address all issues throughout the session?

Options:
A. Summarize earlier turns into a narrative description, preserving full message history only for the active issue.
B. Rely on MCP tools to re-fetch relevant information on demand when the customer references earlier issues.
C. Extract and persist structured issue data (order IDs, amounts, statuses) into a separate context layer.
D. Implement sliding window context that retains the most recent 30 turns.

Image 26

Question:
Your process_refund tool returns two types of errors: technical errors ("503 Service Unavailable", "Connection timeout") that are transient, and business errors ("Order exceeds 30-day return window", "Item already refunded") that are permanent. Monitoring shows the agent wastes 3–4 turns retrying business errors that can never succeed. Currently, both error types return only a plain text message. What’s the most effective way to reduce wasted retries while improving customer-facing response quality?

Options:
A. Implement automatic retry logic at the tool level for technical errors only, passing business errors to Claude without retries.
B. Add a check_refund_eligibility tool that must be called before process_refund to prevent business rule violations.
C. Add few-shot examples showing how to distinguish retriable from non-retriable errors by parsing error message text.
D. Return structured error responses with retriable: false for business errors and a customer-friendly explanation for Claude to use.

Image 27

Question:
A customer writes: "I've been going back and forth on this return for days. I just want to speak to someone who can actually help me." The agent has confirmed via lookup_order that the return is straightforward—within policy and eligible for immediate processing. What should the agent do?

Options:
A. Acknowledge frustration, inform them this is resolvable now, and offer to complete it or escalate
B. Ask what specifically hasn't worked in previous attempts before deciding whether to escalate or resolve automatically
C. Process the refund via process_refund to resolve the underlying issue, then inform them it's complete
D. Call escalate_to_human immediately to honor the customer's request

Image 28

Question:
When the agent calls lookup_order and receives order details showing the item was purchased 45 days ago, how does the agentic loop determine whether to call process_refund or escalate_to_human next?

Options:
A. The agent follows a pre-configured decision tree mapping order attributes to specific tool calls.
B. The orchestration layer automatically routes to the next tool based on the order's status field.
C. The order details are added to the conversation and the model reasons about which action to take.
D. The agent executes the remaining steps in a tool sequence planned at the start of the request.

Image 29

Question:
During a billing dispute resolution, your agent successfully retrieves customer info via get_customer and order details via lookup_order, but when attempting to call process_refund, the tool returns a timeout error. The agent has enough information to explain the charges and verify refund eligibility, but cannot actually process the refund due to the backend failure. What approach best balances first-contact resolution with appropriate error handling?

Options:
A. Implement automatic retries with exponential backoff for process_refund, keeping the conversation open until the refund is successfully processed
B. Explain the billing, confirm refund eligibility, acknowledge the system issue preventing immediate processing, and offer escalation or retry later
C. Escalate immediately to a human agent since the refund action cannot be completed
D. Confirm the refund will be processed and close the conversation, since the system has all necessary information to complete it automatically

Image 30

Question:
Your order management system requires tools for three distinct operations: issuing refunds (requires amount and reason), canceling orders (requires reason), and requesting reshipments (requires shipping address). Each operation shares an order_id parameter but has different additional requirements. You notice during testing that with your current unified tool design, the agent frequently omits required parameters or includes irrelevant ones. What design change will most effectively improve parameter accuracy?

Options:
A. Keep one unified tool but add JSON Schema if-then-else conditionals to enforce that parameters like amount are required only when the operation type is "refund".
B. Split into three separate tools (issue_refund, cancel_order, request_reshipment), each defining only the parameters required for that specific operation.
C. Keep one unified tool with a nested operation_details object parameter whose internal structure varies by operation type, documented in the tool description.
D. Keep one unified tool with all parameters marked optional, but add detailed few-shot examples in the system prompt showing correct parameter combinations for each operation type.

Image 31

Question:
Your agent has access to 50+ specialized API connectors for different external services. As the connector library grew, tool selection accuracy dropped to 58%. You design a search_connectors(description) tool that finds matching connectors, but in testing, agents frequently skip searching and call connectors directly (often incorrectly), or search correctly but still select wrong connectors from the filtered results. How should you design the tool composition pattern to address both issues?

Options:
A. Design a find_and_execute(description, params) composite tool that searches and immediately executes the best-matching connector.
B. Enhance all connector descriptions with detailed usage examples, edge cases, and input requirements. Add few-shot examples showing the correct search-then-use workflow.
C. Design search_connectors to dynamically add matched connectors to the agent's available tools. Connectors start unavailable and persist once discovered.
D. Design connectors with built-in compatibility validation that returns descriptive errors for mismatched requests.

Image 32

Question:
Your publish_article tool calls an external CMS API that occasionally returns transient errors (network timeouts, 503s) and non-transient errors (403 permission denied, 422 validation failure). Currently, every error is returned directly to the agent, which leads to the agent retrying non-transient errors and wasting turns on failures that will never succeed. How should you partition error-handling responsibility between the tool implementation and the agent?

Options:
A. Handle transient errors (timeouts, 503s) with automatic retries inside the tool implementation, and surface non-transient errors (permission denied, validation failures) to the agent with descriptive messages so it can take corrective action.
B. Handle all errors inside the tool: implement retries with exponential backoff for every error type, and only surface a failure to the agent after a fixed number of retry attempts have been exhausted.
C. Implement a universal error handler that catches all exceptions and returns a generic "tool unavailable—try again later" message, shielding the agent from error complexity.
D. Surface all errors to the agent immediately with detailed context, and let the agent decide which errors to retry and how many times—keeping the tool implementation stateless and simple.
