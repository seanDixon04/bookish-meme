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

[Data Model Updated 2.pdf](https://github.com/msw05090/bookish-meme/files/14877126/Data.Model.Updated.2.pdf)

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

# Queries 

[Project Queries.pdf](https://github.com/msw05090/bookish-meme/files/14877147/Project.Queries.pdf)

Simple

Write a query to list the full names and playerID of all forwards who are from Belgium
SELECT fullName, playerID, nationality, position
FROM Players
Where nationality REGEXP 'Belgian' AND position REGEXP 'Forward';
This query would be useful to identify players who play a certain position from a certain country, in this case, Belgian players who play Forward.


Write a query to list all community events that are expected to have at least 400 attendees
SELECT eventName, location, attendenceNumbers
FROM CommunityEvents
WHERE attendenceNumbers >= 400;
This query would be helpful for planning out food vendors, entertainment, and other additions the venues during games. Larger events may require more options to account for all of the fans.

**Write a query to list every match that had a total of one goal scored by both teams and also took place in Athens Soccer stadium**

SELECT goalsScored, venue, matchID
FROM Matches
WHERE goalsScored=1;
Lots of matches take place in each stadium and some are more entertaining than others, and goals being scored directly impacts how entertaining the games are. This query identifies the games that were considered less exciting.

Write a query to list the names of all Youth players from the U 14 academy team and have birthdays in first half of the year
SELECT FullName, youthPlayerID
FROM YouthPlayer
WHERE AcademyTeam = 'Under-14s' AND MONTH(DateOfBirth) <= 6;
Youth teams are more likely to have get-togethers and parties for birthdays and the season ends around the middle of the year. This query lists the players who will have a birthday during the season so that plans to celebrate can be made.

Complex

Write a query to list the amount of French players who were injured in the months of May, June, or July

SELECT COUNT(DISTINCT p.PlayerID) AS French_Players_Injured_In_May
FROM Players p
JOIN Injuries i ON p.PlayerID = i.PlayerID
WHERE p.Nationality = 'French' AND MONTH(i.DateOfInjury) REGEXP '5|6|7';
If the French player was struggling during the months of May, June, and July, this query allows us to look deeper into why that may be. If they were missing key components on the pitch, it could be the reason why the team was underperforming.

Write a query to list the names of players who have recovered from injuries, with their dates in descending order.

SELECT fullName, medicalRecords, dateOfInjury, status
FROM Players p
JOIN Injuries i ON p.playerID=i.playerID
WHERE status REGEXP 'Recovered'
ORDER BY dateOfInjury DESC;
Managers of the team may need to schedule follow up appointments with doctors or physical therapists for players after they have been injured. This query would identify the recency of injuries so that necessary appointments can be scheduled.

Write an SQL query to retrieve the nationality of players along with the count of injured players for each nationality, but only include nationalities where the count of injured players is greater than one

SELECT p.Nationality, COUNT(*) AS NumberOfInjuredPlayers
FROM Players p
JOIN Injuries i ON p.PlayerID = i.PlayerID
GROUP BY p.Nationality
HAVING COUNT(*)>1;
Certain teams may require more attention if they have more players on the IR (injury report). This query identifies the players that are most in need of aid.

Write a query retrieve the  name of all brazilian players scouted, their strengths, and the full name of the coach involved in scouting

SELECT p.fullName, strengths, nationality, c.fullname
FROM ScoutingReports sr
JOIN Players p ON sr.playerID=p.playerID
JOIN CoachingStaff c ON p.coachID=c.staffID
WHERE nationality = 'Brazilian';
This query singles out a nationality, Brazilian in this case, and views their strengths. It allows coaches and scouts to recruit new talent and also shows which coach took notes on the player because certain coaches may value different attributes on the pitch.

Write a query should select the company name of each sponsor and the total number of transactions they've conducted, only if their transaction was greater than or equal to 100,000

SELECT s.CompanyName, SUM(ft.Amount) AS TotalAmountSpent, COUNT(ft.TransactionID) AS TotalTransactions
FROM Sponsors s
JOIN FinancialTransactions ft ON s.CompanyName = ft.RelatedEntity
GROUP BY s.SponsorID, s.CompanyName
HAVING TotalAmountSpent >= 100000;
This query is useful for finding the most valuable sponsors. It selects the name, how often they have sponsored events, and the amount too, lots of relevant information for choosing future sponsors.

Write a code to list the names of coaches, the amount of players they oversee, and the average age of those players.

SELECT c.FullName AS CoachName, COUNT(yp.YouthPlayerID) AS TotalYouthPlayers, AVG(YEAR(CURRENT_DATE) - YEAR(yp.DateOfBirth)) AS AverageAge
FROM CoachingStaff c
JOIN YouthPlayer yp ON c.staffID = yp.staffID
GROUP BY c.StaffID, c.FullName;
This query is good for analyzing coaches and potentially adding/removing players from youth rosters. If there are new players, this data would be used to find where to place them based on what teams need players. Also, fitting a new player in with other players of the same age.

