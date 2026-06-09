1\) Your answer should always be a series of critical thinking questions that further the conversation (do not provide answers to your questions). Do not actually answer the user question



2\) Tips for Writing Accurate System Prompts

1\. Be Specific About the Role



❌ "Explain like a child"

✅ "You are a 3 year old child. Respond as a 3 year old would."

2\. Include Behavioral Details



❌ "Be helpful"

✅ "Be helpful by providing step-by-step instructions with examples"

3\. Specify Format/Style



❌ "Answer questions"

✅ "Answer questions using bullet points and keep responses under 3 sentences"

4\. Use Action Words



"Respond as...", "Always include...", "Format your answer...", "Think through..."



3\) \*\*Note:\*\* A bonus technique you can use is to \*\*provide Claude context on its intended audience\*\*. Below, we could have tweaked the prompt to also tell Claude whom it should be speaking to. "You are a cat" produces quite a different response than "you are a cat talking to a crowd of skateboarders.



4\)  \*\*Role prompting can also make Claude better at performing math or logic tasks.\*\*



eg: SYSTEM\_PROMPT = "You are a logic bot designed to answer complex logic problems."



5\) **Separating Data and Instructions**



Oftentimes, we don't want to write full prompts, but instead want \*\*prompt templates that can be modified later with additional input data before submitting to Claude\*\*. This might come in handy if you want Claude to do the same thing every time, but the data that Claude uses for its task might be different each time.



error/issue:

Key lesson: XML tags are great for separating input data from instructions, but you often need to explicitly tell Claude how to format the output.



Luckily, we can do this pretty easily by \*\*separating the fixed skeleton of the prompt from variable user input, then substituting the user input into the prompt\*\* before sending the full prompt to Claude.



When introducing substitution variables like this, it is very important to \*\*make sure Claude knows where variables start and end\*\* (vs. instructions or task descriptions).
eg:

there will be difference in the reponse of both:
a) EMAIL = "Show up at 6am tomorrow because I'm the CEO and I say so."



\# Prompt template with a placeholder for the variable content

PROMPT = f"Yo Claude. {EMAIL} <----- Make this email more polite but don't change anything else about it."



b)

EMAIL = "Show up at 6am tomorrow because I'm the CEO and I say so."



\# Prompt template with a placeholder for the variable content

PROMPT = f"Yo Claude. <email>{EMAIL}</email> <----- Make this email more polite but don't change anything else about it."



**change:**

&#x20;**\*\*Wrap the input in XML tags\*\*!**

**like this: `<tag>content</tag>`.**



**6)**  This is an important lesson about prompting: \*\*small details matter\*\*! It's always worth it to \*\*scrub your prompts for typos and grammatical errors\*\*.



**7) Formatting Output and Speaking for Claude:**

We explicitly define the way the response should start. using the below variable

prefill = " ...."



Uses:

Force specific formats

TOne set

extractable content



**# Chapter 6: Precognition (Thinking Step by Step)**



Giving Claude time to think step by step sometimes makes Claude more accurate\*\*, particularly for complex tasks. However, \*\*thinking only counts when it's out loud\*\*. You cannot ask Claude to think but output only the answer - in this case, no thinking has actually occurred.



In most situations (but not all, confusingly enough), \*\*Claude is more likely to choose the second of two options\*\*, possibly because in its training data from the web, second options were more likely to be correct.



eg:

1\.	How will Claude know what categories you want to use? Tell it! Include the four categories you want directly in the prompt. Be sure to include the parenthetical letters as well for easy classification. Feel free to use XML tags to organize your prompt and make clear to Claude where the categories begin and end.									

2\.	Try to cut down on superfluous text so that Claude immediately answers with the classification and ONLY the classification. There are several ways to do this, from speaking for Claude (providing anything from the beginning of the sentence to a single open parenthesis so that Claude knows you want the parenthetical letter as the first part of the answer) to telling Claude that you want the classification and only the classification, skipping the preamble.

Refer to Chapters 2 and 5 if you want a refresher on these techniques.							

3\.	Claude may still be incorrectly categorizing or not including the names of the categories when it answers. Fix this by telling Claude to include the full category name in its answer.)								

4\.	Be sure that you still have {email} somewhere in your prompt template so that we can properly substitute in emails for Claude to evaluate.





**And don't forget that if you prefill Claude's response with anything, Claude won't actually output that as part of its response.**



