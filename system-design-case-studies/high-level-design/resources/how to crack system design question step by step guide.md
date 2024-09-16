## [System design framework](https://www.youtube.com/watch?v=i7twT3x5yv8)
---
* understand the problem and establish design scope
	* clarify questions
		* who are the primary users of this system? are we supposed to design from admin perspective also or customer perspective only?
		* module: are we supposed to take care of food delivery system or restaurant / food search system?
		* how many users? how many DAU ?
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
* propose high level design and get buy in
	* define each APIs with request params and response required for functional requirement
	* propose a high level design 
	* not necessary to specify exact db technology at this stage
	* last step: define db model and schema
	* make a list of discussion points for later deep dive section
		* db scalability
		* latency / throughput
		* failure scenario
* design deep dive
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
## [How to crack system design interview](https://www.youtube.com/watch?v=o-k7h2G3Gco)
* practice, practice, practice in mock interview setup in excalidraw
* follow [[#[System design framework](https //www.youtube.com/watch?v=i7twT3x5yv8) | system design framework]]
* note down pros and cons of design decision
* manage your time properly