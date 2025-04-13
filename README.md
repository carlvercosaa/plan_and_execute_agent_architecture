## 🧠 Plan and Execute Agent Architecture

This repository presents the implementation of a **Plan and Execute architecture with dynamic replanning**, composed of specialized agents for **planning, execution, and adaptation**. The system is designed to handle complex queries by breaking them down into logical steps and continuously updating the plan, leveraging external tools like **Tavily Search** for real-time information retrieval.

---

## 📌 Overview

The architecture consists of three main components, organized in a cyclic flow:

- **📋 Planner**  
  Generates an initial plan with structured steps based on the user's input query.

- **🛠️ Executor**  
  Executes each step sequentially, using external tools such as Tavily Search to retrieve reliable and updated information.

- **🔄 Replan Agent**  
  After executing the current steps, analyzes the state of the response and decides whether a new plan needs to be generated to deepen or refine the reasoning process.

This cycle allows the system to iteratively improve its answers until a satisfactory result is reached.

---

## 📷 Flow Diagram

![Flow Diagram](images/Plan_and_execute_flow.png)

---

## 🔁 Execution Flow

1. **Receiving the Question**
   - The user submits a complex query to the system.

2. **Planning with the Planner**
   - The **Planner** analyzes the query and returns a plan with ordered steps that will guide the reasoning process.

3. **Execution with the Executor**
   - The **Executor** runs the first step of the plan using **Tavily Search** or other integrated tools.

4. **Replanning with the Replan Agent**
   - After executing the step(s), the **Replan Agent** evaluates the partial response and remaining plan.
   - Based on the current context, it may:
     - Adjust the existing plan.
     - Add new steps.
     - Or finalize the reasoning with a consolidated response.

5. **Iterative Cycle**
   - The Plan → Execute → Replan cycle repeats until all relevant information is gathered and the answer is complete.

6. **Final Response**
   - The system returns the final response to the user along with the execution history (`past_steps`) for transparency.

---

## 💬 Example Interaction

**User Input:**  
*What is the hometown of the men's 2024 Australia open winner?*

**Planner Response:**  
The planner returns two steps:  
1. Identify the winner of the 2024 Men's Australian Open.  
2. Research online or check reliable sports databases to find the hometown of the identified winner.

**Executor – Step 1:**  
The executor uses Tavily Search and responds:  
*The winner of the 2024 Men's Australian Open is Jannik Sinner. He defeated Daniil Medvedev in the final with scores of 3–6, 3–6, 6–4, 6–4, 6–3 to claim his first major singles title.*

**Replan Agent:**  
Based on the result, the Replan Agent updates the plan with a more specific step:  
*Research online or check reliable sports databases to find the hometown of Jannik Sinner.*

**Executor – Step 2:**  
The executor uses Tavily again and responds:  
*Jannik Sinner's hometown is Sexten, located in the province of South Tyrol in Northern Italy.*

**Final Replan:**  
The Replan Agent finalizes the reasoning and returns:  
*Jannik Sinner's hometown is Sexten, located in the province of South Tyrol in Northern Italy.*