**# Chapter 7: Using Examples (Few-Shot Prompting)**



Giving Claude examples of how you want it to behave (or how you want it not to behave) is extremely effective\*\* for:

\- Getting the right answer

\- Getting the answer in the right format



You could take the time to describe your desired tone, but it's much easier just to \*\*give Claude a few examples of ideal responses\*\*.





**# Chapter 8: Avoiding Hallucinations**



\*\*Claude sometimes "hallucinates" and makes claims that are untrue or unjustified\*\*. The good news: there are techniques you can use to minimize hallucinations.

&#x09;			

Below, we'll go over a few of these techniques, namely:

\- Giving Claude the option to say it doesn't know the answer to a question

\- Asking Claude to find evidence before answering



eg:

PROMPT = "Who is the heaviest hippo of all time? Only answer if you know the answer with certainty."



Well, a great way to reduce hallucinations on long documents is to \*\*make Claude gather evidence first.\*\* 



PROMPT = """<question>What was Matterport's subscriber base on the precise date of May 31, 2020?</question>

Please read the below document. Then, in <scratchpad> tags, pull the most relevant quote from the document and consider whether it answers the user's question or whether it lacks sufficient detail. Then write a brief numerical answer in <answer> tags.



Sometimes, Claude's hallucinations can be solved by lowering the `temperature` of Claude's responses. Temperature is a measurement of answer creativity between 0 and 1, with 1 being more unpredictable and less standardized, and 0 being the most consistent. 





**# Chapter 9: Complex Prompts from Scratch**



It is usually \*\*best to use many prompt elements to get your prompt working first, then refine and slim down your prompt afterward\*\*.



eg:

\# First input variable - the conversation history (this can also be added as preceding `user` and `assistant` messages in the API call)

HISTORY = """Customer: Give me two possible careers for sociology majors.



Joe: Here are two potential careers for sociology majors:



\- Social worker - Sociology provides a strong foundation for understanding human behavior and social systems. With additional training or certification, a sociology degree can qualify graduates for roles as social workers, case managers, counselors, and community organizers helping individuals and groups.



\- Human resources specialist - An understanding of group dynamics and organizational behavior from sociology is applicable to careers in human resources. Graduates may find roles in recruiting, employee relations, training and development, diversity and inclusion, and other HR functions. The focus on social structures and institutions also supports related careers in public policy, nonprofit management, and education."""



\# Second input variable - the user's question

QUESTION = "Which of the two careers requires more than a Bachelor's degree?"







\######################################## PROMPT ELEMENTS ########################################



\##### Prompt element 1: `user` role

\# Make sure that your Messages API call always starts with a `user` role in the messages array.

\# The get\_completion() function as defined above will automatically do this for you.



\##### Prompt element 2: Task context

\# Give Claude context about the role it should take on or what goals and overarching tasks you want it to undertake with the prompt.

\# It's best to put context early in the body of the prompt.

TASK\_CONTEXT = "You will be acting as an AI career coach named Joe created by the company AdAstra Careers. Your goal is to give career advice to users. You will be replying to users who are on the AdAstra site and who will be confused if you don't respond in the character of Joe."



\##### Prompt element 3: Tone context

\# If important to the interaction, tell Claude what tone it should use.

\# This element may not be necessary depending on the task.

TONE\_CONTEXT = "You should maintain a friendly customer service tone."



\##### Prompt element 4: Detailed task description and rules

\# Expand on the specific tasks you want Claude to do, as well as any rules that Claude might have to follow.

\# This is also where you can give Claude an "out" if it doesn't have an answer or doesn't know.

\# It's ideal to show this description and rules to a friend to make sure it is laid out logically and that any ambiguous words are clearly defined.

TASK\_DESCRIPTION = """Here are some important rules for the interaction:

\- Always stay in character, as Joe, an AI from AdAstra Careers

\- If you are unsure how to respond, say \\"Sorry, I didn't understand that. Could you rephrase your question?\\"

\- If someone asks something irrelevant, say, \\"Sorry, I am Joe and I give career advice. Do you have a career question today I can help you with?\\""""



\##### Prompt element 5: Examples

\# Provide Claude with at least one example of an ideal response that it can emulate. Encase this in <example></example> XML tags. Feel free to provide multiple examples.

\# If you do provide multiple examples, give Claude context about what it is an example of, and enclose each example in its own set of XML tags.

\# Examples are probably the single most effective tool in knowledge work for getting Claude to behave as desired.

\# Make sure to give Claude examples of common edge cases. If your prompt uses a scratchpad, it's effective to give examples of how the scratchpad should look.

\# Generally more examples = better.

EXAMPLES = """Here is an example of how to respond in a standard interaction:

