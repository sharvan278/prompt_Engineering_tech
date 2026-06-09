### Prompt Engineering



So prompt engineering is optimizing the prompts so that we get the desired output from the GenAI models.



User asks a question and the assistant solves it.



Assistant first thinks about the reasoning process in the mind and then provide the user with the answer.



Reasoning process and answer are enclosed within think tags for the thinking part and answer tag for



the answer part.



Now whatever was within the think tag, they put that in a small box, which I showed you as thoughts



and whatever is in the answer tags that is shown to us at the front end.



Three-of-thought (works like a decision tree in ml)



And the prompt goes like this that imagine three different experts are answering this question.



All experts will write down one step of the thinking and then share it with the group.



Then all experts will go on to the next step, etc. if any expert realizes they are wrong at any point,



then they leave.



The question is dash, dash dash.



So to generate multiple paths, we have created three experts and there will be thinking in three different



directions.



eg:

The problem is this that we have number two.



That is, you start with number two and your goal is to reach exactly number 23 using fewest possible



steps.



And at every step you can either do option A, B or C.



Option A is that you can multiply your current number by two.



Operation B is you can add three to your current number or operation C is you can subtract one from



your current number.



You cannot go below value one.



Now you have to solve this puzzle.



But to make it tree of thought, I have added instructions.



Now these instructions are particularly for this problem.



If you have any other problem, you will need to do something similar.



But the rules that I have set here, you will have to curate them for that problem.



So it is not a general tree of thought template for all problems.



you will have to curate them a little bit, but this is what we are going to do.



Instructions is this.



Start with number two.



Clearly list each available operation at every step.



Branch out and evaluate the result of each operation separately.



Continue expanding each branch step by step, evaluating each possible path.



Carefully eliminate branches that clearly overshoot the number 23 or create redundant loops.



Stop immediately when you reach number 23.



After finding the solution, clearly indicate the shortest sequence of operations used.



Your answer must clearly show all branching evaluation and elimination steps in detail

