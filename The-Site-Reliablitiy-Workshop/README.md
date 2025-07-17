## Highlights
 * Page Xxiv (Preface):
   > SRE is a journey as much as it is a discipline.

 * Page 4 (Operations Is a Software Problem): "Operations Is a Software Problem"

 * Page 5 (Work to Minimize Toil):
   > the product team and the SRE team select an appropriate availability target for the service and its user base, and the service is managed to that SLO.

 * Page 5 (Work to Minimize Toil):
   > The Wisdom of Production A note on "the wisdom of production": by this phrase, we mean the wisdom you get from something running in production—the messy details of how it actually behaves, and how software should actually be designed, rather than a whiteboarded view of a service isolated from the facts on the ground. All of the pages you get, the tickets the team  gets,  and  so  on,  are  a  direct  connection  with  reality  that  should  inform  better system design and behavior.

 * Page 5 (Work to Minimize Toil):
   > 9 A service level objective is a target for performance of a particular metric (e.g., available 99.9% of the time).

 * Page 6 (Share Ownership with Developers):
   > SREs are specifically charged with improving undesirably late problem discovery, yielding benefits for the company as a whole.

 * Page 10 (Consider Reliability Work as a Specialized Role): "(Nothing slows down feature development like losing user data.)"

 * Page 10 (Consider Reliability Work as a Specialized Role):
   > • Don't just allow, but actively encourage, engineers to change code and configura‐ tion  when  required  for  the  product.  Also  allow  these  teams  the  authority  to  be radical within the limits of their mission, thereby eliminating incentives to pro‐ ceed more slowly. • Support blameless postmortems.17 Doing so eliminates incentives to downplay or cover up a problem. This step is crucial in fully understanding the product and actually optimizing its performance and functionality, and relies on the wisdom of production mentioned previously.

 * Page 17 (Why SREs Need SLOs): "SLOs are key to making data-driven decisions about reliability,"

 * Page 18 (Getting Started):
   > Your  system's  maturity  level might be one of the following: • A greenfield development, with nothing currently deployed • A  system  in  production  with  some  monitoring  to  notify  you  when  things  go awry, but no formal objectives, no concept of an error budget, and an unspoken goal of 100% uptime • A running deployment with an SLO below 100%, but without a common under‐ standing  about  its  importance  or  how  to  leverage  it  to  make  continuous improvement choices—in other words, an SLO without teeth

 * Page 20 (What to Measure: Using SLIs):
   > Once  you  agree  that  100%  is  the  wrong  number,  how  do  you  determine  the  right number? And what are you measuring, anyway? Here, service level indicators come into play: an SLI is an indicator of the level of service that you are providing.

 * Page 20 (What to Measure: Using SLIs):
   > we generally recommend treating the SLI as the ratio of two numbers: the number of good events divided by the total num‐ ber of events. For example: • Number of successful HTTP requests / total HTTP requests (success rate) • Number  of  gRPC  calls  that  completed  successfully  in  <  100  ms  /  total  gRPC requests • Number  of  search  results  that  used  the  entire  corpus  /  total  number  of  search results, including those that degraded gracefully • Number of "stock check count" requests from product searches that used stock data fresher than 10 minutes / total number of stock check requests • Number  of  "good  user  minutes"  according  to  some  extended  list  of  criteria  for that metric / total number of user minutes

 * Page 20 (What to Measure: Using SLIs):
   > The SLI ranges from 0%  to  100%,  where  0%  means  nothing  works,  and  100%  means  nothing  is  broken.

 * Page 21 (What to Measure: Using SLIs):
   > When attempting to formulate SLIs for the first time, you might find it useful to fur‐ ther divide SLIs into SLI specification and SLI implementation: SLI specification The assessment of service outcome that you think matters to users, independent of how it is measured. For example: Ratio of home page requests that loaded in < 100 ms SLI implementation The SLI specification and a way to measure it. For example: • Ratio of home page requests that loaded in < 100 ms, as measured from the Latency column of the server log. This measurement will miss requests that fail to reach the backend.

 * Page 22 (What to Measure: Using SLIs):
   > Your first attempt at an SLI and SLO doesn't have to be correct; the most important goal is to get something in place and measured, and to set up a feedback loop so you can improve

 * Page 22 (What to Measure: Using SLIs):
   > To create your first set of SLOs, you need to decide upon a few key SLI specifications that matter to your service. Availability and latency SLOs are pretty common; fresh‐ ness,  durability,  correctness,  quality,  and  coverage  SLOs  also  have  their  place

 * Page 22 (What to Measure: Using SLIs):
   > If you are having trouble figuring out what sort of SLIs to start with, it helps to start simple: • Choose one application for which you want to define SLOs. If your product com‐ prises many applications, you can add those later. • Decide clearly who the "users" are in this situation. These are the people whose happiness you are optimizing. • Consider  the  common  ways  your  users  interact  with  your  system—common tasks and critical activities. • Draw  a  high-level  architecture  diagram  of  your  system;  show  the  key  compo‐ nents, the request flow, the data flow, and the critical dependencies. Group these components  into  categories  listed  in  the  following  section  (there  may  be  some overlap and ambiguity; use your intuition and don't let perfect be the enemy of the good).

 * Page 22 (What to Measure: Using SLIs): "Types of components"

 * Page 23 (A Worked Example):
   > Request-driven The  user  creates  some  type  of  event  and  expects  a  response.  For  example,  this could be an HTTP service where the user interacts with a browser or an API for a mobile application. Pipeline A system that takes records as input, mutates them, and places the output some‐ where else. This might be a simple process that runs on a single instance in real time, or a multistage batch process that takes many hours. Examples include: • A system that periodically reads data from a relational database and writes it into a distributed hash table for optimized serving • A video processing service that converts video from one format to another • A system that reads in log files from many sources to generate reports • A  monitoring  system  that  pulls  metrics  from  remote  servers  and  generates time series and alerts Storage A system that accepts data (e.g., bytes, records, files, videos) and makes it avail‐ able to be retrieved at a later date.

 * Page 25 (Moving from SLI Specification to SLI Implementation): "API and HTTP server availability and latency"

 * Page 25 (Moving from SLI Specification to SLI Implementation):
   > Your SLIs should be specific and measurable. To summarize the list of potential can‐ didates provided in "What to Measure: Using SLIs" on page 20, your SLIs can use one or more of the following sources: • Application server logs • Load balancer monitoring • Black-box monitoring • Client-side instrumentation

 * Page 26 (Measuring the SLIs):
   > We have a couple potential approaches to measure correctness: • Inject  data  with  known  outputs  into  the  system,  and  count  the  proportion  of times that the output matches our expectations. • Use a method to calculate correct output based on input that is distinct from our pipeline itself (and likely more expensive, and therefore not suitable for our pipe‐ line). Use this to sample input/output pairs, and count the proportion of correct output  records.  This  methodology  assumes  that  creating  such  a  system  is  both possible and practical.

 * Page 29 (Choosing an Appropriate Time Window):
   > Shorter time windows allow you to make decisions more quickly: if you missed your SLO for the previous week, then small course corrections—prioritizing relevant bugs, for example—can help avoid SLO violations in future weeks.

 * Page 30 (Getting Stakeholder Agreement): "Longer time periods are better for more strategic decisions:"

 * Page 30 (Getting Stakeholder Agreement):
   > We  have  found  a  four-week  rolling  window  to  be  a  good  general-purpose  interval. We complement this time frame with weekly summaries for task prioritization and quarterly summarized reports for project planning.

 * Page 30 (Getting Stakeholder Agreement):
   > But we can also gather interesting informa‐ tion about the distribution. Were there any days during the past four weeks when our service  did  not  meet  its  SLO?  Do  these  days  correlate  with  actual  incidents?  Was there  (or  should  there  have  been)  some  action  taken  on  those  days  in  response  to incidents?

 * Page 31 (Establishing an Error Budget Policy):
   > Getting the error budget policy approved by all key stakeholders—the product man‐ ager, the development team, and the SREs—is a good test for whether the SLOs are fit for purpose: • If  the  SREs  feel  that  the  SLO  is  not  defensible  without  undue  amounts  of  toil, they can make a case for relaxing some of the objectives. • If the development team and product manager feel that the increased resources they'll have to devote to fixing reliability will cause feature release velocity to fall below acceptable levels, then they can also argue for relaxing objectives. Remem‐ ber  that  lowering  the  SLOs  also  lowers  the  number  of  situations  to  which  the SREs will respond; the product manager needs to understand this tradeoff. • If  the  product  manager  feels  that  the  SLO  will  result  in  a  bad  experience  for  a significant  number  of  users  before  the  error  budget  policy  prompts  anyone  to address an issue, the SLOs are likely not tight enough.

 * Page 31 (Establishing an Error Budget Policy):
   > Decide how to move forward and what you need to make the decision: more data, more resources, or a change to the SLI or SLO?

 * Page 31 (Establishing an Error Budget Policy):
   > This policy should cover the specific actions that must be taken when a service has consumed its entire error budget for a given period of time, and specify who will take them. Common owners and actions might include:

 * Page 32 (Documenting the SLO and Error Budget Policy):
   > • The development team gives top priority to bugs relating to reliability issues over the past four weeks. • The development team focuses exclusively on reliability issues until the system is within SLO. This responsibility comes with high-level approval to push back on external feature requests and mandates. • To reduce the risk of more outages, a production freeze halts certain changes to the system until there is sufficient error budget to resume changes.

 * Page 32 (Documenting the SLO and Error Budget Policy):
   > This documentation should include the following information: • The  authors  of  the  SLO,  the  reviewers  (who  checked  it  for  technical  accuracy), and the approvers (who made the business decision about whether it is the right SLO). • The  date  on  which  it  was  approved,  and  the  date  when  it  should  next  be reviewed. • A brief description of the service to give the reader context. • The details of the SLO: the objectives and the SLI implementations. • The details of how the error budget is calculated and consumed. • The rationale behind the numbers, and whether they were derived from experi‐ mental or observational data. Even if the SLOs are totally ad hoc, this fact should be  documented  so  that  future  engineers  reading  the  document  don't  make  bad decisions based upon ad hoc data.

 * Page 36 (Improving the Quality of Your SLO): "Change your SLO"

 * Page 36 (Improving the Quality of Your SLO): "Change your SLI implementation"

 * Page 36 (Improving the Quality of Your SLO): "Institute an aspirational SLO"

 * Page 37 (Decision Making Using SLOs and Error Budgets): "Iterate"

 * Page 37 (Decision Making Using SLOs and Error Budgets):
   > These  steps  may include  improving  monitoring,  improving  testing,  removing  dangerous  dependen‐ cies, or rearchitecting the system to remove known failure types.

 * Page 38 (Advanced Topics):
   > bad  pushes  cost  twice  as  much  error  budget  as  database failures. The numbers prove that addressing the release problem provides much more benefit than investing resources in investigating the server failure.

 * Page 38 (Advanced Topics):
   > suggested courses of action based on three key dimensions: • Performance against SLO • The amount of toil required to operate the service • The level of customer satisfaction with the service

 * Page 38 (Advanced Topics):
   > Table 2-5. SLO decision matrix SLOs Toil Customer satisfaction Met Low High Met Met Low Low High High High Low Met Low High Missed Missed Low Low Missed High High Missed High Low Action Choose to (a) relax release and deployment processes and increase velocity, or (b) step back from the engagement and focus engineering time on services that need more reliability. Tighten SLO. If alerting is generating false positives, reduce sensitivity. Otherwise, temporarily loosen the SLOs (or offload toil) and fix product and/or improve automated fault mitigation. Tighten SLO. Loosen SLO. Increase alerting sensitivity. Loosen SLO. Offload toil and fix product and/or improve automated fault mitigation.

 * Page 39 (Grading Interaction Importance):
   > There‐ fore, you should write SLOs in terms of user-centric actions.

 * Page 39 (Grading Interaction Importance):
   > for an online shopping expe‐ rience, critical user journeys might include: • Searching for a product • Adding a product to a shopping cart • Completing a purchase

 * Page 40 (Modeling Dependencies):
   > For example, if a single component is a critical dependency9 for a particularly highvalue interaction, its reliability guarantee should be at least as high as the reliability guarantee  of  the  dependent  action.  The  team  that  runs  that  particular  component needs to own and manage its service's SLO in the same way as the overarching prod‐ uct SLO.

 * Page 40 (Modeling Dependencies):
   > A dependency is critical if its unavailability means that your service is also unavailable.

 * Page 41 (Experimenting with Relaxing Your SLOs):
   > There  are  two  schools  of  thought  regarding  how  an  error  budget  policy  should address a missed SLO when the failure is caused by a dependency that's handled by another team: • Your team should not halt releases or devote more time to reliability, as your sys‐ tem didn't cause the issue. • You should enact a change freeze in order to minimize the chances of future out‐ ages, regardless of the cause of that outage.

 * Page 41 (Experimenting with Relaxing Your SLOs):
   > This process may allow you to mathematically identify a relationship between a key business  metric  (e.g.,  sales)  and  a  measurable  technical  metric  (e.g.,  latency).  If  it does, you have gained a very valuable piece of data you can use to make important engineering decisions for your service going forward.

 * Page 42 (Conclusion):
   > To summarize: • SLOs are the tool by which you measure your service's reliability. • Error  budgets  are  a  tool  for  balancing  reliability  with  other  engineering  work, and a great way to decide which projects will have the most impact. • You should start using SLOs and error budgets today.

 * Page 47 (Introduction of SLOs: A Journey in Progress):
   > In revising our SLOs, we've also learned that it's important to balance what you would like to measure with what's possible to measure.

 * Page 50 (The SLO Culture Project):
   > Services that depend upon each other need to know information like: • How reliable is your service? Is it built for three 9s, three and a half 9s, or four 9s (or better)? Is there planned downtime? • What kind of latency can I expect at the upper bounds? • Can you handle the volume of requests I am going to send? How do you handle overload? Has your service achieved its SLOs over time?

 * Page 52 (Our First Set of SLOs):
   > Ultimately,  we  decided  that  as  a retailer  we  needed  to  size  our  service  for  peaks  like  Black  Friday,  so  we  set  an  SLO according to expected peak capacity.

 * Page 53 (Our First Set of SLOs):
   > If  a  web  service  encountered  an  error,  we  naturally  standardized  on  HTTP response  codes: • A  service  should  not  indicate  an  error  in  the  body  of  a  2xx  response;  rather,  it should throw either a 4xx or a 5xx. • An  error  caused  by  a  problem  with  the  service  (for  example,  out  of  memory) should throw a 5xx error. • An error caused by the client (for example, sending a malformed request) should throw a 4xx error.

 * Page 59 (Summary):
   > Here's an example of simpli‐ fied VALET metrics we might provide: • 99.5%:  Applications  that  are  not  used  by  store  associates  or  an  MVP  of  a  new service • 99.9%: Adequate for the majority of nonselling systems at THD • 99.95%: Selling systems (or services that support selling systems) • 99.99%: Shared infrastructure services

 * Page 60 (Conclusion):
   > These  two  case  studies  highlight  that  SLO  culture  is  an  ongoing  process  and  not  a one-time fix or solution.

 * Page 61 (Chapter 4. Monitoring):
   > some  basic  monitoring definitions and explains that SREs monitor their systems in order to: • Alert on conditions that require attention. • Investigate and diagnose those issues. • Display information about the system visually. • Gain  insight  into  trends  in  resource  usage  or  service  health  for  long-term planning. • Compare the behavior of the system before and after a change, or between two groups in an experiment.

 * Page 62 (Calculations):
   > Data  should  be  available  when  you  need  it:  freshness  impacts  how  long  it  will  take your monitoring system to page you when something goes wrong.

 * Page 63 (Interfaces):
   > if your system doesn't support computing percentiles directly, you can achieve this by: • Obtaining a mean value by summing the seconds spent in requests and dividing by the number of requests • Logging every request and computing the percentile values by scanning or sam‐ pling the log entries

 * Page 64 (Sources of Monitoring Data):
   > Metrics  are  numerical  measurements  representing  attributes  and  events,  typically harvested  via  many  data  points  at  regular  time  intervals.

 * Page 64 (Sources of Monitoring Data): "Logs  are  an  append-only record of events."

 * Page 64 (Sources of Monitoring Data):
   > There's some inherent delay between when an event occurs and when it is visible in logs. For analysis  that's  not  time-sensitive,  these  logs  can  be  processed  with  a  batch  system, interrogated with ad hoc queries, and visualized with dashboards.

 * Page 67 (Treat Your Configuration as Code): "Treat Your Configuration as Code"

 * Page 68 (Prefer Loose Coupling): "Encourage Consistency"

 * Page 68 (Prefer Loose Coupling):
   > If  possible,  make  basic  monitoring  coverage  effortless.  If  all  your  services2  export  a consistent  set  of  basic  metrics,  you  can  automatically  collect  those  metrics  across your  entire  organization  and  provide  a  consistent  set  of  dashboards.  This  approach means  that  any  new  component  you  launch  automatically  has  basic  monitoring. Many teams across your company—even nonengineering teams—can use this moni‐ toring data.

 * Page 68 (Prefer Loose Coupling): "Prefer Loose Coupling"

 * Page 69 (Metrics with Purpose):
   > As  of  this  writing,  there  are  at  least  two  popular  open  standards  for  instrumenting your software and exposing metrics: statsd The  metric  aggregation  daemon  initially  written  by  Etsy  and  now  ported  to  a majority of programming languages. Prometheus An open source monitoring solution with a flexible data model, support for met‐ ric  labels,  and  robust  histogram  functionality.  Other  systems  are  now  adopting the Prometheus format, and it is being standardized as OpenMetrics.

 * Page 70 (Dependencies): "Intended Changes"

 * Page 70 (Dependencies):
   > Add monitor‐ ing that informs you of any changes in production.4 To determine the trigger, we rec‐ ommend the following: • Monitor the version of the binary. • Monitor  the  command-line  flags,  especially  when  you  use  these  flags  to  enable and disable features of the service. • If configuration data is pushed to your service dynamically, monitor the version of this dynamic configuration.

 * Page 70 (Dependencies): "Dependencies"

 * Page 71 (Saturation):
   > If this depend‐ ency is critical, you have a couple of options to monitor it well: • Export  separate  metrics  to  tailor  for  the  dependency,  so  that  the  metrics  can unpack requests they receive to get at the actual signal. • Ask  the  dependency  owners  to  perform  a  rewrite  to  export  a  broader  API  that supports separate functionality split across separate RPC services and methods.

 * Page 71 (Saturation): "Saturation"

 * Page 71 (Saturation):
   > Depending  on  the  programming  language  in  use,  you  should  monitor  additional resources: • In  Java:  The  heap  and  metaspace  size,  and  more  specific  metrics  depending  on what type of garbage collection you're using • In Go: The number of goroutines

 * Page 71 (Saturation):
   > need to set up alerting that fires when you approach exhaustion for specific resources, such as: • When the resource has a hard limit • When crossing a usage threshold causes performance degradation

 * Page 72 (Testing Alerting Logic):
   > It's  a  good  idea  to  add  metrics  or  metric  labels  that  allow  the  dashboards  to  break down served traffic by status code (unless the metrics your service uses for SLI pur‐ poses already include this information). Here are some recommendations: • For HTTP traffic, monitor all response codes, even if they don't provide enough signal for alerting, because some can be triggered by incorrect client behavior. • If you apply rate limits or quota limits to your users, monitor aggregates of how many requests were denied due to lack of quota.

 * Page 72 (Testing Alerting Logic):
   > When  you  write  a  postmortem,  think  about  which  additional  metrics would have allowed you to diagnose the issue faster.

 * Page 73 (Testing Alerting Logic):
   > Monitoring testing environment tiers 1. Binary  reporting:  Check  that  the  exported  metric  variables  change  in  value under certain conditions as expected. 2. Monitoring  configurations:  Make  sure  that  rule  evaluation  produces  expected results, and that specific conditions produce the expected alerts. 3. Alerting  configurations:  Test  that  generated  alerts  are  routed  to  a  predeter‐ mined destination, based on alert label values.

 * Page 76 (1: Target Error Rate ≥ SLO Threshold):
   > Precision The  proportion  of  events  detected  that  were  significant.  Precision  is  100%  if every alert corresponds to a significant event. Note that alerting can become par‐ ticularly  sensitive  to  nonsignificant  events  during  low-traffic  periods  (discussed in "Low-Traffic Services and Error Budget Alerting" on page 86). Recall The proportion of significant events detected. Recall is 100% if every significant event results in an alert. Detection time How  long  it  takes  to  send  notifications  in  various  conditions.  Long  detection times can negatively impact the error budget. Reset time How long alerts fire after an issue is resolved. Long reset times can lead to confu‐ sion or to issues being ignored.

 * Page 81 (4: Alert on Burn Rate):
   > For burn rate–based alerts, the time taken for an alert to fire is: 1 − SLO error ratio × alerting window size × burn rate The error budget consumed by the time the alert fires is: burn rate × alerting window size period

 * Page 82 (5: Multiple Burn Rate Alerts):
   > We recommend 2% budget consumption in one hour and 5% budget consumption in six hours as reasonable starting numbers for paging, and 10% budget consumption in three  days  as  a  good  baseline  for  ticket  alerts.

 * Page 82 (5: Multiple Burn Rate Alerts):
   > Table 5-6. Recommended time windows and burn rates for percentages of SLO budget consumed SLO budget consumption Time window Burn rate Notification 2% 5% 10% 1 hour 6 hours 3 days Page Page Ticket 14.4 6 1 82 | Chapter 5: Alerting on SLOs

 * Page 85 (6: Multiwindow, Multi-Burn-Rate Alerts):
   > We have found that alerting based on multiple burn rates is a powerful way to imple‐ ment SLO-based alerting.

 * Page 86 (Low-Traffic Services and Error Budget Alerting):
   > We recommend a few key options to handle a low-traffic service: • Generate artificial traffic to compensate for the lack of signal from real users. • Combine smaller services into a larger service for monitoring purposes. • Modify the product so that either: — It takes more requests to qualify a single incident as a failure. — The impact of a single failure is lower.

 * Page 88 (Lowering the SLO or Increasing the Window):
   > In practice, we use some combination of the following methods to alert for low-traffic services: • Generating fake traffic, when doing so is possible and can achieve good coverage • Modifying clients so that ephemeral failures are less likely to cause user harm • Aggregating smaller services that share some failure mode • Setting SLO thresholds commensurate with the actual impact of a failed request

 * Page 90 (Alerting at Scale):
   > with availability and latency SLOs, you can group its request types into the following buckets: CRITICAL For request types that are the most important, such as a request when a user logs in to the service. HIGH_FAST For requests with high availability and low latency requirements. These requests involve core interactive functionality, such as when a user clicks a button to see how much money their advertising inventory has made this month. HIGH_SLOW For important but less latency-sensitive functionality, such as when a user clicks a button to generate a report of all advertising campaigns over the past few years, and does not expect the data to return instantly. LOW For requests that must have some availability, but for which outages are mostly invisible  to  users—for  example,  polling  handlers  for  account  notifications  that can fail for long periods of time with no user impact. NO_SLO For  functionality  that  is  completely  invisible  to  the  user—for  example,  dark launches or alpha functionality that is explicitly outside of any SLO.

 * Page 94 (What Is Toil?):
   > Here,  we  provide  a  concrete  example  for  each  toil characteristic: Manual When the tmp directory on a web server reaches 95% utilization, engineer Anne logs in to the server and scours the filesystem for extraneous log files to delete. Repetitive A full tmp directory is unlikely to be a one-time event, so the task of fixing it is repetitive. Automatable1 If your team has remediation documents with content like "log in to X, execute this  command,  check  the  output,  restart  Y  if  you  see...,"  these  instructions  are essentially pseudocode to someone with software development skills! In the tmp directory  example,  the  solution  has  been  partially  automated.  It  would  be  even better to fully automate the problem detection and remediation by not requiring a  human  to  run  the  script.  Better  still,  submit  a  patch  so  that  the  software  no longer breaks in this way. Nontactical/reactive When  you  receive  too  many  alerts  along  the  lines  of  "disk  full"  and  "server down,"  they  distract  engineers  from  higher-value  engineering  and  potentially mask other, higher-severity alerts. As a result, the health of the service suffers. Lacks enduring value Completing  a  task  often  brings  a  satisfying  sense  of  accomplishment,  but  this repetitive  satisfaction  isn't  a  positive  in  the  long  run.  For  example,  closing  that alert-generated ticket ensured that the user queries continued to flow and HTTP requests  continued  to  serve  with  status  codes  <  400,  which  is  good.  However, resolving  the  ticket  today  won't  prevent  the  issue  in  the  future,  so  the  payback has a short duration. Grows at least as fast as its source Many classes of operational work grow as fast as (or faster than) the size of the underlying  infrastructure.  For  example,  you  can  expect  time  spent  performing

 * Page 95 (What Is Toil?):
   > Time  spent  working  on  toil  is generally time not spent thinking critically or expressing creativity; reducing toil is an acknowledgment  that  an  engineer's  effort  is  better  utilized  in  areas  where  human judgment and expression are possible.

 * Page 96 (Measuring Toil):
   > Before beginning toil reduction projects, it's important to analyze cost versus benefit and  to  confirm  that  the  time  saved  through  eliminating  toil  will  (at  minimum)  be proportional to the time invested in first developing and then maintaining an auto‐ mated solution

 * Page 102 (Provide Self-Service Methods):
   > Working with toil in larger aggregates reduces interrupts and helps you identify patterns of toil, which you can then target for elimination.

 * Page 118 (Lessons Learned): "UIs should not introduce overhead or complexity"

 * Page 118 (Lessons Learned): "Don't rely on human expertise"

 * Page 119 (Lessons Learned): "Design reusable components"

 * Page 119 (Lessons Learned): "Don't overthink the problem"

 * Page 119 (Lessons Learned): "Sometimes imperfect automation is good enough"

 * Page 119 (Lessons Learned): "Repair automation is not fire and forget"

 * Page 120 (Lessons Learned): "Build in risk assessment and defense in depth"

 * Page 120 (Lessons Learned): "Get a failure budget and manager support"

 * Page 120 (Lessons Learned): "Think holistically"

 * Page 127 (Lessons Learned): "Challenge assumptions and retire expensive business processes"

 * Page 127 (Lessons Learned): "Build self-service interfaces"

 * Page 127 (Lessons Learned): "Start with human-backed interfaces"

 * Page 128 (Lessons Learned): "Melt snowflakes"

 * Page 129 (Conclusion): "Employ organizational nudges"

 * Page 129 (Conclusion):
   > Once  you  identify  toil,  it's  crucial  to  determine  when  toil  reduction makes  sense,  using  metrics,  return  on  investment  (ROI)  analysis,  risk  assessment, and iterative development.

 * Page 132 (Measuring Complexity):
   > Some more practical proxies for systems-level complexity include: Training time How long does it take a new team member to go on-call? Poor or missing docu‐ mentation can be a significant source of subjective complexity. Explanation time How long does it take to explain a comprehensive high-level view of the service to  a  new  team  member  (e.g.,  diagram  the  system  architecture  on  a  whiteboard and explain the functionality and dependencies of each component)? Administrative diversity How  many  ways  are  there  to  configure  similar  settings  in  different  parts  of  the system? Is configuration stored in a centralized place, or in multiple locations? Diversity of deployed configurations How many unique configurations are deployed in production (including binar‐ ies, binary versions, flags, and environments)? Age How old is the system? Hyrum's Law states that over time, the users of an API depend on every aspect of its implementation, resulting in fragile and unpredict‐ able behaviors.

 * Page 133 (Simplicity Is End-to-End, and SREs Are Good for That):
   > Reader  action:  Before  an  engineer  goes  on-call  for  the  first  time, encourage  them  to  draw  (and  redraw)  system  diagrams.  Keep  a canonical set of diagrams in your documentation: they're useful to new engineers and help more experienced engineers keep up with changes

 * Page 135 (Regaining Simplicity):
   > When considering a rewrite, think about the full project lifecycle, including develop‐ ment toward a moving target, a full migration plan, and extra costs you might incur during  the  migration  time  window.  Wide  APIs  with  lots  of  users  are  very  hard  to migrate. Don't compare the expected result to your current system. Instead, compare the expected result to what your current system would look like if you invested the same effort in improving it. Sometimes a rewrite is the best way forward, but make sure  you've  weighed  the  costs  and  benefits  and  that  you  don't  underestimate  the costs.

 * Page 145 (Part II. Practices):
   > themselves into all of your work. You don't need to think about documenting code, playbooks,  and  service  features—or  even  making  sure  that  tickets  and  bugs  contain all  of  the  information  they  should—as  separate  from  your  project  or  operational tasks. It's simply another facet of those tasks.

 * Page 151 (Google: Forming a New Team):
   > Before going on-call, the team reviewed precise guidelines about the responsibilities of on-call engineers. For example: • At the start of each shift, the on-call engineer reads the handoff from the previ‐ ous shift. • The on-call engineer minimizes user impact first, then makes sure the issues are fully addressed. • At  the  end  of  the  shift,  the  on-call  engineer  sends  a  handoff  email  to  the  next engineer on-call.

 * Page 154 (Evernote: Finding Our Feet in the Cloud):
   > One of the ways we achieve this is to keep our signal-to-noise ratio low by maintain‐ ing  simple  but  effective  alerting  SLAs  (service  level  agreements).  We  classify  any event generated by our metrics or monitoring infrastructure into three categories: P1: Deal with immediately • Should be immediately actionable • Pages the on-call • Leads to event triage • Is SLO-impacting P2: Deal with the next business day • Generally is not customer-facing, or is very limited in scope • Sends an email to team and notifies event stream channel P3: Event is informational only • Information is gathered in dashboards, passive email, and the like • Includes capacity planning–related information

 * Page 155 (Evernote: Finding Our Feet in the Cloud):
   > Any P1 or P2 event has an incident ticket attached to it. The ticket is used for obvious tasks  like  event  triage  and  tracking  remediation  actions,  as  well  as  for  SLO  impact, number of occurrences, and postmortem doc links, where applicable.

 * Page 158 (Anatomy of Pager Load):
   > Pager load is  influenced  by  three  main  factors:  bugs5  in  production,  alerting,  and  human  pro‐ cesses.

 * Page 159 (Anatomy of Pager Load):
   > prevent bugs that haven't yet caused paging alerts: • Ensure systems are as complicated as they need to be, and no more (see Chap‐ ter 7). • Regularly update the software or libraries that your system is built upon to take advantage of bug fixes (however, see the next section about new bugs). • Perform regular destructive testing or fuzzing (for example, using Netflix's Chaos Monkey). • Perform regular load testing in addition to integration and unit testing.

 * Page 159 (Anatomy of Pager Load):
   > However,  software  testing  techniques  are  particularly  useful  in  reducing  the number of bugs that reach production, and the amount of time they remain in pro‐ duction: • Improve  testing  over  time.  In  particular,  for  each  bug  you  discover  in  produc‐ tion, ask "How could we have detected this bug preproduction?" Make sure the necessary engineering follow-up occurs (see "Rigor of follow-up" on page 164).

 * Page 160 (Anatomy of Pager Load):
   > • Have  a  low  tolerance  to  new  bugs.  Follow  a  "detect,  roll  back,  fix,  and  roll  for‐ ward" strategy rather than a "detect, continue to roll forward despite identifying the bug, fix, and roll forward again" strategy. (See "Mitigation delay" on page 162 for more details.)

 * Page 160 (Anatomy of Pager Load):
   > Some bugs may manifest only as the result of changing client behavior. For example: • Bugs  that  manifest  only  under  specific  levels  of  load—for  example,  September back-to-school  traffic,  Black  Friday,  Cyber  Monday,  or  that  week  of  the  year when  Daylight  Saving  Time  means  Europe  and  North  America  are  one  hour closer, meaning more of your users are awake and online simultaneously. • Bugs that manifest only with a particular mix of requests—for example, servers closer to Asia experiencing a more expensive traffic mix due to language encod‐ ings for Asian character sets. • Bugs that manifest only when users exercise the system in unexpected ways—for example,  Calendar  being  used  by  an  airline  reservation  system!  Therefore,  it  is important  to  expand  your  testing  regimen  to  test  behaviors  that  do  not  occur every day.

 * Page 160 (Anatomy of Pager Load):
   > Minimizing the number of bugs in production not only reduces pager load, it also makes identifying and clas‐ sifying new bugs easier.

 * Page 161 (Anatomy of Pager Load):
   > This data revealed that human error was the second most common cause of new bugs in production.

 * Page 161 (Anatomy of Pager Load):
   > Identification delay.    It's important to promptly identify the cause(s) of alerts because the longer it takes to identify the root cause of a page, the more opportunity it has to recur and page again.

 * Page 161 (Anatomy of Pager Load): "Use good alerts and consoles"

 * Page 161 (Anatomy of Pager Load): "Practice emergency response"

 * Page 161 (Anatomy of Pager Load): "Perform small releases"

 * Page 161 (Anatomy of Pager Load): "Log changes"

 * Page 162 (Anatomy of Pager Load): "Ask for help"

 * Page 162 (Anatomy of Pager Load):
   > Mitigation delay.    The longer it takes to mitigate a bug once it's identified, the more opportunity  it  has  to  recur  and  page  again.

 * Page 162 (Anatomy of Pager Load):
   > Generally,  it  is  better  to  "roll  back,  fix,  and  roll  forward"  rather  than "roll forward, fix, and roll forward again."

 * Page 162 (Anatomy of Pager Load): "Use feature isolation"

 * Page 162 (Anatomy of Pager Load): "Drain requests away"

 * Page 165 (Anatomy of Pager Load):
   > To  make  sure  you're  thorough  in  your  follow-up  to  paging  alerts,  consider  the  fol‐ lowing questions: • How can I prevent this specific bug from happening again? • How can I prevent bugs like this from happening again, both for this system and other systems I'm responsible for? • What tests could have prevented this bug from being released to production? • What ticket alerts could have triggered action to prevent the bug from becoming critical before it paged? • What  informational  alerts  could  have  surfaced  the  bug  on  a  console  before  it became critical? • Have I maximized the impact of the fixes I'm making?

 * Page 165 (Anatomy of Pager Load):
   > Data quality.    Once you identify bugs in your system that caused pages, a number of questions naturally arise: • How do you know which bug to fix first? • How do you know which component in your system caused most of your pages? • How do you determine what repetitive, manual action on-call engineers are tak‐ ing to resolve the pages? • How do you tell how many alerts with unidentified root causes remain? • How do you tell which bugs are truly, not just anecdotally, the worst?

 * Page 166 (Anatomy of Pager Load):
   > Tying structured data to bugs and the root causes of your pages has other benefits: • You  can  automatically  populate  a  list  of  existing  bugs  (that  is,  known  issues), which may be useful for your support team. • You can automatically prioritize fixing bugs based on the number of pages each bug causes.

 * Page 168 (On-Call Flexibility):
   > We encourage embracing flexibility as a principle rather than simply adopting the examples listed here.

 * Page 169 (On-Call Flexibility):
   > Decentralization options range from a fully centralized pol‐ icy,  where  only  the  manager  can  change  the  schedule,  to  a  fully  decentralized  one,

 * Page 172 (On-Call Team Dynamics):
   > SREs take on the previously mentioned "error rate versus error ratio" debate by negotiating a change in alerting with the feature develop‐ ers.

 * Page 173 (Conclusion):
   > We've  also  found  that  making  all  members  of  the  on-call  rotation  sit  together, regardless of job title and function area, helps improve team relations tremendously. Encourage teams to eat lunch with each other. Don't underestimate the power of rel‐ atively straightforward changes like these. It plays directly into team dynamics.

 * Page 175 (Chapter 9. Incident Response): "The  basic  principles  of  incident  response include the following:"

 * Page 176 (Incident Command System):
   > • Maintain a clear line of command. • Designate clearly defined roles. • Keep a working record of debugging and mitigation as you go. • Declare incidents early and often.

 * Page 176 (Incident Command System):
   > Incident  response  frameworks  have  three  common  goals,  also  known  as  the  "three Cs" (3Cs) of incident management: • Coordinate response effort. • Communicate between incident responders, within the organization, and to the outside world. • Maintain control over the incident response.

 * Page 180 (Case Study 2: Service Fault—Cache Me If You Can):
   > we  should  have  conducted  rollouts  during  business  hours  or  organized  an on-call rotation that provided paid coverage outside of business hours.

 * Page 180 (Case Study 2: Service Fault—Cache Me If You Can):
   > Declaring  an  incident early ensures that: • Miscommunication between the client and server developers is prevented. • Root-cause identification and incident resolution occur sooner. • Relevant teams are looped in earlier, making external communications faster and smoother.

 * Page 185 (Case Study 3: Power Outage—Lightning Never Strikes Twice…Until It Does):
   > It's important to remember that first responders must prioritize mitigation above all else, or time to resolution suffers. Having a generic mitigation in place, such as roll‐ back and drain, speeds recovery and leads to happier customers. Ultimately, custom‐ ers  do  not  care  whether  or  not  you  fully  understand  what  caused  an  outage.  What they want is to stop receiving errors.

 * Page 185 (Case Study 3: Power Outage—Lightning Never Strikes Twice…Until It Does):
   > With mitigation as top priority, an active incident should be addressed as follows: 1. Assess the impact of the incident. 2. Mitigate the impact. 3. Perform a root-cause analysis of the incident. 4. After the incident is over, fix what caused the incident and write a postmortem.

 * Page 212 (Good Postmortem): "Why Is This Postmortem Better?"

 * Page 212 (Good Postmortem):
   > This postmortem exemplifies several good writing practices. Clarity The  postmortem  is  well  organized  and  explains  key  terms  in  sufficient  detail.  For example: Glossary A well-written glossary makes the postmortem accessible and comprehensible to a broad audience. Action items This  was  a  large  incident  with  many  action  items.  Grouping  action  items  by theme makes it easier to assign owners and priorities.

 * Page 213 (Why Is This Postmortem Better?):
   > Quantifiable metrics The  postmortem  presents  useful  data  on  the  incident,  such  as  cache  hit  ratios, traffic  levels,  and  duration  of  the  impact.  Relevant  sections  of  the  data  are  pre‐ sented  with  links  back  to  the  original  sources.  This  data  transparency  removes ambiguity and provides context for the reader. Concrete action items A postmortem with no action items is ineffective. These action items have a few nota‐ ble characteristics: Ownership All action items have both an owner and a tracking number. Prioritization All action items are assigned a priority level. Measurability The action items have a verifiable end state (e.g., "Add an alert when more than X% of our machines have been taken away from us"). Preventative action Each action item "theme" has Prevent/Mitigate action items that help avoid out‐ age  recurrence  (for  example,  "Disallow  any  single  operation  from  affecting servers spanning namespace/class boundaries"). Blamelessness The authors focused on the gaps in system design that permitted undesirable failure modes. For example: Things that went poorly No individual or team is blamed for the incident. Root cause and trigger Focuses on "what" went wrong, not "who" caused the incident. Action items Are aimed at improving the system instead of improving people. Depth Rather than only investigating the proximate area of the system failure, the postmor‐ tem explores the impact and system flaws across multiple teams. Specifically:

 * Page 214 (Model and Enforce Blameless Behavior):
   > Impact This  section  contains  lots  of  details  from  various  perspectives,  making  it  bal‐ anced and objective. Root cause and trigger This section performs a deep dive on the incident and arrives at a root cause and trigger. Data-driven conclusions All  of  the  conclusions  presented  are  based  on  facts  and  data.  Any  data  used  to arrive at a conclusion is linked from the document. Additional resources These  present  further  useful  information  in  the  form  of  graphs.  Graphs  are explained to give context to readers who aren't familiar with the system.

 * Page 218 (Respond to Postmortem Culture Failures): "Respond to Postmortem Culture Failures"

 * Page 218 (Respond to Postmortem Culture Failures): "Avoiding association"

 * Page 219 (Respond to Postmortem Culture Failures): "Failing to reinforce the culture"

 * Page 219 (Respond to Postmortem Culture Failures):
   > the  following  statement  made  by  senior  leadership  at  a  meeting  about  an outage: VP  Ash:  I  know  we  are  supposed  to  be  blameless,  but  this  is  a  safe  space.  Someone must  have  known  beforehand  this  was  a  bad  idea,  so  why  didn't  you  listen  to  that person? Mitigate  the  damage  by  moving  the  narrative  in  a  more  constructive  direction.  For example: SRE  Dana:  Hmmm,  I'm  sure  everyone  had  the  best  intent,  so  to  keep  it  blameless, maybe we ask generically if there were any warning signs we could have heeded, and why we might have dismissed them.

 * Page 219 (Respond to Postmortem Culture Failures): "Lacking time to write postmortems"

 * Page 219 (Respond to Postmortem Culture Failures):
   > Repeating incidents If  teams  are  experiencing  failures  that  mirror  previous  incidents,  it's  time  to  dig deeper. Consider asking questions like: • Are action items taking too long to close? • Is feature velocity trumping reliability fixes? • Are the right action items being captured in the first place? • Is the faulty service overdue for a refactor? • Are people putting Band-Aids on a more serious problem?

 * Page 227 (Maglev):
   > All packets destined for a given IP address can be evenly spread across a pool of Maglev  machines  via  Equal-Cost  Multi-Path  (ECMP)  forwarding

 * Page 238 (Avoiding Overloading Backends):
   > Including Kill Switches and Manual Overrides It's  a  good  idea  to  have  a  kill  switch  in  case  something  goes  wrong  with  your autoscaling. Make sure your on-call engineers understand how to disable autoscaling and  how  to  manually  scale  if  necessary.  Your  autoscaling  kill  switch  functionality should be easy, obvious, fast, and well documented.

 * Page 239 (Combining Strategies to Manage Load):
   > Or perhaps your data processing pipeline lives in a Kubernetes cluster in one cloud region. When data processing slows significantly, it provisions more pods to handle the work. However, when data comes in so fast that reading it causes you to run out of memory, or slows down garbage collection, your pods may need to shed that load temporarily or permanently. In this case, your system needs to use both load-based autoscaling and load shedding techniques.

