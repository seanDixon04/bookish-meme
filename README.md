# Team 7 Group Project 1
[Sean Dixon]https://github.com/seanDixon04/expert-train.git 

[Manny Walia]https://github.com/msw05090/bookish-meme

[Daniella Raj]https://github.com/daniellaraj/didactic-computing-machine.git

[Jacob Gates]https://github.com/jgates01/fantastic-octo-umbrella

# Problem Description
Prompt:  Pretend you are the owner/operator of a tennis (or football, soccer - your choice) club needing to build a relational database. You hired some students from the MIST 4610 class at the University of Georgia to create the database for you. They need to know more about your organization to identify which entities, attributes, and relationships are important for you. Start by describing your business as a real client.

# Data Model
Our model has a diverse membership base consisting of individuals of all ages, skill levels, and backgrounds. Our club hosts regular tournaments for recreational and competitive matches. Additionally, we offer coaching programs led by certified instructors to help our members improve their skills and reach their full potential on the court.
In terms of operations, we manage court reservations, membership registrations, coaching schedules, tournament logistics, and facility maintenance. We rely on efficient organization and communication to ensure smooth functioning and deliver a positive experience for our members.

# Connecting The Data Model

How these all connect:

Players and Matches:
Each match involves a lineup of players.
Connect via a many-to-many relationship table called "MatchLineup":
MatchID (Foreign Key referencing Matches)
PlayerID (Foreign Key referencing Players)

Players and Coaching Staff:
Players are coached by members of the coaching staff.
Connect via a foreign key in the Players table:
CoachID (Foreign Key referencing Coaching Staff)

Matches and Facilities:
Each match is played at a specific facility.
Connect via a foreign key in the Matches table:
FacilityID (Foreign Key referencing Facilities)

Financial Transactions and Related Entities:
Financial transactions involve various entities like players, staff, facilities, and sponsors.
Connect via foreign keys depending on the related entity:
PlayerID (Foreign Key referencing Players)
StaffID (Foreign Key referencing Coaching Staff)
FacilityID (Foreign Key referencing Facilities)
SponsorID (Foreign Key referencing Sponsors)

Sponsors and Marketing Campaigns:
Sponsors may be associated with specific marketing campaigns.
Connect via a many-to-many relationship table:
SponsorCampaign:
SponsorID (Foreign Key referencing Sponsors)
CampaignID (Foreign Key referencing Marketing Campaigns)

Fans and Matches:
Fans attend matches.
Connect via a many-to-many relationship table:
FanMatchAttendance:
FanID (Foreign Key referencing Fans)
MatchID (Foreign Key referencing Matches)

Youth Players and Coaching Staff:
Youth players are coached by members of the coaching staff.
Connect via a foreign key in the Youth Players table:
CoachID (Foreign Key referencing Coaching Staff)

Marketing Campaigns and Community Events:
Marketing campaigns may promote or be associated with community events.
Connect via a many-to-many relationship table:
CampaignEvent:
CampaignID (Foreign Key referencing Marketing Campaigns)
EventID (Foreign Key referencing Community Events)

Injuries and Players:
Each injury is associated with a specific player.
Connect via a foreign key in the Injuries table:
PlayerID (Foreign Key referencing Players)

Scouting Reports and Players:
Each scouting report pertains to a particular player.
Connect via a foreign key in the Scouting Reports table:
PlayerID (Foreign Key referencing Players)
