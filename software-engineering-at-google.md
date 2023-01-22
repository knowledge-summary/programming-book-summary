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
  SPOFs can arise out of good intentions: it can be easy to fall into a habit of “Let me take care of that for you.” But this approach optimizes for short-term efficiency (“It’s faster for me to do it”) at the cost of poor long-term scalability (the team never learns how to do whatever it is that needs to be done). This mindset also tends to lead to all-or-nothing expertise.
- **All-or-nothing expertise**  
  A group of people that is split between people who know “everything” and novices, with little middle ground. This problem often reinforces itself if experts always do everything themselves and don’t take the time to develop new experts through mentoring or documentation. In this scenario, knowledge and responsibilities continue to accumulate on those who already have expertise, and new team members or novices are left to fend for themselves and ramp up more slowly.
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
| Hire pushovers | Hire people you can push around, cement your position but mean more works for you to guide | Strive to hire people who are smarter than you and can replace you. They will consistently impress you and make great things happen. |
| Ignore low performers | Most difficult cases to handle are when someone just isn't capable of doing their job no matter how long or hard they work. It will drag the high performer and reduce team morale | Put yourself in the position of helping them up or out. Oftentimes, they merely need some encouragement or direction to slip into a more productivity. It almost always requires temporary micromanagement, but still a whole lot of humility, respect, and trust—particularly respect. |
| Ignoring human issues | There are two major areas of focus for the team: the social and the technical | Being more empathy and don't be a jerk | 
| Be everyone's friend  | Don’t confuse friendship with leading with a soft touch: when you hold power over someone’s career, they might feel pressure to artificially reciprocate gestures of friendship. If the friend who is being managed is not self-managing and is not a hard worker, it can be stressful for everyone. | You can be a tough leader without tossing your existing friendships to the wind. Having lunch with your team can be an effective way to stay socially connected to them without making them uncomfortable |
| Compromise the hiring bar | The cost of finding the appropriate person pales when compare with the cost to deal with bad hire. Steve Jobs once said: "A people hire other A people; B people hire C people." | Ensure the candidates meet the hiring bar |
| Treat your team like children | People tend to act the way you treat them, so if you treat them like children or prisoners, don’t be surprised when that’s how they behave. You can manifest this behavior by micromanaging them or simply by being disrespectful of their abilities and giving them no opportunity to be responsible for their work. | If you hire people worthy of trust and show these people you trust them, they’ll usually rise to the occasion. |

Positive patterns
- Lose the ego 
  - There is a fine line between being humble and letting others take advantage of you. You can still have self-confidence and opinions without being an egomaniac.
  - Trust and avoid micromanage
  - Encourage inquiry and constructive criticism
  - Apologize when you make a mistake
- Be a zen master
  - Be less vocally skeptical while still letting your team know you're aware of the intricacies and obstacles involved in the work
  - Mediating your reactions and maintaining your calm
  - Your team will consciously and subconsciously look to you for clues on how to react
  - Zen management trick: asking questions. Help the person to solve the problem on their own by trying to refine and explore the problem.
- Be a catalyst
  - Build consensus, drive the process from start to finish, give a gentle push to the right direction
- Remove roadblocks
  - Jump in to help the team remove technical or organizational roadblocks
  - In many cases, knowing the right person is more valuable than knowing the right answer
- Be a teacher and a mentor
  - Teaching people and giving them a chance to learn on their own can be incredibly difficult at first, but it’s a vital component of effective leadership
  - This is especially important for new hires who, in addition to learning your team’s technology and codebase, are learning your team’s culture and the appropriate level of responsibility to assume.
  - Three things needed
    - Experience with your team’s processes and systems
    - The ability to explain things to someone else
    - The ability to gauge how much help your mentee needs
- Set clear goals
  - If you’re going to have clear goals, you need to set clear priorities and help your team decide how it should make trade-offs when the time comes.
  - Create a concise mission statement for the team, step back and give it more autonomy, periodically checking in to make sure everyone is still on the right track.
- Be honest
  - Sometimes you can't tell your team something, or need to tell everyone something they don't want to hear, or simply don't know
  - Using "compliment sandwich" to soften the blow when giving criticise might make people not hearing the critical message
  - Instead, be kind and empathetic when delivering constructive criticism. Give clear feedback and direction.
- Track happiness
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
To manage codebase, Google maintain a set of style guide that define the rules.

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

Automated enforcement of rules if possible.
- Some technical rules explitcitly call for human judgement
- Other rules are social rather than technical (such as what is considered as small commit)
