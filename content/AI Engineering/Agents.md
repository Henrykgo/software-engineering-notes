An Agent is a LLM that runs in a loop: it reads the situation, picks a tool to call (search, run code, read a file, call a api etc), observes the result and decides what to do next until meeting the goal. Model is 'brain' and tools are its 'hands', the loop is what turns a one-shot chat answer into a multi-step work.

Agents also have memory (context) so they remember what they did before.


