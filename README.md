# MIST4610-Project-1

# project_1_4610

## Group Members - Group 4
- [Tobias Allers](https://github.com/tka29934)
- [Luke Mabry](https://github.com/Luke111033)
- [Alicia Lim](https://github.com/alicianlim)
- [Chris Sierra](https://github.com/Chrissi3rraa)
- [Pranav Rohit](https://github.com/pra984-star)

## Project Scenario and Overview
We were given the task of creating a new, high level for the NBA. They wanted database that could give an overview of their franchise. We built the data model with Teams being the central entity, and most other entities, such as executives on the team board, brand sponsorships, and coaches and players stemming from this primary entity. We were charged with building a data model to visualize the database, populate the database with data relevant to the NBA, and write queries to prove the efficacy of the database built.

## Data Model
<img width="568" alt="MIST 4610 Project 1 Data Model" src="https://github.com/user-attachments/assets/39af895d-bcab-4eb2-b48f-310f4b6cb46b" />

## Relationships Between Tables:

## We built a model that depicts different elements that would be stored by the NBA. We selected to make entities of Seasons, Executives, Games, Venues, Cities, Teams, Coaches, Brand Deals, Sponsors, Players, and Coach Player Pairings. Coaches and Players have a many to many relationship, as many coaches can coach a player and a player can have many coaches, explaining the associative entity of Coach Player Pairings to store the foreign keys between these two. The Coaches entity also has a 1-many relationship with teams, as a single team has many coaches but a coach can only be hired by one team at a time. Players also have a 1-many relationship with Teams for the same reason: a team has many players but a player can only play for one team at a time. Players has a 1-many relationship with Brand Deals, which acts as an associative entity between players and Sponsors as well as Teams and sponsors. This is because both teams and players can have many Brand Deals with Sponsors, and Sponsors can have deals with many Teams and many Players. The player and team IDs can be null in this entity, as a deal could be made using only a player, or only a team. Executives and Teams have a 1-many relationship because Executives work for 1 team but a team can have many executives. Teams have a 1-many relationship with Seasons, as a Team can win many seasons, but a season can only have 1 team be the winner (which is our foreign key). Seasons and Games share a 1-many relationship because Games can only be in 1 season but a Season has many games. Teams and games share two 1-many relationships to partition two foreign keys. These foreign keys are named teamWinner and teamLoser, because each game only has one winner and one loser (demonstrating the 1 sides of the two 1-many relationships), but the many sides of the relationship represent that a single team can be a winner or a loser many times. Teams has a 1-many relationship with Cities, because 1 team can only have (play for) 1 city however a City can have multiple teams (ie: Los Angeles). Cities and Venues have a 1-many relationship for the same reason: 1 city can have multiple venues, but a venue is only located within 1 particular city. And the last relationship is a 1-many between Venues and Games. This is because 1 venue can host many games, but a game can only be located at 1 venue. 


## Data Dictionary

<img width="636" alt="Screenshot 2025-03-20 at 12 26 50 PM" src="https://github.com/user-attachments/assets/7037747a-78c2-421f-bd51-28987c4ee8fc" />
<img width="632" alt="Screenshot 2025-03-20 at 12 27 05 PM" src="https://github.com/user-attachments/assets/a2487ea8-c71c-4ebb-b5c8-3aa06e1d1210" />
<img width="633" alt="Screenshot 2025-03-20 at 12 27 44 PM" src="https://github.com/user-attachments/assets/17260096-fb32-47c7-bec5-7dcf4f75a41f" />
<img width="633" alt="Screenshot 2025-03-20 at 12 28 12 PM" src="https://github.com/user-attachments/assets/f1756d02-dae2-4330-ac15-38f9b2484580" />
<img width="635" alt="Screenshot 2025-03-20 at 12 28 42 PM" src="https://github.com/user-attachments/assets/95d6a982-134b-4b09-83d5-8b224b815d92" />
<img width="635" alt="Screenshot 2025-03-20 at 12 29 23 PM" src="https://github.com/user-attachments/assets/6ef7c94e-139b-4525-99e7-e1349ed9de0f" />
<img width="638" alt="Screenshot 2025-03-20 at 12 30 15 PM" src="https://github.com/user-attachments/assets/8996f146-a84f-4cab-a720-59807d18bc7a" />
<img width="639" alt="Screenshot 2025-03-20 at 12 30 35 PM" src="https://github.com/user-attachments/assets/dbb9f77f-457c-4b67-bf69-48c36ac2625e" />
<img width="633" alt="Screenshot 2025-03-20 at 12 30 56 PM" src="https://github.com/user-attachments/assets/1420e97e-dccd-4fae-a9f1-49e8794f5c81" />
<img width="640" alt="Screenshot 2025-03-20 at 12 31 19 PM" src="https://github.com/user-attachments/assets/609545fc-320b-4416-b6ec-871e9850ed35" />
<img width="634" alt="Screenshot 2025-03-20 at 12 31 41 PM" src="https://github.com/user-attachments/assets/741881e7-66f6-4702-bfdc-ea26e5016dd5" />

## Queries

## Query 1 and Description

SELECT s.seasonYear, s.seasonWinner
FROM Seasons s
WHERE EXISTS (
    SELECT 1
    FROM Teams t
    WHERE t.teamName = s.seasonWinner
    AND t.dateFormed < '1980-01-01'
    AND t.numFans < 10000000);

## Description: Gives Team Name and seasonYear of teams who are seasonWinners and were formed before 1980 and also have less than 10000000 fans. (Shows significant smaller market teams who have been good recently, could be used to bump up league revenue distributed to these teams due to tenure in league and success level).

## Query 2 and Description

SELECT e.execID, e.firstName, e.lastName
FROM Executives e
WHERE EXISTS (
    SELECT 1
    FROM Teams t
    JOIN Cities c ON t.homeCity = c.cityID
    WHERE e.teamWorkedFor = t.teamName
    AND c.population > 800000  -- Try lowering the threshold);

## Description: Displays execID, firstName, and lastName of Executives that work for teams which are located in cities with a population of 800,000 or more. The reason for this query is because if you are a player’s agent (person who tries to find a player a contract on a team) and are trying to find a large market team for your player to play for, you would want to contact one of these executives. 

## Query 3 and Description
 
Select specialty, Coaches.firstName, Coaches.lastName, Coaches.teamSigned
From Coaches
Where specialty On (
Select specialty From Coaches Group By specialty Having Count(*)>1)
Order By specialty, Coaches.lastName;

## Description: This query identifies the coaches that have similar specialties and what team they coach for. This is important for executives choosing a specific coach that they believe will be beneficial to the team and to be a better fit for a manager. From a ownership perspective, understanding which position the coach is in, and how successful their team has been under their tenure in their specialty will help to narrow down the options for a new coach for that specialty. 


## Query 4 and Description

 Select Teams.teamName, Players.firstName, Players.lastName, Players.yearsPlayed
 From Teams
 Join Players ON Teams.teamName=Players.teamSigned
 Where Teams.teamName  (
	Select teamSigned From Players Group By teamSigned Having Avg(yearsPlayed)>5)
    Order By Players.yearsPlayed DESC;

## Description: This helps to narrow down the experience of players by filtering through the amount of years played and ordering the number of players who have played over 5 years. This helps Executives to select a player that has some more experience and give them a shot of winning a championship with that team. 



## Query 5 and Description

USE al_cas20361;
SELECT Teams.teamName, Teams.numFans, 
    AVG(Games.ticketsSold) AS avgTicketsSold, 
    (AVG(Games.ticketsSold) / Teams.numFans) * 100 AS fanEngagementRate,
    (SELECT COUNT(*) 
     FROM Games 
     WHERE Games.teamWinner = Teams.teamName OR Games.teamLoser = Teams.teamName
    ) AS totalGamesPlayed
FROM Teams
JOIN Games ON Teams.teamName = Games.teamWinner OR Teams.teamName = Games.teamLoser
WHERE Teams.numFans > 0  
GROUP BY Teams.teamName, Teams.numFans
HAVING fanEngagementRate < 0.5
ORDER BY fanEngagementRate ASC;

## Description: This query identifies teams with low fan engagement by comparing the average number of tickets sold per game to their total fan base. It helps executives understand which teams struggle to convert their fan base into actual attendees. 



## Query 6 and Description

USE al_cas20361;
SELECT Sponsors.companyName,Sponsors.netWorth,COUNT(`Brand Deals`.teamName) AS totalDeals
FROM Sponsors
JOIN `BrandDeals` ON Sponsors.companyID = `Brand Deals`.companyID
WHERE Sponsors.companyID IN (
    SELECT companyID
    FROM `Brand Deals`
    GROUP BY companyID
    HAVING COUNT(teamName) > (
        SELECT AVG(dealCount)
        FROM (SELECT companyID, COUNT(teamName) AS dealCount FROM `Brand Deals` GROUP BY companyID) AS avgDeals
    )
)
GROUP BY Sponsors.companyName, Sponsors.netWorth
ORDER BY totalDeals DESC;

## Description: This query identifies the top sponsors based on the number of brand deals they have with teams. It filters out sponsors that have fewer than the average number of deals, ensuring the focus is on high-value sponsors. The subquery calculates the average number of deals per sponsor and excludes those below this threshold, allowing for a more meaningful analysis of sponsorship impact.



## Query 7 and Description

SELECT teamName, numFans
FROM Teams
WHERE numFans > 5000000;

## Description: This query identifies teams with a large fan base, which is useful for understanding market size and fan engagement potential. Managers can use this data for strategic decisions, such as expanding merchandise distribution, planning fan engagement events, and negotiating sponsorship deals. Managers would care about this query because teams with larger fan bases represent greater revenue opportunities through merchandise, ticket sales, and sponsorships. Identifying these teams allows for targeted marketing and resource allocation.

## Query 8 and Description

SELECT c.cityName, SUM(v.capacity) AS total_capacity, COUNT(v.venueID) AS venue_count FROM 
Cities c
JOIN Venues v ON c.cityID = v.cityID
GROUP BY c.cityName
HAVING COUNT(v.venueID) > 1 AND SUM(v.capacity) > 40000;

## Description: This query identifies cities that host multiple venues with a large total seating capacity. This information is important for venue management and city planning, helping managers decide where to host large events or allocate resources to improve infrastructure. From a managerial perspective, understanding which cities have large total seating capacities across multiple venues helps in event scheduling, resource allocation, and market analysis. It can also support negotiations with event organizers and sponsors.

## Query 9 and Description


## Query 10 and Description
