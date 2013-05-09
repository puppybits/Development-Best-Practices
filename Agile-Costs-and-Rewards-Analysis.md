# Agile: A formalized process to constantly improve and innovate, deliver constancy and build a stronger team that builds better products.

* if each sprint isn't getting better then you're doing something wrong.
---

### My background
This comes from my personal experience on some very good and very poor implementations of Agile. The cost (developer time) associated in order to get the rewards (stable, useable product) in using a process. Most of the process implementation are from a single project I worked on and how processes lead to an amazingly plyable, useful and stable product. The recommendations come from my experience with balancing the cost/rewards when building new innovated projects.

---

# Key Learnings

---

* The building process is about building out, not up. You should be able to have features & services that can be leveraged, refactored or swapped out without breaking the entire project.
* Tech Lead role: 
  * base level-set on the development skill set
	* must be coding at least 40% of the time
	* can be, but doesn't need to be, the architect 
	* generally tech leads spend too much time leading and not enough time coding and building up the team
* Architect role:
	* the target for every developer to reach
	* focuses on application strategy with minimal time on keeping the client in touch
	* level sets with tech leads
* Unit Testing has a steep learning curve and a large chasm to gain the true benefits. Also if you don't understand what or why you should or shouldn't be testing a piece of code it's probably useless and just a huge time sink. First and for most is to set KPI, track it and if you're not sure about it then remove unit testing to recalibrate your base.
* Code Reviews done properly are an excellent low-cost method to get everyone a wide knowledge of the code base and bring all developers up to the level of the architect (as well as improving the architect).
* If you schedule down to the minute, you need to make room for process improvement. 
* Getting to a decent level of documentation allows for asynchronous work, allows for more hands to fit in the pot.
* Always start with base-line developer documentation (coding styles, build setup, high-level architecture layout). 
* Tech Leads should always code more, formalize processes and track improvements/slippages. 
* Business-owners, UX, creative and tech must by off on the requirements before a story is ready for a sprint.
* Isolation is the key to most everything. Back-end services should be stubbed first, built later.
* It's not done until a non-tech can use and understand it. 
* Leverage the strengths of QA, functional automation testing and unit testing properly to have more reliable product. The strengths of each don't overlap.
* Keep dependency gathering out of email and into a tracking system.  Periodically roll-up discussion when directions are taken to keep the ramp-up time for others people to a minimum.
* QA needs to understand and test both isolation of work and integration or work.
* everybody codes, everybody is a tech lead, everybody has input in the design/UX/services process
* Using retrospectives to subconsciously have the team filter up the main issues and constantly improve the process where it's most needed. 
* The end of sprint product demos are the key to innovation. Analyze what was done, if it should be changed/improved, reset course if necessary (by queuing up tasks for a future sprint), bring all the teams together to review the product's usefulness and 

---

# Planning Process

---

## Pre-Planning

Ad-hoc developers reviewing task documentation from creative, back-end service methods, data model and stubs and QA acceptance criteria. This is a continual process during the sprint. Until a  developer on the team signs off on all the requirements the task can not be included in the sprint.

#### Benefits
* It fills in holes in because story points aren't a 1-to-1 to time estimates.
* Distributes planning and acceptance through-out the team.
* Not planning down to the estimate level allows for a little slack to spend on process improvement.

#### Challenges
* Some developers are weaker at understanding the requirements.

---

## Planning Meeting

Tech Leads gather definitions of tasks for upcoming sprint. Only 100% locked down tasks accepted.  QA works 1 sprint ahead to write Gherkin-style acceptance tests. Design is 1 to 2 sprints ahead to create visuals and filter UX business requirements. Back-end services is 1 sprint ahead with an agreed upon service data stubbed out. Tech Lead stays in sync with QA, Creative and other Tech Leads/Project Architect.

Tech Lead goes through task details with the entire team.  The team discusses dependancies and high-level implementation. After the team feels a task is defined they give story point estimate. Outliers are sell the case for swaying the point value. Stories larger than 5 or over broken out before they can be worked on. Occasional team member swaps to level set all teams across the build process. After the team agrees that 100% of dependancies are met and stories are broken out code-able and qa test-able, developers sign-up for tasks.

Tech Leads would also in a master scrum to help level-set between teams.

