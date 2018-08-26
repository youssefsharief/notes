## Dialog Flow
* Sequential Process
    1. User enters a sentence (a query)
    2. Dialogflow uses NLP to determine the best intent that matches the sentence
        * Questions
            * Is that based on the entities of each intent?
    3. Dialogflow selects one intent (the one with the highest socre or fallback intent if all intents got very low scores)
        * which has context attached to it
    4. Fullfillment (Optional) 
    5. Action which is attached to the intent is done
* How to start?
    * Look at prebuilt agents and add to them responses

### Agent
* is a natural language understanding module
* has 
    * a language
    * voice type
    * timezone
    * oAuthLinking (optional)
    * webhook (optional)
    * 
* is connected to a project
* How to have one?
    * Create custom agent
    * Import a prebuilt one from https://console.dialogflow.com/api-client/#/agent//prebuiltAgents/
  
### Context
* is a state
* an intent is triggered only if all its input contexts are set
* output context of an intent is a way for the intent to save state after it has been triggred
* Lifespan: 20 minutes or 5 requests or custome
* You could set the lifespan to 0 to rest the context
* They link intents together
* Naming convention:
    * 
### Intents
* Types
    * Normal Intent
    * Follow up intent
        * Occurs only when the parent intent has been activated
        * Gets access to the parent's parameter values
            * For example, If the name of the linking context is **MakeAppointment**-**followup** we could use parent's valuess like this
                * #MakeAppointment-followup.date
                * #MakeAppointment-followup.date
    * Fallback Intent
        * do not have training phrases
* Properties
    * priority
* represents a mapping between what a user says and what action should be taken by your software
* which which represent an intention
    * Example
        * "What is your name?", "Do you have a name?", or "name" have the same intention
* There are two default intents
    * Default Fallback Intent when it doesn't understand what your users say  -> Input.unknown
    * Default Welcome Intent greets your users -> Input.welcome
#### Traning phrases 
* for example
    * "What is your name?"
    * "Do you have a name?"
    * "name"

* Questions
    * How does the intent generalizes these questions?
        * How does the intent understand that "Please tell me my name" has the same intent? 
            * Answer
                * Dialogflow automatically checks the query which is "Please tell me my name" against all intents gives them a score. If the score is so low, the fallback intent is matched
* Dialog flow sometimes automatically captures **entites** from training phrases
* has context
    * which is the state of the intent
* induce an action
    * which have parameters
        * which are elements used to connect wprds in a user's response to entities in the agent
        * How to define them?
            * Automatically 
                * extracted from **training phrases**
            * Manually
                * You could assign words in the training phrase to parameters that connects to **pre existing entities**. 
                * For example 
                    * There is language called "Senawi". Dialogflow already has an entity called @sys.language that has some terms but the language "Senawi" is not included. So you could double click on the word "Senawi" and assign in the entity **@sys.language**
        * which have a value
            * Characteristics
                * constant
                    * example: right motor has a value of 500
                * default
                    * 
        * You could consider them the properties of the object made by the intent in the response for example
            * Example
                * Reserve a restaurant, we could have schema of dish array, location string, and rating number. Each one of those is a parameter that is linked to an entity. **is** **list** checkmark reperesents whether the parameter is a string or array
* Responses
    * You could have more than one text for a response 
        * Example
            * My name is Essam
            * Essam is my name
    * You could also have more than one reponse
        * Example
            1. My name is Essam
            2. What is yours
    * You could utilize variables like **language** 
### Entity
* could be considered a property
    * special type of property in which it is considered an extended enum since we have predefined entries for each entity
* Types
    * developer
    * system
    * user 
        * 
        * transient: expire after 10 minutes
* could be shared between different objects (intents)
    * Example
        * Both restaurant(intent) and cafe(intent) could have the **stars** property(entity)
* Features
    * Composite entity
        * Example
            * @bike-woth-color is a composite for @bike-type and @sys.color

* You could add non existing entites. For example "ProgarammingLanguage" entity is not there so you could add it
* Example
    * @rate
    * @date
    * @venue-type
    * @sys.language
    * @isOpen
* has entries
    * which has one or more synonym
        * Example
            * JavaScript, js, ECMAScript
    * Example
        * JavaScript
* Notes
    * Dialogflow can handle simple things like plurality and capitalization



Intent Options
* Match using rule  based + ML  or using only ML. Ml is preferred for larger training phrases
* 

### Webhook
When you activate the webhook, you could remove responses and make the bakend respond

### Naming Conventions
* Intent:
    * "UserProvidesEmailAddress", "UserProvidesZipCode"
    * OR "MakeAppointment"
