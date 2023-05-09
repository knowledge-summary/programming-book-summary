# Software Engineering at Google: Lesson Learned from Programming Over Time - by Titus Winters, Tom Manshreck, Hyrum Wright

# Chapter 1: What is Software Engineering
Three critical differences between programming and software engineering - time, scale and the trade-offs at play.

The most important lessons about 'it works' and 'it is maintainable' is what we've come to call Hyrum's Law.
> With a sufficient number of users of an API, it does not matter what you promise in the contract: all observable behaviors of your system will be depended on by somebody.

Factors that affect the flexibility of a codebase
- Expertise
- Stability
- Conformity
- Familiarity
- Policy

Shifting left - Shifting problem detection to the “left” earlier on this timeline makes it cheaper to fix than waiting longer.

Costs
- Financial costs (money)
- Resource costs (CPU)
- Personnel costs (engineering efforts)
- Transaction costs (costs to take action)
- Opportunity costs (costs to not take action)
- Societal costs (How a choice impact society at large?)

The Beyoncé Rule - If you liked it, you should have put a CI test on it

Jenvons Paradox - consumption of a resource may increase as a response to greater efficiency in its use.


# Chapter 2: How to Work Well on Teams
People are afraid of others seeing and judging their work in progress. Many humans have the instinct to find and worship idols.

Bus factor (noun): the number of people that need to get hit by a bus before your project is completely doomed.

Three pillars of social interactions
- Humility
- Respect
- Trust

Blameless Post-Mortem Culture
- A brief summary of the event
- A timeline of the event, from discovery through investigation to resolution
- The primary cause of the event
- Impact and damage assessment
- A set of action items (with owners) to fix the problem immediately
- A set of action items to prevent the event from happening again
- Lessons learned

Googleyness
- **Thrives in ambiguity** - Can deal with conflicting messages or directions, build consensus, and make progress against a problem, even when the environment is constantly shifting.
- **Values feedback** - Has humility to both receive and give feedback gracefully and understands how valuable feedback is for personal (and team) development.
- **Challenges status quo** - Is able to set ambitious goals and pursue them even when there might be resistance or inertia from others.
- **Puts the user first** - Has empathy and respect for users of Google’s products and pursues actions that are in their best interests.
- **Cares about the team** - Has empathy and respect for coworkers and actively works to help them without being asked, improving team cohesion.
- **Does the right thing** - Has a strong sense of ethics about everything they do; willing to make difficult or inconvenient decisions to protect the integrity of the team and product.

# Chapter 3: Knowledge Sharing
Challenges to Learning
- **Lack of psychological safety**  
An environment in which people are afraid to take risks or make mistakes in front of others because they fear being punished for it. This often manifests as a culture of fear or a tendency to avoid transparency.
- **Information islands**  
  Knowledge fragmentation that occurs in different parts of an organization that don’t communicate with one another or use shared resources. In such an environment, each group develops its own way of doing things. This often leads to the following:
    - *Information fragmentation*  
      Each island has an incomplete picture of the bigger whole.
    - *Information duplication*  
      Each island has reinvented its own way of doing something.
    - *Information skew*  
      Each island has its own ways of doing the same thing, and these might or might not conflict.
- **Single point of failure (SPOF)**  
  A bottleneck that occurs when critical information is available from only a single person. This is related to bus factor.  <br><br>
  SPOFs can arise out of good intentions: it can be easy to fall into a habit of "Let me take care of that for you." But this approach optimizes for short-term efficiency ("It's faster for me to do it") at the cost of poor long-term scalability (the team never learns how to do whatever it is that needs to be done). This mindset also tends to lead to all-or-nothing expertise.
- **All-or-nothing expertise**  
  A group of people that is split between people who know "everything" and novices, with little middle ground. This problem often reinforces itself if experts always do everything themselves and don’t take the time to develop new experts through mentoring or documentation. In this scenario, knowledge and responsibilities continue to accumulate on those who already have expertise, and new team members or novices are left to fend for themselves and ramp up more slowly.
- Parroting  
  Mimicry without understanding. This is typically characterized by mindlessly copying patterns or code without understanding their purpose, often under the assumption that said code is needed for unknown reasons.
- Haunted graveyards
  Places, often in code, that people avoid touching or changing because they are afraid that something might go wrong. Unlike the aforementioned parroting, haunted graveyards are characterized by people avoiding action because of fear and superstition.

Software engineering can be defined as the multiperson development of multiversion programs.

Type of knowledge sharing
- One-to-one advice from the expert
- Documented knowledge
- Community
  - Group sharing
  - Mailing list
  - YAQS (Yet Another Question System)

Setting the stage: Psychological safety

