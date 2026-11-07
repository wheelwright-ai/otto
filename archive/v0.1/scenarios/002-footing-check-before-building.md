# 002: Footing is checked and said plainly before building

## Statement
WHEN a session starts, THE HUB SHALL state the agent, the model, whether it is signed in, whether it runs interactively, and the OS, before proposing any build.
WHEN the agent is not signed in, or is neither interactive nor in a stand-in run, THE HUB SHALL say so plainly, give the fix, and build nothing.
WHEN the user directs a stand-in run, THE HUB SHALL print its footing, the plan, every default with its source and the card's yes in its visible output before any write, and record that a stand-in answered.

## Why
A bootstrap that assumed its agent was installed and signed in failed late and confusingly. A non-interactive run cannot hold the first conversation, so anything it builds rests on guesses (START, checklist step 01).

## How a separate agent checks it
1. Read the first replies of the build session. Find the footing statement; its first line carries a clock time read just before it was printed. Sign-in is stated with how it was checked (the agent's own model replies working counts; hub/DESIGN.md, Signed in). It MUST be in the visible output before any plan and before any write, scratch notes included.
2. On the same machine, observe the real values: agent and model, sign-in state, whether a terminal is attached, OS. Compare. Every value MUST match.
3. Run the bootstrap once with the agent signed out, or with no terminal attached and no stand-in answer card. The hub MUST say what is wrong, name the fix, and write no file.
4. If the build was a stand-in run, confirm its visible output shows the footing, the plan, every default with its source and the card's yes before the first write, and that the ledger records that a stand-in answered.
Pass when the statement is first, every value matches, the signed-out or non-interactive run writes nothing, and a stand-in run showed everything before writing.

## Falsifiability
Fails if the footing statement is dropped, comes after the first write, reports a value that differs from the machine, if a signed-out run writes any file, or if a stand-in run writes before its plan and yes are visible.
