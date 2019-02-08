#Description of Housing System
This application implements an automated reservation system for Bellvue College's on campus resident housing. 


##Design:
All available housing units with descriptions are displayed when an applicant chooses the “Apply” option 
in the main menu. The applicant is prompted to enter 3 preferences + a roommate preference, and then sequentially 
enters username, password, and other personal information. Once everything is inputted, the applicant will get
the match automatically and it will be printed on the screen with the new assigned address. They can return to
the main screen and login as a resident. If no unit is available, they are added to to the waitlist with a 
dummy housing unit. At the time that a unit becomes available, Admissions admin will have to change the values 
and correctly assign the waitlisted applicant a housing unit (We did not implement this part of the project).

Additional functionality includes displaying a maintenance request report for that day. Upon selecting "Admin", followed by "Administrative Reports" and "Maintenance Department Reports", all pending maintenance requests are displayed, with information about the resident and a short description of the problem.

##Assumptions made in EER:
1.	Residents and Waitlisted applicants are two types of users in our housing system. They cannot be both types simultaneously (hence are represented as disjoint), and there are no other types of users (hence complete relationship). A user can also be the family head of other users (hence self-relational).
2.	There are three types of admin: maintenance, residence, and admissions admin. We make the assumption that there are no other types of admin in our model (hence complete relationship). Admin can hold multiple roles though (hence overlapping). They can handle many maintenance requests, many residents, and many waitlisted applications respectively. 
3.	An applicant can have many housing preferences, hence it is a multivalued attribute.
4.	Many residents can live in AT MOST one housing unit. The housing unit has an attribute type, which is either apartment or suite. The attributes, # of bedrooms and max people, indicate which type of apartment or suite it is.  Another attribute called “occupied/not occupied” allows the housing system to know which units are available to lease. A 1 indicates that the housing unit is fully occupied, a 0 indicates that there is still some vacancies in the unit. 
5.	A maintenance request can be filed by AT MOST one person. 
6.	A maintenance request, application, resident can be handled by EXACTLY one admin.
7.	After submitting an Application and getting approved by the College, the students has to confirm their approval. If there are no available units, or the applicant does not confirm their housing unit, they are added to the Waitlist table. 
 
##Design choices in Relational schema:
1.	Multivalued attributes, housing_preference has its own table since it is multivalued. 
2.	Since admin types are overlapping, maintenance admin, resident admin, and admissions admin are represented with boolean flags in the admin table. 
 
##Additional assumptions:
1.	All data is stored and kept for a period of time greater than five years, so it can be accessed later for demographic purposes. 
2.	Roommate preferences ONLY matched if roommate already exists in the system. 
3.	We are only going to book people based on preferences. 
4.	In table “Maintenace_request”, the status column only accepts value “pending” or “completed”. All requests entered should have value “pending” and as soon as a request is dealt with, the administrator will change the status value from “pending” to “completed”.

