# POET Working Group 
## **P**angeo **O**utreach **E**ducation **T**raining 

### Statement of Purpose

The POET working group helps researchers and others accurately perceive and benefit from the pangeo program.
The following narrative uses 'we' to presumptively mean 'members of the pangeo community'.


**First organizing principle** How we describe pangeo really depends on context; and we begin here with two 
flavors of description that address both the broad community of data scientists and the narrower scope of 
Big Data (say by Volume) research computing. 


First description: Pangeo is taken to be a community of tool-builders and therefore resulting tools. These tools enable 
us to do data science more effectively; so to the person approaching pangeo we can answer 'What is pangeo?' 
with an invitation to participate. 'Pangeo is tool-builder scientists and -- good news -- you are invited to join, 
participate, benefit, and contribute.' This incorporates the practical idea that not all data-driven research depends
upon having a dask scheduler that fires up a 100-VM cluster.


Now to a second description: Pangeo is a set of cloud-based technologies -- really a platform and a 
computing ecosystem -- that take advantage of cloud scale to enable large-scale computation: In geoscience
and as it grows in other domains such as astronomy and neuroscience.


Let's see how well we can make use of these two stock answers and continue to more POET considerations.


As the 'learning and advocacy working group' within the pangeo community, POETs are first confronted with the task of
organizing information -- including training materials -- into a findable and usable format. This is why the education-materials
repo maintains the resource table on its front page (and pushes the working group machinery to here). Let's conclude this
section with a second organizing principle, the first being the "two answers" given above. 


**Second organizing principle** So you are a scientist inbound to pangeo. Where do you go and where does your data go? 
Should you copy it from Cheyenne to AWS? Should you just pip install pangeo on the Google cloud? This is the big 
information organizing task that falls to POETs. So get to work. 



## Pangeo technical framework


This section needs written. 


## POETs topics and action items


