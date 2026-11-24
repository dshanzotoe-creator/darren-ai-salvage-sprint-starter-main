# Week 1 evidence

Keep this short. Bullet points, a small table and one diagram or code trace are enough. This is your checkpoint record, not an extra report. Replace the prompts as you work.

Name: Darren Scott
Exact Unity version: 6000.3.26f1
Checkpoint commit / repository: 
Current stage and anything unfinished: Stage 2 

## Initial prediction

Three observations the rival needs, including one it might not have:

Seeing a pickup across a gap proves / does not prove reachability because:

One question about NPC behaviour:

## One complete trace

Use one actual situation. Include the observation data, derived facts, selected task and reason, movement request/result, and how feedback affects a later decision. Identify the responsible code locations. A tiny state diagram can accompany this trace.

One situation I put the "Rival AI" in, was moving a wall from it's original position and blocking the cube with ID "11". 
This resulted in the rival throwing a "Route Failure Error". From my understanding, the Rival AI only cares about what is considered the
"closest" scrap by distance. The AI disregards any other observation data such as: whether the scrap is actually visible, remembered, or blocked.
RivalBrain.Update() gathers observations through PickupSensor.Capture(), then uses DecisionPolicy.Infer() and DecisionPolicy.Choose() to derive facts
and select a task, target and reason. When cube 11 is selected for collection, Navigator.Request() sends its position to NavMeshAgent.SetDestination() to
request a route. Navigator.Poll() checks the result using NavigationFeedback.Classify(), and an incomplete route or more than five seconds without sufficient 
progress can produce TravelStatus.Failed. RivalBrain.Update() responds by recording a six-second block for cube 11 in failedUntil, 
which IsBlocked() makes available to subsequent observations. This feeds the failure back into later decisions.

## Scenario record

| Scenario | Predicted result | Observed result and short evidence / remaining issue |
|---|---|---|
| Normal loop and restart | | |
| Carrying cargo | | |
| Hidden / remembered pickup | | |
| Target taken | | |
| Unreachable target | | |
| No usable pickup | | |

Supplied test result, with any added tests identified:
Live walkthrough checked by / recording link if used:

## One correction and one independent check

The original weakness and why it happened:
What I changed and why it addresses the cause:
My counterexample or experiment: prediction, observed result, and one limitation:

## Collaboration and help

People I discussed or playtested with:
Code, sources or substantive tools/AI assistance I used, and how I verified them:
If unfinished: what works, exact reproduction steps, and the help I need:
