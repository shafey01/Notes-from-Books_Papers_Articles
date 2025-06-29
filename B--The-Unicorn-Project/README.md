# Highlights - the-unicorn-project.pdf


* “… I promised Steve and Dick that I’d put you in a role where you couldn’t make any production changes anymore,” Chris says, squirming. “So, uh, effective immediately, you’re moving from the manufacturing plant ERP systems to help with documentation for the Phoenix Project …” When she’s out of sight, she leans against the wall. Tears well up. Suddenly she remembers the missing step in the KüblerRoss cycle after bargaining: depression.

* You know you’re in real trouble when even the intern feels sorry for you, After all, making developers more productive is always super important, even those working on the Phoenix Project in its fiery, meteoric descent.

* She looks around at the entire floor. Over a hundred developers are typing away, working on their little piece of the system on their laptops. Without constant feedback from a centralized build, integration, and test system, they really have no idea what will happen when all their work is merged with everyone else’s.

* Maxine loves coding and she’s awesome at it. But she knows that there’s something even more important than code: the systems that enable developers to be productive, so that they can write highquality code quickly and safely, freeing themselves from all the things that prevent them from solving important business problems.

* She is still the only person who knows every keyboard shortcut from vi to the latest, greatest editors. But she is never ashamed to tell anyone that she still needs to look up nearly every command line option for Git—because Git can be scary and hard! What other tool uses SHA1 hashes as part of its UI?

* Everyone around here thinks features are important, because they can see them in their app, on the web page, or in the API. But no one seems to realize how important the build process is. Developers cannot be productive without a great build, integration, and test process.

* If you keep checking after each small change, you’ll never have something big you need to fix …” Reflecting on what she said, she adds, “One of the really nice things about running your program frequently is that you get to see it running, which is fun, and that’s what programming is all about.” But in almost every other domain, especially when you have customers, change is a fact of life. A healthy software system is one that you can change at the speed you need, where people can contribute easily, without jumping through hoops. This is how you make a project that’s fun and worthwhile contributing to, and where you often find the most vibrant communities.

* Like most developers, she’s very superstitious that if she stops watching the build, it will fail.

* To everyone’s surprise, Dwayne bets Sunday evening, “You people have no idea how unprepared we really are for this release—this one will go down in the record books.”

* Maxine doesn’t know whether to laugh, smirk, or throw up—when missiles are stuck in the launch tube, it’s a very dangerous scenario, because at that point the missile is already armed and too dangerous to approach.

* Erik answers, “It’s an archaic word, resurrected by Sensei Rich Hickey. ‘Complect’ means to turn something simple into something complex.

* “Simplicity is important because it enables locality. Locality in our code is what keeps systems loosely coupled, enabling us to deliver features faster. Teams can quickly and independently develop, test, and deploy value to customers. Locality in our organizations allows teams to make decisions without having to communicate and coordinate with people outside the team, potentially having to get approvals from distant authorities or committees so far removed from the work that they have no relevant basis to make good Decisions,” he says, clearly disgusted.

* Erik laughs. “There are many definitions, but my favorite is how it was originally defined by Ward Cunningham in 2003. He said, ‘technical debt is what you feel the next time you want to make a change.’ There are many things that people call technical debt, but it usually refers to things we need to

* Clean up, or where we need to create or restore simplicity, so that that we can quickly, confidently, and safely make changes to the system.

* “I’ve started calling all of these things ‘complexity debt,’ because they’re not just technical issues—they’re business issues. And it’s always a choice,” he says. “You can choose to build new features or you can choose to pay down complexity debt. When a fool spends all their time on features, the inevitable outcome is that even easy tasks become difficult and take longer to execute. And no matter how hard you try or how many people you have, it eventually collapses under its own weight, forcing you to start over from scratch.”

* “I’ve heard he’s been having many conversations with Bill Palmer, the new VP of IT Operations,” Kirsten adds. “Bill told me about how Erik is teaching him something called the Three Ways and the Four Types of Work.”

* First Ideal of Locality and Simplicity. We need to design things so that we have locality in our systems and the organizations that build them. And we need simplicity in everything we do. The last place we want complexity is internally, whether it’s in our code, in our organization, or in our processes. The external world is complex enough, so it would be intolerable if we allow it in things we can actually control! We must make it easy to do our work.”

* “The Second Ideal is Focus, Flow, and Joy. It’s all about how our daily work feels. Is our work marked by boredom and waiting for other people to get things done on our behalf? Do we blindly work on small pieces of the whole, only seeing the outcomes of our work during a deployment when everything blows up, leading to firefighting, punishment, and burnout? Or do we work in small batches, ideally singlepiece flow, getting fast and continual feedback on our work? These are the conditions that allow for focus and flow, challenge, learning, discovery, mastering our domain, and even joy.”

* “In its briefest form: The Third Ideal is Improvement of Daily Work. Reflect upon what the Toyota Andon cord teaches us about how we must elevate improvement of daily work over daily work itself. The Fourth Ideal is Psychological Safety, where we make it safe to talk about problems, because solving problems requires prevention, which requires honesty, and honesty requires the absence of fear. In manufacturing, psychological safety is just as important as physical safety. And finally, the Fifth Ideal is Customer Focus, where we ruthlessly question

* Whether something actually matters to our customers, as in, are they willing to pay us for it or is it only of value to our functional silo?” The First Ideal—Locality and Simplicity The Second Ideal—Focus, Flow, and Joy The Third Ideal—Improvement of Daily Work The Fourth Ideal—Psychological Safety The Fifth Ideal—Customer Focus

* Being able to test and push code to production is more productive, makes for happier customers, creates accountability of code quality to the people who write it, and also makes the work more joyful and rewarding.

* This is not the famous Amazon ideal of the “twopizza team,” where features can be created by individual teams that can be fed with two pizzas.

* “Technical debt is a fact of life, like deadlines. Business people understand deadlines, but often are completely oblivious that technical debt even exists. Technical debt is inherently neither good nor bad—it happens because in our daily work, we are always making tradeoff decisions,” he says. “To make the date, sometimes we take shortcuts, or skip writing our automated tests, or

* Hardcode something for a very specific case, knowing that it won’t work in the longterm. Sometimes we tolerate daily workarounds, like manually creating an environment or manually performing a deployment. We make a grave mistake when we don’t realize how much this impacts our future productivity.”

* Satya Nadella, CEO of Microsoft, still has a culture that if a developer ever has a choice between working on a feature or developer productivity, they should always choose developer productivity.

* “In 2010, Risto Siilasmaa was a board director at Nokia. When he learned that generating a Symbian build took a whole fortyeight hours, he said that it felt like someone hit him in the head with a sledgehammer,” Erik says. “He knew that if it took two days for anyone to determine whether a change worked or would have to be redone, there was a fundamental and fatal flaw in their architecture that doomed their nearterm profitability and longterm viability. They could have had twenty times more developers, and it wouldn’t have made them go any faster.

* “Business people can see features or apps, so getting funding for those is easy,” he continues. “But they don’t see the vast architectures underneath that support them, connecting systems, teams, and data to each other. And underneath that is something extraordinarily important: the systems that developers use in their daily work to be productive.

* Maxine smiles as she hears the suggestions fly fast and furious. They start making a list: Every developer uses a common build environment. Every developer is supported by a continuous build and integration system. Everyone can run their code in productionlike environments. Automated test suites are built to replace manual testing, liberating QA people to do higher value work. Architecture is decoupled to liberate feature teams, so developers can deliver value independently. All the data that teams need is put in easily consumed APIs … As Sensei Dr. Steven Spear said, ‘It is ignorance that is the mother of all problems, and the only thing that can overcome it is learning.’

* “You may recognize them as rigid project plans, inflexible procurement processes, powerful architecture review boards, infrequent release schedules, lengthy approval processes, strict separation of duties … “Each adds to the coordination cost for everything we do, and drives up our cost of delay. And because the distance from where decisions are made and where work is performed keeps growing, the quality of our outcomes diminish. As Sensei W. Edwards Deming once observed, ‘a bad system will beat a good person every time.’

* ‘a bad system will beat a good person every time.’

* ‘a bad system will beat a good person every time.’

* ‘a bad system will beat a good person every time.’

* “You may have to change old rules that no longer apply, change how you organize your people and architect your systems,” he continues. “For the leader, it no longer means directing and controlling, but guiding, enabling, and removing obstacles.

* “That’s not servant leadership, it’s transformational leadership,” Erik says. “It requires understanding the vision of the organization, the intellectual stimulation to question the basic assumptions of how work is performed, inspirational communication, personal recognition, and supportive leadership.

* “Which brings us to the Fourth Ideal of Psychological Safety. No one will take risks, experiment, or innovate in a culture of fear, where people are afraid to tell the boss bad news,” Erik says, laughing. “In those organizations, novelty

* “When something goes wrong, we ask ‘what caused the problem,’ not ‘who.’ We commit to doing what it takes to make tomorrow better than today. As Sensei John Allspaw says, every incident is a learning opportunity, an unplanned investment that was made without our consent.

* Is discouraged, and when problems occur, they ask ‘Who caused the problem?’ They name, blame, and shame that person. They create new rules, more approvals, more training, and, if necessary, rid themselves of the ‘bad apple,’ fooling themselves that they’ve solved the problem,” he says.

* They stare at Erik walking away. Dwayne eventually says, “He’s so right about the Third and Fourth Ideal. What can we do about the culture of fear that’s all around us? Look at what happened to Chad. He tried to do the right thing and got fired. I probably have more reasons to dislike Chad than any of you—those rolling network outages during the day drove me crazy. But firing Chad doesn’t do a damned thing to make those outages less likely in the Future.

* “Oh, my God,” Maxine blurts out, horrified. She knows exactly how this feel. She’s done it several times in her career. You type something, hit enter, and immediately realize you’ve made a huge mistake, but it’s too late. She’s accidentally deleted a customer database table thinking it was the test database. She’s accidentally rebooted the wrong production server, taking down an order entry system for an afternoon. She’s deleted wrong directories, shut down wrong server clusters, and disabled the wrong login credentials.

* “How did we get into this position where someone is so overworked that they’re working four nights in a row? What sort of expectations are being set when someone can’t take a day off when they need to? And what sort of message are we sending when the reward for caring so much is that we fire you?”

* “So, let’s suppose that all our changes work perfectly—when would be the soonest that our customers actually get to use what we wrote?” she asks. Tom starts counting on his fingers. “Two weeks for another testing cycle. Then they open up a ticket with Operations, requesting that they deploy the changes into production. Sometimes it takes a bit of time for them to work it into their schedule … that could take another three weeks.” He looks at his fingers. “So that’d be seven weeks from now.”

* They tell her about the projects they’re working on, which provides a shared context. Then she asks what they find most frustrating about the testing process. The flood gates open. Their pain points and stories sound all too familiar to her: waiting for environments, environments not completely cleaned up, the problems that cascade when something goes wrong, the inability to determine whether problems were caused by errors in the code or something wrong with the environment.

* Maxine once heard a joke: “A QA engineer walks into a bar. Orders a beer. Orders zero beers. Orders 999,999,999 beers. Orders a lizard. Orders negative one beer. Orders a ‘sfdeljknesv.’”

* More and more dependencies, as far as the eye can see, she thinks. There is no place in this whole screwedup system where you can get anything done. It doesn’t matter whether you’re creating the ticket, processing the ticket, waiting on the ticket, or working the ticket. It doesn’t matter. You’re trapped in a web of dependencies, completely unable to get anything done, no matter where you are.

* “… This isn’t over. You somehow managed to find a patron, but she won’t be able to protect you forever. You think you’re better than us? You think you can come in here, put on airs, and automate everyone’s job away? Not on my watch. I’ll make sure we bring you down.” Over the decades, Maxine has tried to explain to nontechnical people how frightening code merges are. Her best description is having fifty screenwriters simultaneously working on a Hollywood script when they haven’t decided who the main characters are, or what the ending will be, or whether it’s a gritty, detective story or a bumbling sleuth with a sidekick. They break up the writing responsibilities between all the writers, and each writer works on their part of the script in isolation, typing away in Word for weeks at a time. Then, right before the script needs to be finalized, all fifty writers get together in a room to merge all their work back together into a single story.

* Maxine loves it when everyone merges their changes frequently to the

* ‘master branch,’ such as once per day. That way, the size of the changes being merged are never allowed to get too large. Small batch sizes, like in manufacturing, create a smooth flow of work, with no jarring disruptions or catastrophes.

* In the dark, Maxine wonders how the oppressive bureaucracy gained so much control.

* Immutability is another concept from functional programming that is making the world a more predictable and safer place, Maxine thinks, smiling.

* Whitespace deployment, Kurt starts the meeting, saying, “Every time we have an outage, we’ll be conducting a blameless postmortem like this one. The spirit and intent of these sessions are to learn from them, chronicling what happened before memories fade. Prevention requires honesty, and honesty requires the absence of fear. Just like Norm Kerth says in the Agile Prime Directive, ‘Regardless of what we discover, we understand and truly believe that everyone did the best job they could, given what they knew at the time, their skills and abilities, the resources available, and the situation at hand.’

* Maxine nods emphatically. She looks at Maggie for several moments and then asks the question she’s been wanting to ask since last night. “Just what does it take to build great products? And how can we as developers help?” “Where do I start?” Maggie says. “It usually begins with understanding who our customers are, both current and desired. Then we typically segment the customer base, so we know what set of problems each faces. Once we know that, we can understand which of those problems we want to solve, based on market size, ease of reaching them, and so forth. Once we know that, we think about pricing and packaging, offer development, and more strategic issues, such as the overall profitability of the product portfolio and how it affects the achievement of strategic goals.

* This is not a story about small beating large; it’s fast beats slow. What the past couple of months have decisively proven to her is that greatness can be stifled, but it can also be restored.

* Maxine is familiar with these techniques. Their use exploded after the famous 2004 Google Map/Reduce research paper was published, which described the techniques Google used to massively parallelize the indexing of the entire internet on commodity hardware, using techniques at the core of functional programming. This led to the invention of Hadoop, Spark, Beam, and so many other exciting technologies that transformed this space, just like NoSQL revolutionized the database landscape.

---