#### Benefits
* level-sets the story points based on level of effort for a normal developer
* team's velocity is track-able and compared against historical
* Complete lock on visuals, functionality, services and business-level acceptance prior to starting a sprint.

#### Challenges
* Some dependancies would be found after coding started. Developer would take the lead on fulfilling the missing requirements.
* There was never an up-front place in the process to plan the architecture. This was done after the fact in the code review. I would like to try a separate team meeting to review a proposed implement by the developer who did the pre-planning on the task.

#### Happy side-effects
* developers understood a wider-range of the code base.
* this forced the tech lead to not be leading from the top but freed up to code and focused more on quality of the developers and code and less on process
* kept developers busy with planning while QA was testing near the end of the sprint.

---

## Development Phase

---

### TDD (Test-Driven Development) & Unit Testing

---

TDD was prompted but not rigorously enforced. What was enforced was that Code Completion(CC) was at 98% for the server-side page creation where back-end services would be joined with HTML/JS/CSS. Because of this insanely high metric, unit tests were required for every possible pass through the code. Unit tests were part of the build process and required to be fully isolated. Every object used in code required a mock. The mocks are injected in the setup for the test and completely makes your test separated from the rest of the code. Stubbed data needed to be created for every variant of the data that could be returned.

Controllers and models lend themselves much better to fully isolated unit testing than view code. It's almost best to forget about unit testing view code and instead lean on functional testing for views.

#### Benefits
* The selling benefit of unit testing is that your code is more reliable by creating tests for know instance. This did happen but some of the happy side-effects are where the real gains were.
* Front-end could be isolated from back-end changes and dependancies on the back-end services.
* If an end-user effecting issue comes up, then code a unit test to make sure that is fixed and doesn't happen again (because it will).

#### Challenges
* Unit testing can not cover unknown situations that developer don't predict.
* There is a large increase of time the developer spend to write tests, mocks and stub. Also rewriting tests when things change takes a lot of time.
* If unit testing isn't built into the build process the tests will never get watched and fall by the way-side.

#### Happy Side-Effects
* After 3 months of drinking the kool-aid of hard-core TDD. I reverted back to coding my unit tests after the fact.
* The biggest win is by going so in-depth in unit testing is that developer become much better. Developers see connections in code, see why and how to isolate and encapsulate functionality, pick better OO patterns, use a wider range of OO patterns. This is because it take so much "wasted" time for a developer once they get past the huge learning curve and figure out what to test, they start finding ways inside their production code to be better separated and in turn do less work in the unit test but still achieve complete isolation in the test. This did take 3 to 6 months for me to get past the how, what then the why to get there. It's a long process with a lot of grumbling and costs a lot of time. Take it on faith and do it until you've gained the respect of the code.
* I've come to rest on a mixed bag with unit testing. I ALWAYS write unit tests for risky or important code. This is code that is relying on 3rd party services, mission critical business logic, parsers or things dependent on complex state machine(like login stuff). As a project adds developers or becomes more iterative improvements, I start to solidify unit tests by enforcing mocks and stubs. If back-end services are shity then I  have the build script also rerun the back-end unit tests without the mocks/stubs and report and track the stability of back-end services. Take unit testing out for a couple sprints and see if there is an effect on your bug reports and end-user defects? If there's not a big dip you're testing the wrong things or testing too much.

---

### Living Style Guide

---

After a task has all of it's dependancies completed and approved by the team, coding starts. This is front-end development, so the result of everything is that a user can do something (something that QA/automation can test). First was building a component that the site would use. Every component would be first built in the Style Guide. 

The Style Guide is and interactive, internal website. There rare a couple main sections to the Style Guide: components, page layout (some type of grid system), application controllers. Each component would have a static image from visual with all of it's defined functionality and possible visual states. It also has an interactive one that they developer would build and code and notes to leverage this component in the future.

#### Benefits
* developers can get a quick visual lay of the parts of the application and then have sample code to leverage pieces. This builds consistency and reusability of functionality.

#### Challenges
* component and functionality developed away from the end page might if push back from QA to test and validate.
* if the item for the style guide needed to be created in the same sprint as integrating it on the page there was some additional cost of time.

#### Happy Side-effects
* it gave QA, creative, developers and business-owners a place to discuss low-level functionality on a similar platform. 
* Quicker ramp up time and more diversification about which developer to tackle task in a new part of code.
* Overall the Style Guide was a massive win project wide.
* * I would have liked to see it leveraged more and includes more to set a base-line and talk about functionality with creative/ux

