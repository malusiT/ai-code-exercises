# Code Journal 
** (Summary of Code Base) **


## Understanding a Specific Feature

### My Understanding

The Task is created when code in the cli is ran as it is the entry point and user input is taken and then to create a task The task.java file class is used as a blueprint of tha task and
by default is creates a task priority of meduim using taskPriority enum in the model package then a task is created and save using the TaskStorage class.

cli package JavaCliManager.java - Seems to be entry point and where user input is parsed
2. model package where Task.java, TaskPriority.java and TaskStatus.java - Might be handling might handle creation and update of a task
3. storage package where TaskStorage.java - Contains references to task saving logic.

### My Prompt

```bash
I'm trying to understand how the task creation and status updates works in our java gradle codebase.
This feature seems to handle Tasks to create and updates them in 

Here are the key files that appear to be involved:
/src/main/java/za/co/wethinkcode/taskmanager

1. cli package JavaCliManager.java - Seems to be entry point and where user input is parsed
2. model package where Task.java, TaskPriority.java and TaskStatus.java - Might be handling might handle creation and update of a task
3. storage package where TaskStorage.java - Contains references to task saving logic.


Could you:
1. Explain in simple terms what this component actually does
2. Walk me through the execution flow when atask is created.
3. Clarify how these files interact with each other
4. Identify any external dependencies or services this component relies on
5. Explain any complex code blocks
6. Provide a mental model I can use to think about this component

I'm particularly confused about updating the task, so extra detail there would help.
Finally, suggest 3 small code changes I could make to validate my understanding. Do not give the me change, and instead give me the requirement.
```

### Understanding After AI

- When I create or update a task, the CLI layer interprets the command, the model layer represents the task in memory, and the storage layer saves or updates it.

- The CLI receives an update command (e.g., "update task 3 to done").
- It finds the task (by ID or name) using the storage layer.
- Updates the task’s status (using the `TaskStatus` enum).
- Saves the updated task back to storage.


## Deepen Understanding Through Guided Questions

- How task priorities work

### My Understanding

- The task are priorities as:
1. Low
2. High
3. Medium
4. Urgent

-Each has a level value from 1 - 4, One being low and High being 4.
- When not specified each task has a priority of Medium and can be updated when a task is updated.

## My Prompt
```bash
I'd like your help in deepening my understanding of a codebase by you acting as my senior development pair programmer.
First, I'll share my current understanding of the code I'm exploring. Please acknowledge what parts I've understood correctly, then guide me with thoughtful questions rather than direct explanations.
## My Current Understanding:

I'm exploring files on the model package From what I can tell
The task are priorities as:
1. Low
2. High
3. Medium
4. Urgent

-Each has a level value from 1 - 4, One being low and High being 4.
- When not specified each task has a priority of Medium and can be updated when a task is updated.
The main files involved appear to be:
- Task.java
- TaskPriority.java
I think the code works like this:
[describe what you believe happens when this code runs]

1. Acknowledge what parts of my understanding seem accurate
2. Ask me 3-5 thoughtful questions that will help me discover insights about:
   - What specific parts of the code actually do
   - How data moves through these functions
   - What happens in different scenarios missing parameters and if peiority selected on not available   - Why certain implementation choices were made

3. For some questions, ask me to share specific code snippets that would help answer the question
4. End with a practical question about how I might use or modify this code

Please don't give me direct explanations - help me discover the answers through guided questioning.
```

## My understanding After AI

- I Hade the correct dea on how the priorities are set up but didn't know not think about how to add changes tp the app eg. when to add prority level Critical

## Mapping Data Flow

User Input (CLI) <br>
  &emsp;&emsp;&emsp; &emsp;↓<br>
TaskCliManager (parses command) <br>
  &emsp;&emsp;&emsp; &emsp;↓<br>
TaskManager (finds and updates Task) <br>
  &emsp;&emsp;&emsp; &emsp;↓ <br>
Task.markAsDone() (updates state) <br>
   &emsp;&emsp;&emsp;&emsp;↓<br>
TaskStorage.save() (serializes and persists) <br>
   &emsp;&emsp;&emsp;&emsp;↓<br>
CLI Output (success/error) <br>

