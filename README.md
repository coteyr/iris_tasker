Goals
======

First, to create a set of tasks that can be used to integrate our Android smart phones with our Iris Systems
Second, to share those tasks in a way that lots (or at least some) other people can readily use
Third, to share ideas and concepts to create new and better tasks and automation
 
Rules
======

1. All code uploaded to the repo is covered under the GPL v3. Meaning it's open for ANYONE to use. 
2. No ads or nags or such in the tasks.
3. All variable names start with iris or IRIS (depending on scope), Tasks should start with Iris. -- This helps keep the collisions down with non-iris related tasks
4. No Personal credentials (don't leave your user names and passwords (or devices) in the tasks.
5. Tasks should do one thing, and only one thing. i.e. Turning off a switch requires a login, then the command, then a notification. These should be converted to three tasks so we can reuse them later.
6. Tasks should not (most of the time) require editing to use. So we have to write them in a way that, at least most of the time people can use them with no need to edit them. 
7. Tasks should use Iris Init before calling commands (to handle login and session management)
8. Tasks should use a similar icon (we can use the Iris one for now) so we can easily id them in among our other existing tasks. 
 
Examples
========
 
So a simple "turn on the light task"
 
Bad Way: Copy a task then modify it so that the task holds the login call, the API call, and a notification. 
Reason it's bad: When you need to make another turn on the light switch call you have a lot of editing, and after you have 10 of these, when the API changes. Your whole setup needs to be redone.
 
Good Way: Create a task that calls "Iris Init" then, "Iris Switch On", then "Iris Notify" with arguments for the device id.
Reason it's good: When the API changes you only have to modify the "Iris Init", "Iris Switch On" and "Iris Notify" commands and all your 10 switches keep working.
 
This is tricky but becomes very important as we start adding features. For example session management (which makes MUCH faster) isn't even possible unless you use something like "Iris Init" to handle it. Same with notifications, it seems simple, but you can get much nicer and uniform notifications using a notification task instead of building a notification in every task.
 
Finally some rules about things not to do
 
9. First keep in mind that were calling a Non-Supported API. Try to not kill there servers.
10. No Pooling tasks (the kind that keep checking the API to see if something has changed, getting data is fine, getting it once every 5 seconds isn't)
