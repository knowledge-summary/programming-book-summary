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