---

### Page Implementation

---

The page creation back-end would retrieve data from the stubbed services. Pull in any of the components detailed in the Style Guide and any other routing/transformation of data that was needed. Server sessions should be never be used. They add lots of dependancies on the back-end's performance and threading. It also adds states which is kills concurrency and creates a lot of side-effects.

#### Benefits
* code reusability is forefront because components are separated into different tasks
* pages are 100% functional it stub data that has been agreed upon with back-end services. QA can fully test and validate that the page works. 
#### Challenges
* end-to-end regression is addressed later when the services are complete and attached to live database data. 
#### Happy side-effects
* focus on functional automation and acceptance on the end results of the page. 

---

### BDD - Functional Testing

---

After the task is complete and if there is integration into a page, then QA would have previously written acceptance tests to be complete. 
Developer would write functional behavior tests. The pass/fail of the acceptance test was added into CI which would fail if the test failed. 

#### Benefits
* using stubbed data provided a higher degree of accuracy when running functional tests in the build.  * more automation allowed for continuos regression on the entire site. 

#### Challenges
* functional tests, especially restarting the browser for each test to reset a clean slate, take a long time. 
* QA spent a lot of time writing, level-setting and fleshing out testing. 
* Developer spent a lot of time building functional test. Later using a page level and story level class structure helped cut down on CCP metric and gave better reuse ability in the BDD framework. 
* code refractors and changing visuals were more costly. 

#### Happy side-effects
* developer were better in the planning stage because they could see and add a complete list of functionality for a given item. 

---

### Code Acceptance (Code Reviews, Merging to Master)

---

After a task was completed by the developer they would make sure  all they had created the unit and behavior functional testing. Running the build script would validate code completion and run through the functional testing only for the affected session. This was for performance reasons since behavior tests should be isolated and each test would restart close and reopen the browser it could get tedious. Once a passing grade was received the developer would open a code review.

The code review would need to be linked to the documentation of the back-end services, visual/UX and anything else pertinent. The code would need to be accepted by 1 official code reviewer (approved by the architect) and 2 nonofficial code reviewers. Official code reviewers frequently had the architect review their code as well.

If the code was reject, it would be refactored according to notes in the code review and a new review would be opened. After the code review was accepted, along with a review of the unit test and behavior test the code was allowed into the master branch. If the unit test or behavior test wasn't completed a code review could still be opened for the main task to be in the review process while the developer was working to complete the task. QA testing also was not dependent on code being into the main branch. Since QA was testing functionality of a feature on the page it is separate from end-to-end and regression testing.

#### Benefits
* Non-performant code almost never made it into the release.
* Proper application of OO patterns was enforced.
* Massive amounts of tech debit was averted. Sometimes causing a developer to completely re-write his task mid-sprint.
* The coding style guide document would be continuously updated when new items were addressed in code reviews.
* Have a tool is CRITICAL. Tracking commits and being able to work asynchronously is critical.
* Developers will fill up more end-of-sprint time doing code reviews and understanding a wider base of the application as well ad being able to be critical about the application of other developers OO patterns.
  
#### Challenges
* No architectural planning structure lead to ad-hoc discussions and in the worse cause a developer would be scrabbling to re-factor his entire code at the tail end of a sprint.
* Sometimes an official code reviewer were hard to come by. 

#### Happy side-effects
* Code reviews disseminate best practices from the architect down to all the developers. This is a massive win. It brings up the code of the entire team up very quickly and almost acted as a proxy for the architect coding the entire site himself.
* This was a massive win for getting developers to talk about if they made the right OO design decisions and self-educate the group with tips and tricks.
* commented code, magic numbers, anti-patterns and progressively slipping code quality was almost eliminated.

---

### Testing and Acceptance Cycle

---

QA creates gherkin-style acceptance testing that is agreed upon with development prior to accepting a task into the sprint. Acceptance criteria is defined prior to a task being accepted in a sprint. 

Generally QA starts a sprint by creating acceptance criteria for the upcoming sprint. At the end of the sprint developer are freed up to review acceptance criteria and either accept or work with the QA to agree on modifications to the tests. 

The second week of the sprint QA is switching focus more to manual testing and regression on the features for the current sprint. During this time developer are wrapping up coding the functionality and focusing more on code reviews, writing the BDDs for the acceptance test and reviewing all the do do documentation for the upcoming sprint. 

