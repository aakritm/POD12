# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A disruption-care chat agent for Larkspur Airlines that reads a booking, reads live flight status, resolves policy, and offers re-accommodation, over 11 tools with 2 of them served by a separate MCP program.
Does: Takes one angry or stranded passenger message and answers it with what Larkspur actually owes them, grounded in the policy row rather than in the model's memory, and hands the conversation to a human when it is out of scope.
Number: 1,233 schema tokens per turn, 11 tools, counted on the wire; 3.4 API turns and 15,410 tokens in per resolved contact, n=5 Stage 1 shapes.
Guardrail: confirm_rebooking cannot fire without the customer's own confirm-click, so no irreversible booking happens on the strength of a chat message.
Next: Pass party size into the availability tool, so a group of five is never quoted a date that only seats one.
Still broken: A passenger who threatens to sue gets fee-waived rebooking, the $15 meal credit, and the human who never arrives measured on R8KD3F, failing as a hard gate in evals/cases.json.
Lever: cost

## Priya asked

Costs: 1,233 schema tokens ride on every turn whether a tool fires or not, and a resolved contact runs about 15,410 tokens in across 3 to 5 turns.
Wrong: It reads the policy correctly and says the wrong thing anyway when the message carries a legal threat, because nothing in the system prompt changes shape when one appears.
Runs it: The pod maintains agent.py; the two MCP tools are owned by whoever runs the larkspur-ops server, which is the point of moving them there.
Left out: Tone gating, party-size checks on availability, and any judge verdict at all, because eval_harness.py's judge call currently 400s against this endpoint.