| Project | Description (Leads) |
| ----------------- | ----------- |
| Pangeo Core | Develop a core curriculum for pangeo; emphasis on *by reference* (e.g. 'use Jake') rather than *ab initio*; and emphasis as well on "What are the learning outcomes?" and "3 essential things" rather than "20 good things to have" (Anthony, ...) |
| Curriculum Case Studies | Pangeo in the classroom: How to, small scale first (Julia, Lindsey, Dax, David, Phil, ...) |
| Scientist Case Studies | description (leads) |
| Tire Kicker | Review references (main table); produce reviews and feedback (Rob, ...)  |
| Maintain | Per [Issue 5](https://github.com/pangeo-data/education-material/issues/5) and this related [Discourse issue](https://discourse.jupyter.org/t/testing-notebooks/701) we have an open challenge (leads) |
| The Book | Jupytext... Jupyter Book... mods? and etcetera. Support proposal possible. (Ryan, Ryan's sprint crew, plus Lindsey, Chris, Phil, ...) |
| Help | [Discourse](https://discourse.jupyter.org) as a forum alternative to GitHub (leads) |
| Post-launch QA/QC | Now that you've gotten training, gotten on the platform, are excited about using pangeo: How do we keep you airborn and moving forward? Addressing the transition from 'Pangeo: I get it' to 'Pangeo is what I use'. (Ariel) |
| Data publication 1 | cf Ryan's white paper idea. Integration with STAC. How do I do it? What is important: Being on the cloud? Being in COG or ZARR format? How much metadata is enough metadata? (leads) |
| Data publication 2 | What should NASA publish on the public cloud? NOAA? EPA? ...etc... (Joe, Ryan, Chelle) |
| Package authorship | description (leads) | 
| Lightning in a bottle | Now that we have a success let's capture that into the history of pangeo (Erin) |
| What GPU Don't Know Can Slow You Down | description (Matt) |
| Education event streamlining | what we already do informally: Does it need improvement? (leads) |
| Binder | Practical considerations and details on sharing notebooks effectively (Rob) |
| Jupyter Community Workshop proposal for pangeo | description (Lindsey) |
| DAG YML Decision Shrub | description (Chris) |


# POETs  

* Ryan Abernathy (@rabernat) Columbia
* Anthony Arendt (@aaarendt) UW eScience / Applied Physics Laboratory
* Philip Austin (@phaustin) Chair Atmospheric Sciences Programme at UBC EOASciences
* Deepak 
* Erin Dougherty
* Rob Fatland (@robfatland) UW eScience/IT Research Computing Director
* Joe Hamman (@jhamman) NCAR
* Scott Henderson (@scottyhq) UW eScience 
* Chris Holdgraf UCBerkeley
* Julia Kent NCAR 
* Lindsey Heagy UCBerkeley
* Robin IPCC
* Ariel Rokem UW eScience
* Elizabeth Maroon
* David Shean UW Civil Engineering
* Dax Soule (@daxsoule) QCNY
* Amanda Tan (@amanda-tan) UW eScience


# Source notes

## August 21 22 23 pangeo community meeting UW Alder Hall

### Wednesday 4pm Aug 21

- Leading Open Questions on Education
  - "What is unclear or perhaps confusing about pangeo?" as path to "Who and what and how is pangeo teaching?"
  - How should the pangeo Education WG play a role in testing pangeo tech?
  - Does "publications = evidence of pangeo impact" motivate "What should the pangeo team emphasize today?" (Education, *)
  - Value of "Get dataset X wired into pangeo"  
    - Idea is to motivate scientists who use X to migrate to pangeo
    - What is { X } ? 
    - Process to select and import X? 
    - Should Pangeo Ed teach you how to import your own X?


### Thursday Aug 22

- Anthony: Expand on what we have as a starting point; += 
- Robin: Training, using Jupyter notebooks; recreate climate science figures
- Shean: I have to teach now; examples that bridge the gap between small to large scale problems
- Amanda: Only 5 AGU abstracts from pangeo; how do we expand outside this core user grou3 years in!
- Deepak: NCAR, xarray
- Phil Austin: UBC, invested in Jupyter, 12000 accounts; curriculum, 
- Elizabeth Maroon: Teaching data analysis; students
- Lindsey Heagy: Postdoc geophysics Jupyter team: Community around educational resources; hacks; like geosci; not reinvent base level stuff
- Julia, NCAR, interest in EPO from STEM; improving documentation; for ease of use; hosting tutorial for scientists; 200; from all fields; 
- Chris at UCB on Jupyter; two interesting things: How do you define the pattern of shared infrastructure to improve educational outcomes; and using the pangeo stack as highlighting the benefit of the massive resources; so hearts and minds buying into these platforms; and then what are things we could build that facilitate learning. The dask scheduler widget popup being an example. 
- Dax: QC-CUNY. Teaching faculty how to access OOI data using Jupyter; PI on grant on Project Eddy: Data-driven pedagogies. Student pathway from novice to self-sufficient. Data science as core of liberal arts. 

- Curated bootstrapping list seems a consensus concept
  - Jake's book as an example 
  - Core track 3 must-do
  - Pedagogy notebook that does some reverse engineering
- What does it mean to teach pangeo? (AT)
  - It is all these tools; 
  - AA: What are the learning outcomes; take a pedagogical approach
  - Dax: UNIX as context really helps build the context web going into Python  

TASK: Develop a core curriculum for learning pangeo (AA)


Deep: It is stuff for scientists; then pangeo for sysadmins. Ultimately helping... 

DS: If we're trying to teach datascience you don't need a 5TB datacenter. People don't need dask clusters. 

Rob: I think pangeo is a community teaching service...

Lindsey: Who is the first group as target audience? (Scientists!) 

Lindsey: Case history or use-case driven approach. (This is what Joe suggested also) 

TASK: Phil: September teaching a PBL class: Includes all-comers sessions. 15-20 supernumeraries: So this is our first registered project. 

DS: "I am here, here is what I want to do..." decision tree. decision shrub. 

Chris: DAG yml file 

TASK: DAG per Chris, Shean

Chris: How do we generate organized feedback into the organization? 

Lindsey: Get multiple people contributing in a coherent way. The Case History driven approach gets to a framework: Same 7 steps. This suggests

TASK: Lindsey: Common framework for a pangeo case history. Perhaps two kinds: Analysis template and technical template. 

[example from em](https://em.geosci.xyz/content/case_histories/mt_isa/index.html)


Anthony: Given 3 days to teach pangeo... thought experiment. 

Example: Laptop is swapping, 2000 satellite images, where do I go next? 


TASK: Ryan's book. Phil: Jupytext. You never check notebooks in. You check Python in. 

Chris: Agree on Jupytext. Automatic 2-way synch. Work in nb, save, saves in Python or MD. Add to .ignore anything that ends in ipynb. Also Ryan mentioned JupyterBook: Jupytext uner the hood is something he'd been meaning to add. 

Phil: Cross-referencing also needed. This is a green light that such a book is feasible. 

Lindsey: There are Jupyter community workshops. Did a sprint and wrote a book in 3 days. 80% of the work got done in three days. Set aside critical days and critical mass. Bring 15 people. 


Robin: Looking to transition into Python from MATLAB. Echo make an HTML website. There is a marketing aspect to this: Demonstrating the sort of things you can do with this. Panopto. MAke the case that it is worth the time and effort to invest to learn. Think about media: Webinars, video; as easy as possible for the overwhelmed and the lazy. 

Phil: Matt Rocklin has mastered the short screencast: Less than four minutes. Link below on the YouTube channel that sends you to his notebook. 

CESM has a forum... "Help I don't know what's going on..." (Elizabeth). Jupyter uses a platform called DISCOURSE. From Discourse to issues as needed. Safer place to have conversations. Breaks out of the power dynamic of GitHub: Devs and Plebes. 


Rob: Data publication

Ryan's white paper idea

$200k / PB / year. Phil brings up HPC versus cloud thing; demonstrating pangeo tech works rather than cloud works. Certain data has to be in house. AA: Similar for NASA HIMAT. Had we had pangeo. 

Ariel: Carpentries are a super-helpful entry point. But what about the day after the workshop. Using effectively after you are airborne. 

- RA: Living dynamic Jupyter book for { scientists, administrators }
- "I will never ask a question on GitHub" help desk problem
- Discussion questions
  - What is pangeo? ---> Who, what, how does pangeo teach? 
  - How should POET test pangeo?
  - Are pubs evidence of impact?...
    - ...how might this motivate POET focus today
  - Data canon
    - Comment on the value of "Get dataset X wired into pangeo" 
      - Will this motivate scientists who use X to migrate to pangeo? 
    - What is the set { X1, X2, X3, ... }? 
    - Process to select and import X? 
    - Should Pangeo Ed teach how to import some X?
- Repo is http://github.com/pangeo-data/education-materials
  - Currently in three parts... pedagogy { cloud, core, git, pod, virtualenv} , wg, README mapping
  - More repos?
- Enrollment: Who is in POET voluntarily? Involuntarily?
- What are target proposals?
  - Who can we work with? e.g. UW SoO/APL + OOI RCA is a good candidate
  - Past: NSF 19-524 
- Lindsey Heagy: Jupyter Community Workshop proposal
- Six month time frame: Milestones
- Designated PM or PMs
- Teaching itinerary
- Recording progress: Importance of, how to
- What’s missing here? How do you see improving organization? 
- Review related open GitHub issues ()
  - Issue #521 at pangeo-data/pangeo: Glacier model proposal by fmaussion: Follow-up?
  - Issue #440 at pangeo-data/pangeo: Resources for education events: We need an owner for this sub-topic (especially load testing)
  - Issues #411 and #575 require review with follow-up with contributors >> Game Plan
  
* Friday


## June 17-21 Icesat 2 Hackweek at UW

This event is included in pangeo-ed owing to the wealth of resources that were generated in support of the event.
We need to identify events and resources that become available from events of this sort to include them in the 

## June 4 2019 start call



### pending follow-on

- Review related open GitHub issues ()
  - Issue #521 at pangeo-data/pangeo: Glacier model proposal by fmaussion: Follow-up?
  - Issue #440 at pangeo-data/pangeo: Resources for education events: We need an owner for this sub-topic (especially load testing)
  - Issues #411 and #575 require review with follow-up with contributors >> Game Plan

#### [pangeo](http://pangeo.io) pillars

Pangeo is a coordination point between scientists, software, and computing infrastructure 
- Community building: Foster collaboration around open source scientific Python ecosystem for O/A/L/CS
- Domain tool-building: Support development of domain-specific geoscience packages
- Scale-tech building: Improve scalability of these tools, i.e. operate on large datasets

#### summary / directional material 

- Funding: What is pending? What are the opportunities?
  - Example (past): [NSF 19-524](https://www.nsf.gov/publications/pub_summ.jsp?WT.z_pims_id=505342&ods_key=nsf19524)
- "Thanks for the pod... by the way who pays for this?"
  - Schedule: Year 2 (NASA) starts in August; many other gears also turning
  - What are the different ways that pangeo education goes into practice? (list courses, hackweeks, etc)
- Meetings as applied to pangeo-ed
  - Joe report on France meeting?
 - August meeting is pending; we'll need a pangeo-ed agenda
  - What does community building look like? 
    - Bring in more scientists; so what is in it for them?
    - Bring in more developers; so what is in it for them?
    - How does publishing domain code create positive feedback?
- methods
  - "A cascade of education materials" (similar size, smaller quanta composable units)
    - modularized from a 20 minute talk to a 4 hour AGU tutorial to multi-day presence at hackweek 
  - Identify typical user's concerns (teach only what is necessary (best guess))
  - 5 or 6 virtual sprints per year, virtual working space
  - Need a ***testing protocol and testing schedule*** for content
    - Pedagogical issues: Expert blind spot, ***debugging***, time-to-proficiency estimation, what else?
  - Do-and-capture mantra
  - Existing content
    - Damien's OA s/w carpentry (Example review question: 'Does this include `dask`?')
    - Need a review/overhaul of the table presented on the 
[*education-material* repo main page](https://github.com/pangeo-data/education-material)
  - Z2JHub: Good exemplar project model for content
    - Z2Pangeo is nice but too general; suggesting Z2PangeoX where X is the focus
  - Synthesis and Wheel Non-Reinvention
    - Let's consider R-OpenSci and Pi-OpenSci: Peer review s/w publication
    - Z2Pangeo >> Z2JHub???
    - "Focus on building better documentation elsewhere" not just += the pangeo portfolio (tag!)
    - Align with NCAR's ongoing efforts, NCL transition, etc?




 
