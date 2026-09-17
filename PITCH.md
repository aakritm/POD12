# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A disruption-care chat agent for Larkspur Airlines that reads a booking, reads live flight status, resolves policy, and offers re-accommodation, over 11 tools with 2 of them served by a separate MCP program.
Does: Takes one angry or stranded passenger message and answers it with what Larkspur actually owes them, grounded in the policy row rather than in the model's memory, and hands the conversation to a human when it is out of scope.
Number: $0.0241 model cost per resolved contact, down 59% from $0.0589, n=5 Stage 1 shapes x 3 runs each side; 2,811 input tokens per contact, down 82%, at an 81% cache hit.
Guardrail: confirm_rebooking cannot fire without the customer's own confirm-click, so no irreversible booking happens on the strength of a chat message.
Next: Author TONE_ADDENDUM so a legal threat stops the entitlements rundown, then pass party size into the availability tool so a group of five is never quoted a date that only seats one.
Still broken: A passenger who threatens to sue gets fee-waived rebooking, the $15 meal credit, and the human who never arrives measured on R8KD3F, failing as a hard gate in evals/cases.json.
Lever: cost

## Priya asked

Costs: $0.0241 model cost per resolved contact, about $330/week at Larkspur's 13,700 chats/week against $94,530 for the human line. Model cost only: Larkspur's own loaded number ran about 60% higher than model cost, so call it loaded and estimated if you quote it that way. 1,233 schema tokens still ride on every turn whether a tool fires or not; caching is what makes them cheap, not absent.
Wrong: It reads the policy correctly and says the wrong thing anyway when the message carries a legal threat, because nothing in the system prompt changes shape when one appears.
Runs it: The pod maintains agent.py; the two MCP tools are owned by whoever runs the larkspur-ops server, which is the point of moving them there.
Left out: Tone gating, party-size checks on availability, and latency, which barely moved (p50 13.48s to 12.96s) because this lever cut tokens, not time. Also every judge verdict: eval_harness.py's judge call 400s against this endpoint, so two of the three cases are unproven rather than failed.