[Recurse Center's social rules](https://www.recurse.com/manual#sub-sec-social-rules)
- **No feigned surprise** (What?! I can't believe you don't know ...) - Feigned surprise is a barrier to psychological safety and makes members of the group afraid of admitting to a lack of knowledge.
- **No 'well-actuallys"** - Pedantic corrections that tend to be about grandstanding rather than precision.
- **No back-seat driving** - Interrupting an existing discussion to offer opinions without committing to the conversation.
- **No subtle "-isms"** - Small expressions of bias (racism, ageism, homophobia) that can make individuals feel unwelcome, disrespected, or unsafe.

[Chesterson’s fence](https://en.wikipedia.org/wiki/Wikipedia:Chesterton's_fence): before removing or changing something, first understand why it’s there.

Ways of teaching
- Office hours
- Giving tech talks
- Teaching classes
- Writing documentation
- Reviewing code

Culture is important at every stage of growth.

Peer bonuses are a monetary award and formal recognition that any Googler can bestow on any other Googler for above-and-beyond work.

Similar to peer bonuses are kudos: public acknowledgement of contributions (typically smaller in impact or effort than those meriting a peer bonus) that boost the visibility of peer-to-peer contributions.

go/links are Google's internal URL shortener.

Code review is mandatory at Google. Every changelist (CL)18 requires **readability** approval, which indicates that someone who has readability certification for that language has approved the CL.


# Chapter 4: Engineering for Equity
Bias is the default. Unconscious bias is insidious and often more difficult to mitigate than intentional acts of exclusion.

Engineers should focus on people who are different than themselves, especially people who might attempt to use their products to cause harm.

There is an enormous amount of individualism that goes into being a high-performing engineer. Yet to succeed, we must extend our focus beyond our own communities to the next billion users or to current users who might be disenfranchised or left behind by our products.

It’s critical that on your journey to becoming an exceptional engineer, you understand the innate responsibility needed to exercise power without causing harm. The first step is to recognize the default state of your bias caused by many societal and educational factors. After you recognize this, you’ll be able to consider the often-forgotten use cases or users who can benefit or be harmed by the products you build.

Making diversity actionable.

A common methodology today is to build for the majority use case first, leaving improvements and features that address edge cases for later. But this approach is flawed; it gives users who are already advantaged in access to technology a head start, which increases inequity. Relegating the consideration of all user groups to the point when design has been nearly completed is to lower the bar of what it means to be an excellent engineer. Instead, by building in inclusive design from the start and raising development standards for development to make tools delightful and accessible for people who struggle to access technology, we enhance the experience for all users.

Ratings, although an important way to measure performance during a specific period, are not predictive of future performance and should not be used to gauge readiness for a future role or qualify an internal candidate for a different team.

1. Take a hard look in the mirror. 
2. Don’t build for everyone. Build with everyone.
3. Design for the user who will have the most difficulty using your product.
4. Don’t assume equity; measure equity throughout your systems.
5. Change is possible.


# Chapter 5: How to Lead a Team
A piece of software is just like that boat: if no one pilots it, you’re left with a group of engineers burning up valuable time, just sitting around waiting for something to happen (or worse, still writing code that you don’t need).

Two leadership roles in Google
- Manager - leader of people
- Tech Lead - leads technogy efforts

Can be the same person - Tech Lead Manager (TLM)

The people skills required to succeed in each role is wildly different.

Engineering Manager
- In Google, they are required to have engineering background
- Responsible for performance, productivity, and happiness of every person on the team

Tech Lead (TL)
- Responsible for the technical aspect of the product, including technology decisions and choices, architecture, priorities, velocity and general project management
- Work with engineering manager to ensure that the team is adequately stuffed for their product and that engineer are set to work on tasks that best match their skill sets and skill levels

Tech Lead Manager (TLM)
- A single person who can handle both the people and technical needs of their team (more often taken by an individual contributor)
- Tricky role and require balance individual work, delegation and people management
- Mentoring and assistance from more experienced TLMs


Influence without Authority - Get people outside of your organization—or heck, even outside of your product area sometimes—to do something that you think needs to be done.

Reasons people avoid management role
- Spend much less time writing code
- Achievement can be less tangible/visible
- Peter Principle - In a hierarchy, every employee tends to rise to his level of incompetence

Greats reasons to consider becoming a TL/manager
- A way to scale yourself
- You might just be really good at it

> "Above all, resists the urge to manage." - Steve Vinter, an engineering director from Google

Servant leadership - the most important thing you can do as a leader is to serve your team (The cure for the "management" disease)
- Remove bureaucratic obstacles that a team member can't remove by themselves
- Helping the team achieve consensus
- Buying dinner for the team when they are working late at the office

If a manager makes it obvious that they trusts the employee, the employee feel the positive pressure to live up to that trust. A good manager forges the way for a team, looking out for their safety and well-being, all while making sure their needs are meet.

> Traditional managers worry about how to get things done, whereas great managers worry about what things get done (and trust their team to figure out how to do it).

- Don't babysit
- Building psychological safety for risk taking
    > If you try to achieve an impossible goal, there’s a good chance you’ll fail, but if you fail trying to achieve the impossible, you’ll most likely accomplish far more than you would have accomplished had you merely attempted something you knew you could complete


Antipatterns/Characteristics of bad managements include
| Antipatterns | Description | What should be done |
| --- | --- | --- |
| **Hire pushovers** | Hire people you can push around, cement your position but mean more works for you to guide | Strive to hire people who are smarter than you and can replace you. They will consistently impress you and make great things happen. |
| **Ignore low performers** | Most difficult cases to handle are when someone just isn't capable of doing their job no matter how long or hard they work. It will drag the high performer and reduce team morale | Put yourself in the position of helping them up or out. Oftentimes, they merely need some encouragement or direction to slip into a more productivity. It almost always requires temporary micromanagement, but still a whole lot of humility, respect, and trust—particularly respect. |
| **Ignoring human issues** | There are two major areas of focus for the team: the social and the technical | Being more empathy and don't be a jerk | 
| **Be everyone's friend**  | Don’t confuse friendship with leading with a soft touch: when you hold power over someone’s career, they might feel pressure to artificially reciprocate gestures of friendship. If the friend who is being managed is not self-managing and is not a hard worker, it can be stressful for everyone. | You can be a tough leader without tossing your existing friendships to the wind. Having lunch with your team can be an effective way to stay socially connected to them without making them uncomfortable |
| **Compromise the hiring bar** | The cost of finding the appropriate person pales when compare with the cost to deal with bad hire. Steve Jobs once said: "A people hire other A people; B people hire C people." | Ensure the candidates meet the hiring bar |
| **Treat your team like children** | People tend to act the way you treat them, so if you treat them like children or prisoners, don’t be surprised when that’s how they behave. You can manifest this behavior by micromanaging them or simply by being disrespectful of their abilities and giving them no opportunity to be responsible for their work. | If you hire people worthy of trust and show these people you trust them, they’ll usually rise to the occasion. |

Positive patterns
- **Lose the ego** 
  - There is a fine line between being humble and letting others take advantage of you. You can still have self-confidence and opinions without being an egomaniac.
  - Trust and avoid micromanage
  - Encourage inquiry and constructive criticism
  - Apologize when you make a mistake
- **Be a zen master**
  - Be less vocally skeptical while still letting your team know you're aware of the intricacies and obstacles involved in the work
  - Mediating your reactions and maintaining your calm
  - Your team will consciously and subconsciously look to you for clues on how to react
  - Zen management trick: asking questions. Help the person to solve the problem on their own by trying to refine and explore the problem.
- **Be a catalyst**
  - Build consensus, drive the process from start to finish, give a gentle push to the right direction
- **Remove roadblocks**
  - Jump in to help the team remove technical or organizational roadblocks
  - In many cases, knowing the right person is more valuable than knowing the right answer
- **Be a teacher and a mentor**
  - Teaching people and giving them a chance to learn on their own can be incredibly difficult at first, but it’s a vital component of effective leadership
  - This is especially important for new hires who, in addition to learning your team’s technology and codebase, are learning your team’s culture and the appropriate level of responsibility to assume.
  - Three things needed
    - Experience with your team’s processes and systems
    - The ability to explain things to someone else
    - The ability to gauge how much help your mentee needs
- **Set clear goals**
  - If you’re going to have clear goals, you need to set clear priorities and help your team decide how it should make trade-offs when the time comes.
  - Create a concise mission statement for the team, step back and give it more autonomy, periodically checking in to make sure everyone is still on the right track.
- **Be honest**
  - Sometimes you can't tell your team something, or need to tell everyone something they don't want to hear, or simply don't know
  - Using "compliment sandwich" to soften the blow when giving criticise might make people not hearing the critical message
  - Instead, be kind and empathetic when delivering constructive criticism. Give clear feedback and direction.
- **Track happiness**
  - Example
    - Makes a spreadsheet of all the grungu, thankless tasks that need to be done and split them evenly across the team
    - Watch the hour worked, uses comp time and fun team outings to avoid burnout and exhaustion
    - One-on-one session to deal with technical issues, make sure that everything needed are prepared, talks about how they're enjoying the work
  - Ask "What do you need?" to make sure that each team member has what they need to be productive and happy.

## Where you see your career in five years
Usually people won't say much about this.

There are usually a few things that everyone would like to do in the next five years
- Be promoted
- Learn something new
- Launch something important
- Work with smart people

Effective leader should be thinking how they can make these happen. Take these implicit goals and make them explicit so that when you're giving career advice, you have a real set of metrics with which to evaluate situations and opportunities.

## Other tips and tricks
- Delegate, but get your hands dirty
  - Gain respect by taking on a grungy task that no one else wants to do.
- Seek to replace yourself
- Know when to make waves
- Shield your team from chaos
- Give your team air cover
- Let your team know when they're doing well
- It's easy to say "yes" to something that's easy to undo

People are like plants, they need varying amount of motivation and direction. Motivate the one in the rut, provide stronger direction to those who are distracted or uncertain of what to do.

There are two types of motivation: extrinsic (such as monetary compensation) and intrinsic, which comes from within.

To increase the intrinsic motivation, give people three things: autonomy, mastery and purpose.


# Chapter 6: Leading at Scale
Your effectiveness depends more than ever on your general technical intuition and ability to galvanize engineer to move in a good direction.

"The Three Always of Leaderships": **Always be deciding, always be leaving, always be scaling**

## Always be deciding
Three steps:
1. Identify the blinder (discover bizarre coping mechanisms or rationalizations that evolved to justify the status quo)
2. Identify the trade-offs (leave a trail of self-sufficient success)
3. Decide and iterate on a solution

Analysis paralysis: fall into trap of finding the perfect solution.

Instead, make your teams comfortable with iteration.

## Always be leaving

Being a successful leader means building an organization that is able to solve the difficult problem by itself.

Silicon Valley has well-known mantras about "falling fast and iterating". It doesn't just apply to engineering design, but to human learning as well.

What can I do that nobody else on my team can do?
- Protect your team from organizational politics
- Give encouragement
- Make sure everyone treating others well
- Manage up - make sure your management chain understand what your group is doing
- Define a high-level strategy

What good management is about: 95% observation and listening, 5% making critical adjustments in just the right place

Anchoring team's identity to a general problem, instead of a specific product.

## Always be scaling
The cycle of success
- Analysis
- Struggle 
- Traction
- Reward

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781492082781/files/assets/seag_0602.png)

As you moved into leadership, your job became less proactive and more reactive.

Key techniques
- Delegate
- Schedule dedicated time
- Find a tracking system that works

Important vs urgent

Dropping ball

Declutter abstract clutter. 

Think of your physical possessions as living in three piles
- About 20% of your things are useless
- About 60% are somewhat interesting and vary in importance
- About 20% are exceedingly important

Instead of identifying the bottom 20%, you should instead identifying the top 20%. First, even if you don't delegate the middle 60%, your subleaders often notice and pick them up automatically. If that middle bucket is truly critical, it will end up in the 20% bucket.

Protecing your energy
- As you grow older, your overall stamina build up.
- Leader gradually learn to manage their energy more intelligently
- Take real vacation
- Make it trivial to disconnect (disable/remove work related tools)
- Take real weekends
- Take breaks during the day
- Give yourself permission to take a mental health day


# Chapter 7: Measuring Engineering Productivity
To increase the scope of business, you can
- add more people
- make each individual more productive

Adding more people will be necessary to increase the scope of your business, but the communication overhead costs will not scale linearly as you add additional personnel.

Google has a team of researchers dedicated to understanding engineering productivity.
- Personal motivation
- Incentive structures
- Strategies for managing complex tasks

Before measuring, we need to know if a metric is even worth measuring. In Google, we comes out with a series of questions to help teams determine.
- What results are you expecting, and why?
- If the data supports your expected result, what action will be taken?
- If we get a negative result, will appropriate action be taken?
- Who is going to decide on take action on the result, and when would they do it?

Some good reasons to not continue with the measurement
- You can't afford to change the process/tools right now
- Any results will soon be invalidated by other factors
- The result will be used only as vanity metrics to support something you were going to do anyway
- The only metrics available are not precise enough to measure the problem and can be confounded by other factors

After we decide to measure a software process, we need to determine what metrics to use. At Google, we use Goals/Signals/Metrics (GSM) framework to guide metric creation.
- Goal: desired end result
- Signal: how you know that you've achieved the end result
- Metric: Proxy for signal that can be measure

Using GSM framework prevents the streetlight effect, prevent metric creep and metric bias, show us where we have measurement coverage.

Streetlight effect: if you look only where you can see, you might not be looking in the right place.

The Google research team divides productivity to five components with mnemonic "QUANTS"
- Quality of the code
- Attention from engineers
- Intellectual complexity
- Tempo and velocity
- Satisfactory

# Chapter 8: Style Guides and Rules
To manage codebase, Google maintain a set of style guide that define the rules. Each language has a style arbiter to manage.

As an organization grows, the established rules and guidelines shape the common vocabulary of coding. A common vocabulary allows engineers to concentrate on what their code needs to say rather than how they’re saying it.

Overarching principles that guide the development of style guide
- Pull their weight
- Optimize for reader (aim for local reasoning)
- Be consistent
- Avoid error-prone and surprise constructs
- Concede to practicalities when necessary

Advantage of consistency
- Help readers focus on what's getting done rather than how it is presented.
- Enable scaling 
- Ensure resilience to time

Be consistent starts locally.

What goes into style rules:
- Rules to avoid danger (some language features have nuanced usage patterns that might not be intuitive or easy to apply properly)
- Rules to enforce best practices (such as comment, project structure, naming)
- Rules to enforce consistency (such as naming convention, indentation, import ordering)

In addition to rules, we curate programming guidance in various forms. Guidance represents the collected wisdom of our engineering experience, documenting the best practices that we’ve extracted from the lessons learned along the way.

Automated enforcement of rules if possible. However,
- Some technical rules explitcitly call for human judgement
- Other rules are social rather than technical (such as what is considered as small commit)


# Chapter 9: Code Review
Code review is the process in which code is reviewed by someone other than the author, often before the introduction of that code into a codebase, the stage is called *precomit review*. The implementation vary across the software industry.

Google uses a custom tool called Critique to do code review. 

The end goal of a code review is to get another engineer to consent to the change, which we denote by tagging the change as "look good to me" (LGTM).

Typical code review workflow
1. Write changes, submit to code review tool.
2. Self review, afterwards mail the change and notify the reviewers.
3. Reviewers post comments.
4. Author modifies the change, upload and replies back to the reviewers. Step 3 and 4 may be repeated multiple times.
5. Reviewers agree and accept by marking "LGTM".
6. Author commit the change.

Code is a liability. It is a maintenance task for someone somewhere down the line. Like the fuel of airplane, have weight, and necessary for airplane to fly.

There are three aspects of reviews that require approval (can be by same person)
- A correctness and comprehension check that the code does what the author claims it does
- Approval from code owner of a particular codebase
- Approval from someone with language "readability"

Most code reviews that require more than one approval usually go through a two-step process: gaining an LGTM from a peer engineer, and then seeking approval from appropriate code owner/readability reviewer(s). This allows the two roles to focus on different aspects of the code review.

Splitting reviews to different components help with scaling.

Code review is a mandate, one of the few blanket process that each software engineer in Google need to participate.

Benefits of well-designed code review process and a culture of taking code review seriously
- Check code correctness
- Ensure the code change is comprehensible to other engineers
- Ensure code consistency across the codebase
- Psychologically promote team ownership
- Enables knowledge sharing
- Provides a historical record of the code review itself

Code review processes that are heavyweight, or that don’t scale properly, become unsustainable. Authors are given deference to their particular approach, reviewer can propose alternatives only if they improve comprehension or functionality.

In Google, we expect feedback from a code review within 24 (working) hours.

Core reviews best practices
- Be polite and professional
- Write small changes (limited to about 200 lines of code)
- Writ good change descriptuons
- Keep reviewers to a minimum
- Automate when possible

Different types of code reviews
- Greenfield reviews and new feature development
- Behavioural changes, improvements and optimizations
- Bug fixes and rollbacks
- Refactorings and large-scale changes


# Chapter 10: Documentation
The key to making it easier for engineer to write quality documentation is to introduce processes and tools that scale with the organization and that tie into their existing workflow.

At Google, our most successful efforts have been when documentation is treated like code and incorporated into the traditional engineering workflow, making it easier for engineers to write and maintain simple documents.

Main pain point: the benefit of documentation isn't immediate

Documentation helps to answer
- Design decisions
- Implementation reasoning

Benefits of documentation
- Help formulate the API and reevaluate design decisions
- Road map for maintenance and a historical record
- Makes your code look more professional and drive traffic
- Prompt fewer questions from other users

Document is just a different language, called English. Documents should have owner.

There is also canonical documentation, acting as the source of truth. (eg: "go/links" at Google)

Your documentation should
- Have internal policies or riles to be followed
- Be place under source control
- Have clear ownership responsible for maintaining the dics
- Undergo reviews for changes (and change with the code it documents)
- Have issues tracked, as bugs are tracked in code
- Be periodically evaluated (tested, in some respect)
- If possible, be measured for aspects such as accuracy, freshness, etc. (tools have still not caught up here)

Google started with own internal wiki (GooWiki), all engineers shared the single documentation set and could update it if needed.

Move important documentation under version control. Introduce markdown as a common documentation formatting language.

Google introduced its own framework for embedding documnetation within code: g3doc.

## Audience
Identify the audiences of your documentation.

Consideration 1:
- Experience level
- Domain knowledge
- Purpose

Consideration 2:
How a user encounter a documentation
- **Seekers** are engineers who know what they want and want to know if what they are looking at fits the bill (key: consistency)
- **Stumblers** might not know exactly what they want (key: clarity)

Consideration 3:
- Customer (such as user of API)
- Provider (such as member of proejct team)

Keep your documentation short. Write descriptively enough to explain complex topics to people unfamiliar with the topic, but don’t lose or annoy experts. Can have separate documentation for different audiences.

## Types of Documentation
It is important to know the different types of documentation, and to not mix types. A document should have a singular purpose, and stick to it.

Main types of documentation:
- Reference documentation (anything that document the usage of code within the codebase)
  - File comments
  - Class comments
  - Function comments (starts with declarative verb. A single sentence can be enough, Google didn't find it necessary to have boilerplate session like 'Returns', 'Throws')
- Design documents (require approval before starting work on any major work, cover aspects such as security implications, internationalization, storage requirements, privacy concerns. A good design documents cover goal, implementation strategy and key design decisions. Can be used to measure whether a project achieve its goals)
- Tutorials (each step should be an action that the user need to take)
- Conceptual documentation (mean to augment instead of replace reference documentation)
- Landing pages (serve as a traffic cop)

## Review a Documentation
A technical document benefits from three different types of reviews
- A technical review, for accuracy
- An audience review, for clarity
- A writing review, for consistency

## Documentation Philosophy 
- Answer who, what, when, where, why
- Having more sessions help breaking down the flow into logical pieces
- Redudancy can be useful in documentation

The parameters of good documentation: completeness, accuracy and clarity.

A "good document" is the document that is doing its intended job.

In Google, we attach "freshness date" to documentation. Email will be sent when the document hasn't been touched in, for example, three months.


# Chapter 11: Testing Overview
Why do you need testing?
- Catching bugs
- Support the ability to change
- Improve the design of the system

Test suite is a collection of simple tests. As test suite grows, it will begin to face challenges like instability and slowness. A bad test suite can be worse than no test suite at all.

Automating test consists of three activities
- Writing tests
- Running tests
- Reacting to test failures

Healthy automated testing culture
- Encourage everyone to share the work of writing tests
- Ensure that tests are run regularly
- Fixing broken tests quickly to maintain high confidence

Benefits of testing
- Less debugging
- Increased confidence in changes (encourage refactoring)
- Improved documentation
- Simpler reviews
- Thoughtful design
- Fast, high quality releases

Most important qualities we want from our test suite are speed and determinism.

Test size
- Small test run in a single process
  - Run on a single thread
  - Can't run a server or database
  - Not allowed to sleep, perform I/O operations, make any other blocking calls
  - Not allowed to access network or disk
- Medium test run on a single machine
  - Not allowed to make networks call to any system other than localhost
- Large test run whatever they want

> Software provides many sources of nondeterminism: clock time, thread scheduling, network latency, and many more. It can also tied to low level concerns such as hardware interrupts or browser rendering engines. A good automated test infrastructure should help engineers identify and mitigate any nondeterministic behavior.

All test should strive to be hermatic: a test should contain all of the information necessary to set up, execute, and tear down its own environment. There should assume as little as possible about the outside environment.

A test should contain only the information required to get expected behaviour. Keep test clear and simple

Test scope
- **Narrow-scoped tests (unit tests)** - test individual class or method
- **Medium-scoped tests (integration tests)** - verify interactions between a small number of components
- **Large-scoped test (functional tests, end-to-end tests, or system tests)** - validate the interaction of several distinct parts of the system, or emergent behaviors that aren’t expressed in a single class or method.

Google aims to have a mix of around 80% narrow-scoped, 15% medium scoped and 5% end-to-end tests. The mix of tests is determined by two primary goals: engineering productivity and product confidence.

Antipatterns
- "Ice cream cone"
- "Hourglass"

The Beyoncé Rules - "If you liked it, then you shoulda put a test on it."

What actually need to be tested? Straightforward answer: test everything that you don’t want to break.

A usual suspects include 
- performance
- behavioural correctness
- accessibility
- security
- failure handling (shouldn't be ignored)

**Code coverage** is a measure of which lines of feature code are exercised by which tests. If you have 100 lines of code and your tests execute 90 of them, you have 90% code coverage. It is a proxy to answer the question "do we have enough tests?" and should be used mindfully.

Most of Google’s code is kept in a single, monolithic repository. We have more than two billion lines of code in the repository today. Google’s codebase experiences close to 25 million lines of change every week. Roughly half of them are made by the tens of thousands of engineers working in our monorepo, and the other half by our automated systems, in the form of configuration updates or large-scale changes.

Another thing that makes Google a little different is that almost no teams use repository branching. All changes are committed to the repository head and are immediately visible for everyone to see. Furthermore, all software builds are performed using the last committed change that our testing infrastructure has validated. One of the key components of our CI system is our Test Automated Platform (TAP).

Friction
- Brittle tests (Overspecify expected outcome, rely on extensive and complicated boilerplate)
- Slow tests
- Not deterministic

Google volunteer - Testing Grouplet

Three key initiatives that help usher automated testing:
- Orientation Classes (to introduce testing to new hires)
- Test Certified Program (a five-level program with concrete action to improve code hygiene on the team)
- Testing on the Toilet (TotT)

Today, as a the replacement for Test Certified, one of our engineering productivity teams recently launched a tool called Project Health (pH).

Testing has become an integral part of Google's engineering culture.

Limit of automated testing
- Test that need human judgement (quality of search result, audio)
- Complex security vulnerabilities
  
**Exploratory testing** - a fundamentally creative endeavor in which someone treats the application under test as a puzzle to be broken, maybe by executing an unexpected set of steps or by inserting unexpected data


# Chapter 12: Unit Testing
Brittle test wastes valuable time.

The ideal test is unchanging.

Types of changes to codebase
-  Pure refactorings
-  New features
-  Bug fixes
-  Behaviour changes

Ways to prevent brittle test:
- Only behaviour changes are expected to have to make updates to the system's existing test.
- Test via public APIs (write tests that invoke the system being tested in the same way its users would. If such a test breaks, it implies that an existing user of the system will also be broken)
- Test state, not interaction (state: looks after invoking code, interaction: expected sequence of actions)

If a method or class exists only to support one or two other classes (i.e., it is a “helper class”), it probably shouldn’t be considered its own unit

Ways to write clean tests
- Make your tests complete and concise (it is okay to violate DRY principle if it leads to clearer tests)
- Test behaviours, not method (a single method often does a few things under the hood, writing test for method can make test unclear. Behaviors can often be expressed using the words "given," "when," and "then")
  ``` c
  @Test
  public void transferFundsShouldMoveMoneyBetweenAccounts() {
    // Given two accounts with initial balances of $150 and $20
    Account account1 = newAccountWithBalance(usd(150));
    Account account2 = newAccountWithBalance(usd(20));

    // When transferring $100 from the first to the second account
    bank.transferFunds(account1, account2, usd(100));

    // Then the new account balances should reflect the transfer
    assertThat(account1.getBalance()).isEqualTo(usd(50));
    assertThat(account2.getBalance()).isEqualTo(usd(120));
  }
  ```
- Name tests after the behavior being tested
- Don't put logic in tests
- Write clear failure message  
  ``` shell
  // bad example
  Test failed: account is closed
  
  // good example
  Expected an account in state CLOSED, but got account:
      <{name: "my-account", state: "OPEN"}
  ```

Truth (assertion library developed by Google)

Test should be **DAMP** (Descriptive and Meaningful Phrases)

**Shared values**: Many tests are structured by defining a set of shared values to be used by tests and then by defining the tests that cover various cases for how these values interact. A better way to accomplish this goal is to construct data using helper methods that require the test author to specify only values they care about, and setting reasonable defaults for all other values. 

**Shared set-up**: The best use case for setup methods is to construct the object under tests and its collaborators. One risk in using setup methods is that they can lead to unclear tests if those tests begin to depend on the particular values used in setup. The test should state those values directly.

**Shared helper and validation**: The best validation helper methods assert a single conceptual fact about their inputs, in contrast to general-purpose validation methods that cover a range of conditions.

**Defining Test Infrastructure**: Sometimes, it can also be valuable to share code across multiple test suites. (eg: JUnit for Java)


# Chapter 13: Test Doubles
A **test doubles** is an object or function that can stand in for a real implementation in a test. (e.g. in-memory database, trigger an rare error condition, ensure heavyweight function is called without actually executing the function's implementation, testing credit card transaction without incurring transaction fee)

- Testability (e.g. code that is flexible to use in-memory databases)
- Applicability
- Fidelity - how closely the behaviour of a test double resembles the behaviour of the real implementations

Test doubles often need to be vastly simpler than the real implementations.

A good test should need to change only if user-facing behavior of an API changes.

## Basic Concepts
A *seam* is a way to make code testable by allowing the use of test doubles, it makes it possibl to use different dependencies for different systems.

*Dependency injection* is a common technique for introducing seams. (e.g. Java Framework: [Guice](https://github.com/google/guice), [Dagger](https://dagger.dev/)).

Dynamically typed languages such as Python or JavaScript allows dynamically replace individual functions or object methods. This makes it possible to use real implemenetations of dependencies in test while only overriding functions or methods of the dependency that are unsuitable for tests.

A mocking framework is a software library that makes it easier to create test doubles within tests, allows you to replace an object with a mock. (e.g. Mockito for Java)

Mock is a test double whose behaviour is specified inline in a test.

## Techniques for Using Test Doubles
- **Faking** - A fake is a lightweight implementation of an API that behaves similar to the real implementation but isn't suitable for production (e.g. in-memory database)
- **Stubbing** - A process of giving behaviour to a function that otherwise has no behaviour on its own, specify the return value of a function (stub the return value)
- **Interaction Testing** (called *mocking*) - A way to validate how a function is called without actually calling the implementation of the function (e.g. return error when function isn't called the correct way - wrong argument, not being called)

## Real Implementation
Writing testable code requires an upfront investment. It is especially critical early in the lifetime of a codebase. The later testability is taken into account, the more difficult it is to apply to a codebase.

Although tests were easy to write, they might require constant effort to maintain while rarely finding bugs. Many Google engineers avoid mocking frameworks in favor of writing more realistic tests.

At Google, the preference for real implementations developed over time as we saw that overuse of mocking frameworks had a tendency to pollute tests with repetitive code that go out of sync with the real implementations and made refactoring difficult.

Preferring new implementation in tests is known as **classical testing**. Preference to use mocking frameworks instead of real implementation is called **mockist testing**.

Paper by ThoughtWorks regarding how to use mock objects - [link](http://jmock.org/oopsla2004.pdf)

Google created a `@DoNotMock` annotation in JavaScript.

Every time a mocking framework is used for stubbing or interaction testing, it duplicates behavior provided by the API.

How to decide when to use a real implementation
- Execution time - It is often simpler to use a real implementation until it becomes too slow to use
- Determinism - A real implementation might be more complex and increase the chance of non-deterministic (e.g. multithreading which occasionally fail, not hermetic code, code that depends on clock time)
- Dependency construction - A real implementation might have too many dependencies
  - The construction need to be flexible enough to be able to use test doubles rather than hardcoding the implementation that will be used for production

## Deep dive into different techniques
### Faking
Example: A filesystem that store the file contents in memory instead of on disk

Pro: 
- Execute quickly and allow you to effectively test the code without the drawbacks of using real implementations
- Radically improve the testing experience, be an enormous boost to engineering velocity
- Useful when real implementations is slow and flaky, and there is a large user base

Trait:
- Ideally, the team that owns the real implementation should write and maintain a fake
- A system under test shouldn't be able to tell whether it is interacting with a real implementation or a fake. 
- It requires maintenance
  - The fake should be implemented in the root level to reduce repeated code (e.g. a fake for database API rather than for each class that calls the database API)
  - If the implementation needs to be duplicated across multiple languages, a solution is to create a single fake service and have test configure to send request to this fake service
- Fidelity - how closely the behavior of a fake matches the behavior of the real implementation
  - The fake must have perfect fidelity to the real implementation, but only from the perspective of the test
  - Example: 
    - If an item is successfully saved when ID does not exist but produced an error when the ID already exists, the fake must conform to the same behaviour
    - A fake database won't have fidelity in term of hard drive storage, it won't have the same hash value for the database, it won't have the same latency and resource consumption
  - Best to have fake to fail for unsupported behavior
- Fakes should be tested to ensure that the behavior don't diverge over time as the real implementation evolves
  - The owner of the fake should test against the API's public interface and running those test against both the real implementation and the fake (known as contract tests) 

### Stubbing
Stubbing is a way for a test to hardcode behavior for a function that otherwise has no behavior on its own.

Example: Simulate a response from a credit card transaction

Con:
- Tests become unclear, it can be hard to understand if you are not familiar with the implementation
- Tests become brittle, stubbing leaks implementation details of your code into the test
- Tests become less effective, there is no way to store state using stubbing, and hardcore logic is duplication of the details of API logic

Trait:
- A test typically should stub out only a small number of functions
- Can be helpful to retuen values or errors that might not be possible to trigger from a real implementation or fake
- Each stubbed function should have a direct relationship with a test's assertion

### Interaction Testing
Interaction testing is a way of validate how a function is called without actually calling the implementation of the function.

It is preferred to test code through state testing. (e.g. Call the system under test and validate that either the correct value was returned or some other states of the system under test was properly changed.)

Con:
- Interaction testing can't tell if the system under test is working properly, it only validate that certain functions are called as expected
- It utilizes the implementation details of the system under test

Trait:
- Useful when you are unable to use a real implementation or a fake, but you want to validate that certain functions are called
- Useful when the differences in the number of order of calls would cause undesired behavior (e.g. when testing caching)

Best practices
- Prefer to perform interaction testing only for state-changing functions
- Avoid overspecification


# Chapter 14: Larger Testing





# Chapter 15: Deprecation





# Chapter 16: Version Control and Branch Management
A VCS is a system that tracks revisions (versions) of files over time. A VCS maintains some metadata about the set of files being managed, and collectively a copy of the files and metadata is called a repository.

Google used a centralized version control systems called Piper and a monorepo.

DevOps Research Association (DORA)

The problem that using a development branch are attempting to solve (instability of the product) is a legitimate one—but one that we have found to be solved far better with more extensive use of tests, Continuous Integration (CI), and quality enforcement practices like thorough code review.

All of that effort in merging and retesting is pure overhead. The alternative requires a different paradigm: trunk-based development, rely heavily on testing and CI, keep the build green, and disable incomplete/untested features at runtime.

It may be sensible to create a release branch that represents the exact code that went into the release build for your product. If any critical flaws are discovered between the actual release of that product into the wild and the next release cycle, fixes can be cherry-picked (a minimal, targeted merge) from trunk to your release branch. A dev branch is expected to merge back to trunk, and could even be further branched by another team. A release branch is expected to be abandoned eventually.

Google have a OWNERS file that lists the username of engineers allowing to commits within the subtree of the repo.

One-Version Rule - Developers must never have a choice of “What version of this component should I depend upon?”

Dependency across time in any form is far more costly and complicated than code that is time invariant. Internally, Google production services make relatively few promises of that form. We also benefit greatly from a cap on potential version skew imposed by our “build horizon”: every job in production needs to be rebuilt and redeployed every six months, maximum.

Many Google teams use release branches, with limited cherry picks. If you’re going to put out a monthly release and continue working toward the next release, it’s perfectly reasonable to make a release branch.

Software engineering tools including both VCS and build systems are increasingly providing mechanisms to smartly blend between fine-grained repositories and monorepos to provide an experience akin to the monorepo—an agreed-upon ordering of commits and understanding of the dependency graph. Git submodules, Bazel with external dependencies, and CMake subprojects all allow modern developers to synthesize something weakly approximating monorepo behavior without the costs and downsides of a monorepo.

Fine-grained repositories in a federated/virtual-monorepo (VMR)–style repository can make it easier to isolate experimental or top-secret projects while still holding to One Version and allowing access to common utilities.

To put it another way: if every project in your organization has the same secrecy, legal, privacy, and security requirements, a true monorepo is a fine way to go. Otherwise, aim for the functionality of a monorepo, but allow yourself the flexibility of implementing that experience in a different fashion. If you can manage with disjoint repositories and adhere to One Version or your workload is all disconnected enough to allow truly separate repositories, great. Otherwise, synthesizing something like a VMR in some fashion may represent the best of both worlds.

Argument against monorepo
- Technical limitations
- it doesn’t match how development happens in the Open Source Software (OSS) world
- as your organization scales up, it is less and less likely that every piece of code is subject to exactly the same legal, compliance, regulatory, secrecy, and privacy requirements

Looking at the past few years of major improvements to Git, there’s clearly a lot of work being done to support larger repositories: shallow clones, sparse branches, better optimization, and more.



# Chapter 17: Code Seaech





# Chapter 18: Build Systems and Build Philosophy





# Chapter 19: Critique: Google's Code Review Tool





# Chapter 20: Static Analysis
Static analysis refers to programs analyzing source code to find potential issues such as bugs, antipatterns, and other issues that can be diagnosed without executing the program.

Codify best practices
- Identify constant expressions that overflow
- Tests that never run
- Invalid format strings in logging statements that would crash when executed
- Verifying that naming conventions are upheld
- Flagging the use of deprecated APIs
- Pointing out simpler but equivalent expressions that make code easier to read

Make static analysis scalable and usable
- Focus analyses on files affected by a pending code change
- Anything that can be fixed automatically should be fixed automatically
- Focus on smooth developer workflow integration

Three keys lessons in making static analysis work
- Focus on developer happiness (reduce effective false-positive rate)
- Make static analysis a part of the core developer workflow
- Empower users to contribute

A static analysis tool can produce warnings that are technically correct but misinterpreted by users as false positives. We call the user-perceived false-positive rate the "**effective false positive**" rate.

Tricorder: Google's Static Analysis Platform

The four criteria for new Tricorder checks
- Be understandable
- Be actionable and easy to fix
- Produce less than 10% effective false positive
- Have the potential of significant impact on code quality

There are many different types of static analysis tools integrated with Tricorder.
- [Error Prone](http://errorprone.info/)
- [clang-tidy](https://clang.llvm.org/extra/clang-tidy/)

Tricorder also built integrated feedback channel such as button of "Not useful", "Please fix" to collect feedback. It also provides automated fixes.

There are also additional optional analyzers (such as The Proto Best Practices Analyzer).

The key insight to making this customization successful was to focus on project-level customization, not user-level customization.

Presubmits checks include very simple customizable built-in checks on the contents or metadata of a change, such as ensuring that the commit message does not say “DO NOT SUBMIT” or that test files are always included with corresponding code files. 

Integrate static analysis into compiler. We enforce these criteria
- Actionable and easy to fix
- Produce no effective false positives
- Report issues affecting only correctness rather than style or best practices

Integrate static analysis with Integrated Development Environment (IDE).


# Chapter 21: Dependency Management





# Chapter 22: Large-scale Change





# Chapter 23: Continuous Integration
Continuous Integration, or CI, is generally defined as “a software development practice where members of a team integrate their work frequently and each integration is verified by an automated build to detect integration error as quickly as possible. The fundamental goal of CI is to automatically catch problematic changes as early as possible.

Modern definition: the continuous assembling and testing of our entire complex and rapidly evolving ecosystem.

CI and testing is tightly coupled. From a testing perspective, CI is a paradigm to inform the following
- Which test to run in development/release workflow
- Compose system under test (SUT), balancing concerns like fidelity and setup costs

## CI Concepts
Life of a code change
![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781492082781/files/assets/seag_2302.png)


Canarying - deploying to a small percentage of production first

Version skew - a state of a distributed system in which it contains multiple incompatible versions of code

Experiments and feature flags are extremely powerful feedback loops. They reduce deployment risk by isolating changes within modular components that can be dynamically toggled in production.

### Fast feedback loops
- Accessible and actionable feedback
### Automation
- Continuous Build (CB) - integrates the latest code changes at head and runs an automated build and test. Introduce two heads, true head and green head (verified by CB)
- Continuous Delivery (CD) - a continuous assembling of release candidates, followed by the promotion and testing of those candidates throughout a series of environments—sometimes reaching production and sometimes not.
- Continuous Testing
  - Pre-submit: Fast and reliable ones
  - Release-candidate testing

Any static configuration you do have should be promoted as part of the release candidate so that it can undergo testing along with its corresponding code.

Release candidate (RC): A cohesive, deployable unit created by an automated process, assembled of code, configuration, and other dependencies that have passed the continuous build.

As an RC progresses through environments, its artifact (e.g. binaries, containers) ideally should not be recompiled or rebuilt. Using containers such as Docker helps enforce consistency of an RC between environments, from local development onward. Similarly, using orchestration tools like Kubernetes (or in our case, usually Borg), helps enforce consistency between deployments.

Testing on only pre-submit is too expensive.

Mid-air collision: Two changes that touch completely different files cause test to fail.

Benefits of running release-candidate testing, even if it is the same suite that CB ran against the code on post-submit
- As a sanity check
- For auditability
- To allow for cherry picks
- For emergency pushes

Production testing

A well-managed alerting system helps to ensure that your Service-Level Objectives (SLOs) are being met. A good CI system helps to ensure that your build is in good shape—the code compiles, tests pass, and you could deploy a new release if you needed to. 

### Challenge of implementing CI
- Presubmit optimization
- Culprit finding and failure isolation
- Resource restraints
- Failure management (what to do when tests fail)
- Test instability

### Hermatic Testing
Hermetic tests: tests run against a test environment (i.e., application servers and resources) that is entirely self-contained (i.e., no external dependencies like production backends).

## CI at Google
TAP (Test Automation Platform)

Every team has a Build Cop to keep all the tests passing in their particular project, regardless of who breaks them.




# Chapter 24: Continuous Delivery
- Agility: Release frequently and in small batches
- Automation: Reduce or remove repetitive overhead of frequent releases
- Isolation: Strive for modular architecture to isolate changes and make troubleshooting easier
- Reliability: Measure key health indicators like crashes or latency and keep improving them
- Data-driven decision making: Use A/B testing on health metrics to ensure quality
- Phased rollout: Roll out changes to a few users before shipping to everyone

- **Velocity is a team sport**: The optimal workflow for a large team that develops code collaboratively requires modularity of architecture and near-continuous integration.
- **Evaluate changes in isolation**: Flag guard any features to be able to isolate problems early.
- **Make reality your benchmark**: Use a staged rollout to address device diversity and the breadth of the userbase. Release qualification in a synthetic environment that isn’t similar to the production environment can lead to late surprises.
- **Ship only what gets used**: Monitor the cost and value of any feature in the wild to know whether it’s still relevant and delivering sufficient user value.
- **Shift left**: Enable faster, more data-driven decision making earlier on all changes through CI and continuous deployment.
- **Faster is safer**: Ship early and often and in small batches to reduce the risk of each release and to minimize time to market.


# Chapter 25: Compute as a Service