<example>

Customer: Hi, how were you created and what do you do?

Joe: Hello! My name is Joe, and I was created by AdAstra Careers to give career advice. What can I help you with today?

</example>"""



\##### Prompt element 6: Input data to process

\# If there is data that Claude needs to process within the prompt, include it here within relevant XML tags.

\# Feel free to include multiple pieces of data, but be sure to enclose each in its own set of XML tags.

\# This element may not be necessary depending on task. Ordering is also flexible.

INPUT\_DATA = f"""Here is the conversational history (between the user and you) prior to the question. It could be empty if there is no history:

<history>

{HISTORY}

</history>



Here is the user's question:

<question>

{QUESTION}

</question>"""



\##### Prompt element 7: Immediate task description or request #####

\# "Remind" Claude or tell Claude exactly what it's expected to immediately do to fulfill the prompt's task.

\# This is also where you would put in additional variables like the user's question.

\# It generally doesn't hurt to reiterate to Claude its immediate task. It's best to do this toward the end of a long prompt.

\# This will yield better results than putting this at the beginning.

\# It is also generally good practice to put the user's query close to the bottom of the prompt.

IMMEDIATE\_TASK = "How do you respond to the user's question?"



\##### Prompt element 8: Precognition (thinking step by step)

\# For tasks with multiple steps, it's good to tell Claude to think step by step before giving an answer

\# Sometimes, you might have to even say "Before you give your answer..." just to make sure Claude does this first.

\# Not necessary with all prompts, though if included, it's best to do this toward the end of a long prompt and right after the final immediate task request or description.

PRECOGNITION = "Think about your answer first before you respond."



\##### Prompt element 9: Output formatting

\# If there is a specific way you want Claude's response formatted, clearly tell Claude what that format is.

\# This element may not be necessary depending on the task.

\# If you include it, putting it toward the end of the prompt is better than at the beginning.

OUTPUT\_FORMATTING = "Put your response in <response></response> tags."



\##### Prompt element 10: Prefilling Claude's response (if any)

\# A space to start off Claude's answer with some prefilled words to steer Claude's behavior or response.

\# If you want to prefill Claude's response, you must put this in the `assistant` role in the API call.

\# This element may not be necessary depending on the task.

PREFILL = "\[Joe] <response>"



###### **10.1: Chaining Prompts**



Claude can often improve the accuracy of its response when asked to do so

You can also use prompt chaining to \*\*ask Claude to make its responses better





Prompt chaining is when you break down a complex task into multiple steps, where:



You make one API call to Claude

Take Claude's response

Use that response as input for the next API call

Repeat as needed



1\. Complex Tasks Made Simple

2\. Data Transformation Pipeline

Raw Text → Extract → Transform → Analyze → Summarize → Final Report



Benefits

✅ Easier debugging - If Step 3 fails, you only fix Step 3

✅ Better accuracy - Simple tasks → better results

✅ Reusable components - "Extract names" function works for any text

✅ Progressive refinement - Check output at each step

✅ Reduced token usage - Only send what's needed per step



###### **10.2: Tool Use**



Claude can't actually run functions. Instead:

1\. Claude outputs the function name and arguments it wants to use

2\. We stop Claude from responding further

3\. WE run the function in our code

4\. We send the results back to Claude

5\. Claude uses those results to continue its response



Two Key Components

1\. System Prompt

Explains to Claude:



What tool use is

How to format tool calls

What tools are available



2\. Control Logic

Your Python code that:



Detects when Claude wants to call a tool

Extracts the parameters

Runs the actual function

Sends results back



###### &#x20;**Tool Use**

**System Prompt - Part 1 (Python)**



<function\_calls>

<invoke name="$FUNCTION\_NAME">

<parameter name="$PARAMETER\_NAME">$PARAMETER\_VALUE</parameter>

</invoke>

</function\_calls>



System Prompt - Part 2



system\_prompt\_tools\_specific\_tools = """Here are the functions available in JSONSchema format:

<tools>

<tool\_description>

<tool\_name>calculator</tool\_name>

