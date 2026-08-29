Here is the updated write-up with the new section on attention and the non-linear execution model woven into the introduction:

---

Programming with Intelligent Generative Models

Programming with intelligent generative models should use the most advanced model for learning about a domain, run inference on the cheapest possible model, and—as programming is with natural language—it has to be customizable in production.

The Mindset: Einstein for Research, Engineer for Runtime

The guiding philosophy is to separate thinking from doing. For research and deep analysis, you want the most sophisticated model available—one with enough complexity to see across a wide range of possibilities and connect them to the outcome you're after. The larger the model, the better it is at understanding the problem space, mapping requirements, and distilling the essence of what needs to happen.

But once that understanding is captured—once the requirements are documented and the logic is clear—you don't need that level of intelligence to execute. You distill everything into tight, precise prompts (and possibly additional training) for a much smaller model. The big model does the physics; the small model does the calculation.

Running on a small model forces you to be efficient and to confront unexpected behavior from day one. It makes the system resilient because you design around the assumption that the model might get things wrong, rather than assuming it will always be right. You account for error, you build in guardrails, and you end up with a product that is robust by necessity. It is the difference between needing Einstein to derive the theory, and needing a reliable engineer to plug numbers into E = mc².

Context and Learning Are Interchangeable

A core part of this architecture is that context and learning are two sides of the same coin. Whatever you might supply to a model as runtime context to drive the right answer can, alternatively, be baked into the model itself through training on data that reflects that same context. Conversely, data can be analyzed to extract the contextual patterns that would duplicate the same behavior at runtime. This means the boundary between "what the model knows" and "what the model is told" is fluid. You can shift context from the prompt into the weights, or extract it from the weights back into the prompt—whichever makes the system cheaper, faster, and more maintainable.

Prompts Are the Program

GPT-2 made it clear that these models are not trained specifically for any single task. Instead, they learn broad capabilities, and it is through prompts that we steer them to execute a particular task. This shifted the paradigm: the prompt is not merely a tool for generating code; the prompt is the instruction that drives the work.

Generating code became a background concern. Code, once deployed, is rigid—it is not easily changed in the field. Prompts, on the other hand, are dynamic and customizable at runtime. If you capture more of your program's logic as prompts, supported by only the most basic underlying functionality, what you get is an application that can be customized and reconfigured on the spot, wherever it is running.

Your runtime becomes a sequence of prompts—chained, orchestrated, and adjusted live to perform autonomous or agentic work. The prompts are the logic; they are the control flow. External tools and APIs (much like MCP) can handle execution side effects, but the reasoning, decision-making, and action selection all happen inside the prompt sequence. This is why Clojure is a natural fit: its homoiconicity means executing code is structurally the same as manipulating text. A prompt and a function call are not different categories—they are the same material, which makes it seamless to build a system where natural language instructions drive the runtime.

Attention as the Execution Model

The first advantage of an LLM is that natural language controls the behavior of the model. The second, deeper advantage is the attention mechanism itself—the n-squared complexity of looking across the entire structure to determine the next token, the next thought, the next action.

In traditional programming, the execution model is linear and localized. If you are dealing with a stack, a Python programmer looks only at the top of the stack; the code is organized to recursively or iteratively traverse it, one frame at a time, because the CPU executes sequentially. The program has access only to what is explicitly loaded into registers or the current scope.

In an LLM, the "stack" lives in the context window, and everything in that context is fair game simultaneously. The model does not look at just the top of the stack; it attends to the entire history, the entire state, the entire problem description at once. It can draw a connection between a requirement mentioned fifty turns ago and a detail in the current input without you explicitly wiring that pointer. And it does this all in parallel across the GPU.

This is a fundamentally different programming model. A CPU application is a linear march through instructions. An LLM application is a parallel, attention-weighted search through context. Your program has access to far more data at the moment of decision, and it reasons holistically rather than procedurally. You are not writing a recipe; you are describing a situation and letting the model find the relevant patterns across the whole situation to decide what comes next. That is why the prompt—and the context you feed into it—is the true program. The execution is not linear; it is relational.

---

My Process for Developing an AI-Driven App

1. Deep Analysis with a Large Model
I start by using a large language model to perform deep analysis on the data and the operational environment. I feed it the full context of the problem and have it break down what's required. From that analysis, I derive the initial set of prompts that will drive the work.

2. Build the Core Project in Clojure
Next, I move to a real project built in Clojure, working in a REPL loop for rapid iteration. I take those initial prompts and test them against the smallest, cheapest model instance that can still handle the task. The goal is to find the minimum viable model that does the job.

3. Act as the Runtime Environment
At this stage, I am essentially the runtime environment. I feed the model sample data—both current and historical—and evaluate the outputs. When something is off or I spot anomalies, I adjust the prompts, refine the instructions, and retest. I keep iterating until the behavior is correct.

4. Convert to a Service with a Chat Interface
Once the core logic is solid, I convert the Clojure code into a running service. Rather than interacting through a command line, I expose the application through a chat interface—similar to Claw—where I can feed commands, review outputs, and steer the system conversationally. This becomes the primary way to operate and manage the runtime.

5. Expose Development Tools via API
Everything I needed while developing the app is exposed through the API. I can query the current prompt, update it, search through aspects of the application's behavior, and inspect how the system is operating—all through the same interface. Git operations are also part of the API: I can save changes, check them into the project, and manage version history without leaving the chat. The boundary between running the app and evolving it disappears.

6. Build in Updateability
Because the system will encounter edge cases and shifting data in production, the whole process must be designed for ongoing updates. The prompts are not static; they are living artifacts that evolve as the model encounters real-world inputs at the customer side.

7. Version Control and Long-Term Evolution
By now, I have a Git-managed Clojure project containing the service, the loop structure, and all the prompts the app feeds to the LLM. When I refine a prompt, I check it in through the API, validate it, and update the project. Over time, the system evolves, and because everything is under version control, I can roll back to any previous state. The repository itself becomes the runtime environment.

---

Let me know if the new section captures the distinction you were aiming for, or if you want to sharpen the contrast with traditional CPU execution further.