#### Benefits 
* having acceptance criteria prior to task acceptance allows for a deeper understanding and exposes more details for the developer to make a better assessment that all dependencies have been completed. 
* acceptance tests also spend the work on the QA more evenly when it tends to cluster into a mad dash and frequent overtime at the end of a sprint. 

#### Challenges
* regressions are a little for sparse while QA is focusing time on creating the acceptance. 
* lots of time is spent writing automated testing a d there is not a counter-factual to judge their worth or what is a comparable level of automation. 

#### Happy side-effects
* QA has a much deeper understanding of what they are testing, what should and shouldn’t be automated and have a better working communication with development. 

---

### Continuous Integration

#### Benefits
#### Challenges
#### Happy side-effects

---

### Build Script

#### Benefits
#### Challenges
#### Happy side-effects

---

### Design Life-Cycle

#### Benefits
#### Challenges
#### Happy side-effects

---

### Business Owner Buy-off (Product Demo)

#### Benefits
#### Challenges
#### Happy side-effects

---

### Continual Tracked Improvement

---

Retrospectives are a key part of agile that should NEVER be left out. A key part of Agile is continuos improvement. Retrospectives are the only point where the team has an formalized open forum to bring up grievances and breaks in the process.

Our retrospectives started by having one developer say one thing that was good and everything bad that came up during the sprint. It would go around the room until all developers had a chance to bring up any issues. It worked best when developers would track issues during the sprint and be able to shotgun through their list in the meeting. Then there would be another pass around for developer to +1 on any task that was a big issue on the sprint. 

The top 3 or 4 items usually would be brought out and discussed until there was something actionable that could happen. One person would volunteer to be the owner of the issue and work towards improvements during the following sprint. 

Retrospectives were tracked and shared across teams. They would also receive a bullet point in the stack holder demo review meeting. It would cover main issues on the teams and what had been improvements had been taken from last sprint. No actions are carried or tracked on past sprint until an item had re-appeared in the current sprint's retrospective.

#### Benefits
* Without triaging issues and taking actions to improve the process there is no Agile
* Continuos self-analysis by everyone.
* Constant incremental improvement on the process. Re-weighting the costs of some process with the rewards.

#### Challenges
* There are many ways to do retrospectives. Going through different techniques and analyzing the strengths and weaknesses of the techniques will create better triaging of the issues.
* Having a well-trained leader for the retrospective is important in getting the most of out it.

#### Happy side-effects
* The implementation of this technique in this manner breeds a wonderful subconscious agreement on what is most critical to fix and what should be done to attempt to fix it.
* It focused on collaboration with no discussion. Only having one person talking and the leader of the meeting writing down the items (almost not having to say anything), and giving other team members a change to reflect and think about the impacts. This turns the tech lead from a director controlling everything into creating an environment and opportunity where the team can collectively rise.

---

### Story Lifecycle

---

Stories typically because with the business owner having a problem that needs a solution in the project. Generally it is UX related and goes to the creative team to address. Creative works through the problem and solution with open communication between developers. They will be working on stories anywhere from 1 to 5 sprints ahead of development. 
Once creative has a solution the visuals are approved by the business owner. The 

#### Benefits
#### Challenges
#### Happy side-effects

---

# Sample of a good sprint encapsulation 

---

* All testing for the tasks in the sprint must be completed in the sprint.
* There must be something useable by the end-user as a result of the sprint.
* Separating testing functionality with stubbed data and true end-to-end helps keep QA active and spreads their work better across the sprint.