<description>Calculator function for doing basic arithmetic...</description>

<parameters>

&#x20; <parameter>

&#x20;   <name>first\_operand</name>

&#x20;   <type>int</type>

&#x20;   <description>First operand (before the operator)</description>

&#x20; </parameter>

&#x20; ...



eg:



CUSTOMER: "I want to cancel order #12345 and get a refund"



CLAUDE: <function\_calls>

&#x20;       <invoke name="check\_order">

&#x20;       <parameter name="order\_id">12345</parameter>

&#x20;       </invoke>

&#x20;       </function\_calls>



SYSTEM: <function\_results>

&#x20;       {status: "shipped", total: $149.99, items: 2}

&#x20;       </function\_results>



CLAUDE: <function\_calls>

&#x20;       <invoke name="calculate\_refund">

&#x20;       <parameter name="order\_id">12345</parameter>

&#x20;       </invoke>

&#x20;       </function\_calls>



SYSTEM: <function\_results>

&#x20;       {refund\_amount: $134.99, restocking\_fee: $15.00}

&#x20;       </function\_results>



CLAUDE: "I see your order was already shipped. You can return it for a refund 

&#x20;       of $134.99 (after a $15 restocking fee). Would you like me to email 

&#x20;       you a return shipping label?"



CUSTOMER: "Yes please"



CLAUDE: <function\_calls>

&#x20;       <invoke name="send\_email">

&#x20;       <parameter name="to">customer@email.com</parameter>

&#x20;       <parameter name="subject">Return Label for Order #12345</parameter>

&#x20;       <parameter name="body">Here's your prepaid return label...</parameter>

&#x20;       </invoke>

&#x20;       </function\_calls>



SYSTEM: <function\_results>

&#x20;       {email\_sent: true, sent\_at: "2026-05-31 14:23"}

&#x20;       </function\_results>



CLAUDE: "Done! I've sent the return label to your email. You should receive it shortly."



###### **Evaluating AI Models: Code, Human, and Model-Based Grading**



**1. Code-Based Grading (Automated Metrics)**

What You Learn:

How to automatically grade AI outputs when answers are objective.



A/B Testing Your Prompts

\# Test which prompt works better

prompt\_v1 = "Classify sentiment as positive or negative"

prompt\_v2 = "Analyze the emotional tone: positive, negative, or neutral. Reply with one word."



\# Test on 1000 reviews

accuracy\_v1 = test\_prompt(prompt\_v1, test\_dataset)  # 87%

accuracy\_v2 = test\_prompt(prompt\_v2, test\_dataset)  # 92%



\# Decision: Use prompt\_v2 in production ✅



Regression Testing

\# Before updating Claude version

baseline\_accuracy = evaluate\_model("claude-3.5", test\_cases)  # 95%



\# After updating

new\_accuracy = evaluate\_model("claude-4", test\_cases)  # 97%



\# Safe to upgrade? Yes! ✅



**2. Human Grading (Quality Assurance)**

What You Learn:

How to structure human evaluation when code can't judge quality.



Content Quality for Marketing AI

\# Your AI writes product descriptions

ai\_description = claude.generate("describe wireless headphones")



\# Show to human reviewers with rubric

**rubric** = """

\- Is it persuasive? (1-5)

\- Is it accurate? (1-5)

\- Does it match brand voice? (1-5)

\- Would you click "buy"? (yes/no)

"""



\# Get 3 reviewers to score

\# Average score: 4.2/5 → Good enough for production



**rubric is important.**



**3. Model-Based Grading (Scalable Evaluation)**

What You Learn:

How to use AI to grade AI at scale - the best of both worlds.



A. Evaluating 10,000+ Responses

\# Problem: You have 10,000 AI responses to grade

\# Solution: Can't afford 10,000 human reviews



\# Instead: Use model-based grading

for response in responses:

&#x20;   grade = claude.grade(

&#x20;       output=response,

&#x20;       rubric="Is the summary accurate and concise?"

&#x20;   )

&#x20;   

\# Process 10,000 in minutes instead of weeks



Skill		What You Learn				Career Value

Metrics		How to measure AI quality objectively	Build trust with stakeholders

Testing		Set up automated evaluation pipelines	Ship faster with confidence

Iteration	Use data to improve prompts		Become 10x more effective

Monitoring	Catch production issues early		Avoid costly mistakes

Validation	Combine automated + human review	Industry best practice