* Context: "awaitingEmailAddress"

### How to make it smarter
* Use a prebuilt agent which is called "small talk" to complement your agent
    * Copy all intents among with related entities


#### Applications
1. Google Assistant
2. Chat bot

#### Learning Resources
* Aravind Mohanoor in YouTube
    * https://courses.miningbusinessdata.com/courses/take/dialogflow-conversation-design/lessons/3247621-introduction
    * not reliable
    * Suggestions
        * Always have context with span of 1
        * Do not make use of prompts to fill slots of a single intent instead 
        * 
* Pluralsight: Dialogflow
* lynda (no one found)
* Official Docs
* udemy
  
### Type of Dialogs
* Linear Dialogs
    * Single Intent Linear Dialog
        * You could have an action which is bookflight that needs several parameters like date, time, and location. If they are required, agent would keep askingtill all are fullfilled
    * Multiple intent Linear Dialogs
        * Use big intents for example for booking flights with all values needed and propmts for those values and ig you need the same values elsewhere like booking a room, you could use the context "#flight_context" for example. You could keep this context to have a lifespan for 8 for example. You need to add a defult value for the date parameter in bookcar to be "#flight_context.$date"
        * This is not what we want for booking a flight and a room since we might want to book a room without booking a flight
    * Follow Up Intents
        * Better way to book flights and book a car where you could book a car by 2 intents, the first is normal and the second is a followup intent of the booking a flight(which could use the "#flight_context"). This way you could book a car after booking a flight with a good UX since the system have default values from the flight context and at the same time you could book a car from scratch
* Non linear dialogs
    * Example 
        * Feedbacks for location and services
            * We could simple have an action and intent for "send feedback" that would have two parameters **locationFeedback** and **servicesFeedback** and mark both as **required** but in this case we could hardly show our sympathy with the user's emotions in case the feedback is bad. So what could we do?
            * We could have a specific intents called "UserProvidesGoodLocationFeedback" and "UserProvidesBadLocationFeedback" where we respond to the user by a sympathetic message 
  
### Deployment
* Firebase Functions
    * Need to upgrade tiyr firebase tier to Blaze
* Lambda
    * Why?
        * Cheaper
    * How?
        * Add lambda functin that is triggered by **ApiGateway** 
        * Uncheck Lambda proxy integration from the integration request in APIGateway

### Integration
* Slack
    * Go to api.slack.com/apps
    * Create an app
    * Click on bot user on the left navigation bar
    * Click on event subscription on the left navigation bar
    * Add bot user event
        * meesage.im
    * Take the ClientId and ClientSecret found in basic info
    * Go to Integrations
        * Select Slack and add client secret
        * You should find oauth url and event request url
    * Go to Slack and add redirect url for ouath 

### Advanced Questions
* How to recorrect an incorrect input
    * Fallback Intent
        * have the same input context as the original intent
        * no output context as the input context
            * Notice that having similar input and output context creates a loop if the input (zipCode) is incorrect and the **UserProvidesZipCode** is not triggred (fallback is triggred instead)
        * 
        * The issue with this approach is that the user could get stuck in the same loop in he inputted the zip code  incorrectly forever
            * We need to be able to reset the dialog
        * Naming
            * UserZipCodeIsIncorrect
    * Explicit intents
        * **UserProvidesZipCode** that have input context of **awaitingZip** and output context of **awaitingCity** (this get fired only if the response is correct since Dialogflow checks that the entity (zipCode) coming from the user is correct)
        * 
        * **UserZipCodeIsIncorrect** that have the same input context as **UserProvidesZipCode** but
        * **UserProvidesZipCode2** that have the same input context as **UserProvidesZipCode** but
        * **ZipCodeIsIncorrectSecondTime** that have the same input context as **UserProvidesZipCode** and as **UserProvidesZipCode2**
                                            * How to loop?
                                                * Example:
                                                    * I want to add 3 flowers, then respose what do you want to add again then respond with 3 roses, and keep asking for adding again, again, and again
* What does adding follow up fro the UI do under the hood?
    * It adds a context to the putput of the parent and adds the same context to the input of the child
    * 


### Other
* Suggestion Chip
* Link out suggestions


### Auth tokens
* Client token 
    * do not expose to client
* Developer Token does all the client token does plus (updating, editing, and deleting) intents

* Sample App
    * Rent bike
        * Check that start date is after end date
        * Return back if no bikes are available
        * 





            * Example
                * "Mohamed Abou Treika" could be added manually as a football player if it is not known to google


* Lambda Function Configuration
    * Create a new role thet uses **simple microservice** policy
    * When you test your lambda function 