<table border=0 cellpadding=0 cellspacing=0 width=100% style='border-collapse: collapse;table-layout:fixed;width:100%'> <col width=212 style='mso-width-source:userset;mso-width-alt:9045;width:212pt'> <col width=65 span=10 style='width:65pt'> <tr height=42 style='mso-height-source:userset;height:42.0pt'><td height=42 width=212 style='height:42.0pt;width:212pt'></td><td class=xl65 colspan=3 width=195 style='mso-ignore:colspan;width:195pt'>Sample2 week Sprint cadance</td><td width=65 style='width:65pt'></td><td width=65 style='width:65pt'></td><td width=65 style='width:65pt'></td><td width=65 style='width:65pt'></td><td width=65 style='width:65pt'></td><td width=65 style='width:65pt'></td><td width=65 style='width:65pt'></td> </tr> <tr height=20 style='height:20.0pt'><td height=20 class=xl66 style='height:20.0pt'>Developers</td><td colspan=10 style='mso-ignore:colspan'></td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt'>days</td><td class=xl68>1</td><td class=xl68>2</td><td class=xl68>3</td><td class=xl68>4</td><td class=xl68>5</td><td class=xl68>6</td><td class=xl68>7</td><td class=xl68>8</td><td class=xl68>9</td><td class=xl68>10</td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt;border-top:none'>reviewingrequirements</td><td class=xl69>50%</td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl69>10%</td><td class=xl69>20%</td><td class=xl69>30%</td><td class=xl69>10%</td><td class=xl69>30%</td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt;border-top:none'>coding</td><td class=xl69>50%</td><td class=xl69>100%</td><td class=xl69>100%</td><td class=xl69>100%</td><td class=xl69>100%</td><td class=xl69>60%</td><td class=xl69></td><td class=xl70></td><td class=xl70></td><td class=xl70></td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt;border-top:none'>code hardening(testing/bug fixing)</td><td class=xl70></td><td class=xl69></td><td class=xl69></td><td class=xl69></td><td class=xl69></td><td class=xl69></td><td class=xl69></td><td class=xl69>40%</td><td class=xl69>60%</td><td class=xl69>60%</td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt;border-top:none'>code reviews</td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl69>10%</td><td class=xl69>60%</td><td class=xl69>30%</td><td class=xl69>30%</td><td class=xl70></td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt;border-top:none'>behaviortesting</td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl69>20%</td><td class=xl69>20%</td><td class=xl70></td><td class=xl70></td><td class=xl70></td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt;border-top:none'>planningmeeting (w/ QA and creative)</td><td class=xl70>x</td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt;border-top:none'>retrospective(w/ QA)</td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70>x</td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt;border-top:none'>scrum</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td> </tr> <tr height=48 style='mso-height-source:userset;height:48.0pt'><td height=48 class=xl66 style='height:48.0pt'>QA</td><td colspan=10 style='mso-ignore:colspan'></td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt'>days</td><td class=xl68>1</td><td class=xl68>2</td><td class=xl68>3</td><td class=xl68>4</td><td class=xl68>5</td><td class=xl68>6</td><td class=xl68>7</td><td class=xl68>8</td><td class=xl68>9</td><td class=xl68>10</td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt;border-top:none'>accectanceplanning for future sprint</td><td class=xl69>50%</td><td class=xl69>100%</td><td class=xl69>100%</td><td class=xl69>50%</td><td class=xl69>50%</td><td class=xl70></td><td class=xl69></td><td class=xl69></td><td class=xl69></td><td class=xl69></td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt;border-top:none'>Testing/creating bugs</td><td class=xl70></td><td class=xl69></td><td class=xl69></td><td class=xl69>50%</td><td class=xl69>50%</td><td class=xl69>100%</td><td class=xl69>100%</td><td class=xl69>100%</td><td class=xl69>100%</td><td class=xl69>100%</td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt;border-top:none'>retrospective(w/ QA)</td><td class=xl70>x</td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt;border-top:none'>retrospective</td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70></td><td class=xl70>x</td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt;border-top:none'>acceptance/validationof task completion</td><td class=xl71></td><td class=xl71></td><td class=xl71></td><td class=xl71></td><td class=xl71></td><td class=xl71></td><td class=xl71></td><td class=xl71></td><td class=xl70>x</td><td class=xl70>x</td> </tr> <tr height=15 style='height:15.0pt'><td height=15 class=xl67 style='height:15.0pt;border-top:none'>scrum</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td><td class=xl70>x</td> </tr></table>

---

# Are you doing it right? 

---

* Do your developers and testers ALWAYS leave on time?
* Are you becoming more constant with completing the task agreed upon for the sprint?
* Do you have some free time to work on improving the process?
* Are you triaging properly? When you spend time changing something on process does it make developers, testers, creative, business owners and end users happier?
* Do you have anything metric'ed and tracked cross sprint? (If you're not then give an SLA to the business owner that gets a bullet point in the product demo)
* Is there enough pain when someone fails to follow and improve the process?
* How can you show you're improving something unless it's tracked or documented?
