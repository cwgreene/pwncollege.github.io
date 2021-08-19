# Syllabus

This is the syllabus for CSE 466, Fall 2021.

## Course Description

This course will take students through an exploration of the ways that the Security of Computer Systems can fail.
Security is a complicated thing: it is only as strong as its weakest link, and a small, single mistake can often bring down otherwise extremely secure software.

Taking the intuition that, to build secure systems in the future, one must understand how security can break, we will cover a number of different failure modes of computer systems, ranging from application security to network and operating system security to web security.
Each lecture will consist of an introduction to a new topic, examples of real-world effects of security failures related to the topic, and an assignment for students to explore these concepts.

These assignments will be very thorough, and by the end, students will have an _intuitive_ understanding on how to exploit these vulnerabilities, and will have the building blocks needed to prevent them, both in the lab and in the real world.

## Prerequisites

This course will be *EXTREMELY* challenging, and students are expected to learn some of the necessary technologies on their own time.

This course requires a good understanding of low-level computer architecture (for example, students should understand x86 assembly) and low-level programming languages (specifically, C), and good command of a high-level programming language (specifically, Python).
You should have a _very_ good background in operating systems (especially Linux or UNIX variants).
If you do not have these skills, or do not plan on acquiring them very early in the course, you will have a hard time.
A good approximation of the type of material that you will be faced with is the first six levels of the [Vortex wargame](http://overthewire.org/wargames/vortex/).


# Recommended Textbook

There is no recommended textbook for this course.
Any reading material assigned will be from publicly-available sources on the internet.


# Course Communication

All announcements and communications for the class will take place on the pwn.college discord, with announcements in the #announcements public channel and discussion in the #text class-specific channel.
Students are *required* to be on this discord.

Student may use the discord to ask questions or clarifications, and the TA, Instructor, or other students can answer.
Note that sharing full solution scripts or answers is expressly prohibited, but otherwise, collaboration on the way to the solution is allowed.
If done digitally, such collaboration *must* take place on the official pwn.college discord, in one of the text or voice channels created for this purpose.
Collaboration on other discords or other digital channels will be considered to be an academic integrity violation.

Questions should be emailed to [pwn-college@asu.edu](mailto:pwn-college@asu.edu).
Questions meant just for the professor should be addressed to the following email address: yans@asu.edu.
PLEASE do not email course material questions just to Yan: he gets super swamped and starts packet dropping.
Your questions will get much more attention if sent to [pwn-college@asu.edu](mailto:pwn-college@asu.edu).

Before emailing your question, please consider asking it on the discord instead.
This way, the entire class will benefit from your question.

# Course Topics

The course will consist of the modules listed on https://pwn.college.
Each module will take roughly one week, with some slack throughout the semester for review and catch-up.

# Assessment

## Assignments only, no exams or quizzes.

Students will be evaluated on their performance on between 7 and 14 equally-weighted homework assignments (the modules), with each assignment consisting of between 20 and 150 (yes, really) challenge problems.

## Assignment timing.

Assignments will be released at the end of class, and will normally be due at 4pm, one week after they are assigned (i.e., a homework assigned at the end of class on Tuesday would normally be due at 4pm the next Tuesday).
All grading is done automatically through flag submissions.
Late submissions are allowed, but only earn half points toward the final grade.

## Challenge-based assignments with flags as rewards.

Each assignment will consist of a large amount of varied, but related challenges, and will be live for between one and two weeks.
Solving these challenges may require the use or implementation of fairly complex hacking tools.
Solving each individual challenge will grant a _challenge-specific_ passcode, called a "flag".
The maximum number of flags possible to score for an assignment is equal to the maximum number of challenges in the assignment.

The existence of flags means that _there is no wrong way to solve a challenge_.
If you tricked the challenge into giving you the valid flag, good job.

## Converting flags to grades.

For each assignment, a student's grade is the ratio of the flags they earn out of the possible flags, scaled to 100%.
If a student earns 70 flags from 70 challenges on an assignment (yes, assignments may be this big and even bigger), they will receive 100%.
If they earn 50 flags out of 70 possible ones, they will get 71% on the assignment.

## Extra credit: CTFs

There are cybersecurity competitions being held every weekend.
Every weekend, during the semester, you and your friends can participate in one CTF and earn one percentage point bonus in the course.
Teams can be anywhere from a minimum of 4 players to a maximum of 8 players.
If you need a team size exception (for example, to play with a well-established CTF team), please email us.
Each player will have to submit a writeup about what they worked on during the weekend, what they solved, and what they learned.

To get the percentage point of extra credit, you need to either solve a _non-trivial_ challenge (i.e., not a "sanity check") _or_ put in at least 8 hours of effort.

You can earn one percentage point per weekend, up to a maximum of 14% or 15% added to your final grade, depending on the exact timing of when grades are due and so on (which could vary slightly due to COVID).
The expected amount of viable weekends is 15.

## Extra credit: helping others.

**NEW THIS YEAR!** We have recruited the help of a reputation bot on the pwn.college discord.
Whenever you get thanked by a student in a public channel, the reputation bot will award reputation.
At the end of the semester, we will tally up this reputation and run something like PageRank on the reputation graph to award up to 10% extra credit.

This is a new, experimental extra credit system.
Please do not abuse and ruin it.
We will consider adversarial reputation farming to be cheating, and respond accordingly.

## More extra credit: bug bounty program.

Any *responsibly-disclosed* _serious_ security issues in course infrastructure will earn an extra 5 to 50 "bug bounty" _percentage points_ for the current assignment, for a theoretical maximum of 150% for the assignment, depending on the severity of the issue.
Blatantly spurtious reports may earn a *negative* percentage report of up to -15 percentage points.
Allowances will be made for honest mistakes leading to a spurtious bug bounty filing, but don't waste our time on purpose.

## Final grade calculation.

The final grade will be calculated by averaging the grades of each homework assignment, equally weighted, then adding extra credit.
For example, if there are 10 assignments, and a student scores 100% on each assignment, participates in a CTF every weekend, and is the most helpful student on discord, they will score 125%.
If they score 100% on each assignment and ignore CTFs, they will score 100%.
If they score 100% on each assignment except for one assignment that they blow off completely, they will get a grade of 90%.
Being the most helpful on discord will bring that back up to 100%.

Percentages will be translated to letter grades with the following initial cutoffs:

| Percentage Grade | Letter Grade |
|------------------|--------------|
| >= 99            | A+           |
| >= 92            | A            |
| >= 90            | A-           |
| >= 88            | B+           |
| >= 82            | B            |
| >= 80            | B-           |
| >= 78            | C+           |
| >= 70            | C            |
| >= 60            | D            |
| < 60             | E            |

With the exception of the cutoff for A+, these cutoffs can be curved _downward_ in the event that students do worse than expected.
That is, if you earn an 88% in the course, you are guaranteed at least a B+, but if everyone else does super poorly, the curve might pull you up to an A, but never an A+.
Updates on the theme of "what would the cutoffs be if the course ended today" will be provided at the conclusion of each assignment.

For expectation management, in Fall 2021, the final curve was:

| Percentage Grade | Letter Grade |
|------------------|--------------|
| >= 82            | A            |
| >= 67            | B            |
| >= 52            | C            |
| >= 37            | D            |
| < 37             | E            |

# Special Accommodations

Students requesting disability accommodations should register with the Disability Resource Center (DRC) and present the instructor with appropriate documentation from the DRC.

# Plagiarism and Cheating

Plagiarism or any form of cheating in assignments or projects is subject to serious academic penalty. To understand your responsibilities as a student read: [ASU Student Code of Conduct](http://www.asu.edu/aad/manuals/usi/usi104-01.html) and [ASU Student Academic Integrity Policy](http://provost.asu.edu/academicintegrity/policy).
There is a zero tolerance policy in this class: any violation of the academic integrity policy will result in a zero on the assignment and the violation will be reported to the Dean’s office.
Plagiarism is taken very seriously in this course.

Examples of academic integrity violations include (but are not limited to):

- Sharing code with a fellow student (even if it’s only a few lines).
- Collaborating on code with a fellow student (unless explicitly allowed).
- Using another students solution to solve a challenge and get a flag.
- Sharing a flag with another student (NEVER ALLOWED UNDER ANY CIRCUMSTANCES).

Posting your assignment solutions online _before the due date of the assignment_ is expressly forbidden, and will be considered a violation of the academic integrity policy.
Note that this includes working out of a public Github repository.
The [Github Student Developer Pack](https://education.github.com/pack) provides unlimited private repositories while you are a student, making it easy to begin with a private GitHub repository and easily make it public after the assignment deadline.

**Collaboration policy:** New this year: we are a kinder, gentler CSE 466, and full collaboration (except for direct sharing of solution scripts) is allowed in person or on the official pwn.college discord. Collaboration through other discords or other digital channels is not allowed, and will be considered an academic integrity violation. Sharing of solution scripts or flags is not allowed, and will be considered an academic integrity violation.

# Syllabus Update

Information in the syllabus may be subject to change with reasonable advance notice and an announcement on discord.

# Misc

Syllabus copyright 2021 Yan Shoshitaishvili, along with all lectures and course-related written materials.
During this course students are prohibited from making audio, video, digital, or other recordings during class, or selling notes to or being paid for taking notes by any person or commercial firm without the express written permission of the faculty member teaching this course.
Be reasonable.

Title IX is a federal law that provides that no person be excluded on the basis of sex from participation in, be denied benefits of, or be subjected to discrimination under any education program or activity.  Both Title IX and university policy make clear that sexual violence and harassment based on sex is prohibited.  An individual who believes they have been subjected to sexual violence or harassed on the basis of sex can seek support, including counseling and academic support, from the university.  If you or someone you know has been harassed on the basis of sex or sexually assaulted, you can find information and resources at https://sexualviolenceprevention.asu.edu/faqs. 

 As a mandated reporter, I am obligated to report any information I become aware of regarding alleged acts of sexual discrimination, including sexual violence and dating violence. ASU Counseling Services, https://eoss.asu.edu/counseling, is available if you wish discuss any concerns confidentially and privately.


