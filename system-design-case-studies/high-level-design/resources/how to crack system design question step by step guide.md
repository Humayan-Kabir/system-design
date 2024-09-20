## [System design framework](https://www.youtube.com/watch?v=i7twT3x5yv8)
---
* **understand the problem and establish design scope**
	* clarify questions
		*  Who is going to use it? are we supposed to design from admin perspective also or customer perspective only?
		* What specific features are we going to build?
			* ask features related questions after getting list.
		* What is the scale of the system? Is it built for a startup or a big company with a large user base?
		 - Will the system work in a distributed environment
		- What are the inputs and outputs of the system?
		* how many users? how many DAU ?
		* How fast does the company anticipate to scale up? What are the anticipated scales in 3 months, 6 months, and a year?
		- What is the company’s technology stack? What existing services you might leverage to simplify the design?
		- How much data do we expect to handle?
		- How many requests per second do we expect?
		- What is the expected read to write ratio?
		- module: are we supposed to take care of food delivery system or restaurant / food search system?
		* is our system going to be used only in Bangkok or globally?
		* availability or consistency?
	* function requirement
		* list down all functional requirements
		* make an agreement with interviewer regarding which features should be focused
	* non functional requirement
		* scalability
		* performance
		* consistency 
		* availability
		* reliability
		* security
	* back of the envelop estimation
* **propose high level design and get buy in**
	* define each APIs with request params and response required for functional requirement
	* propose a high level design 
	* not necessary to specify exact db technology at this stage
	* last step: define db model and schema
	* make a list of discussion points for later deep dive section
		* db scalability
		* latency / throughput
		* failure scenario
* **design deep dive**
	* discuss areas that could be potentially problematic
	* propose different solutions with pros / cons
	* focus on non functional 
	* topics
		* single point of failure 
			* replication 
		* scaling
			* sharding 
			* multi geo cluster
			* distributed caching / consistency / logger / scheduler
		* hot user / fanout service
	* this is open ended section so discuss with interviewer more
* **wrap-up**
	* recap whole design
	* error case / edge case
	* log, metric
	* what to handle the next scale
	* other refinement you could share if you have time
## [How to crack system design interview](https://www.youtube.com/watch?v=o-k7h2G3Gco)
* practice, practice, practice in mock interview setup in excalidraw
* follow [[#[System design framework](https //www.youtube.com/watch?v=i7twT3x5yv8) | system design framework]]
* note down pros and cons of design decision
* manage your time properly