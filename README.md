# MIST4610-Project-1
# project_1_4610

## Group Members - Group 4
- [Tobias Allers](https://github.com/tka29934/project_1_4610)
- [Luke Mabry](https://github.com/Luke111033/MIST4610-Project-1/blob/main/README.md)
- [Alicia Lim](https://github.com/alicianlim/Project-1-4610)
- [Chris Sierra](https://github.com/Chrissi3rraa/4610-Project-1/blob/main/README.md)
- [Pranav Rohit](https://github.com/pra984-star/GroupProject)

## Project Scenario and Overview
We were given the task of creating a new, high level database for the NBA. They wanted database that could give an overview of their franchise. We built the data model with Teams being the central entity, and most other entities, such as executives on the team board, brand sponsorships, and coaches and players stemming from this primary entity. We were charged with building a data model to visualize the database, populate the database with data relevant to the NBA, and write queries to prove the efficacy of the database built.

## Data Model
<img width="568" alt="MIST 4610 Project 1 Data Model" src="https://github.com/user-attachments/assets/39af895d-bcab-4eb2-b48f-310f4b6cb46b" />

We built a model that depicts different elements that would be stored by the NBA. We selected to make entities of Seasons, Executives, Games, Venues, Cities, Teams, Coaches, Brand Deals, Sponsors, Players, and Coach Player Pairings. Coaches and Players have a many to many relationship, as many coaches can coach a player and a player can have many coaches, explaining the associative entity of Coach Player Pairings to store the foreign keys between these two. The Coaches entity also has a 1-many relationship with teams, as a single team has many coaches but a coach can only be hired by one team at a time. Players also have a 1-many relationship with Teams for the same reason: a team has many players but a player can only play for one team at a time. Players has a 1-many relationship with Brand Deals, which acts as an associative entity between players and Sponsors as well as Teams and sponsors. This is because both teams and players can have many Brand Deals with Sponsors, and Sponsors can have deals with many Teams and many Players. The player and team IDs can be null in this entity, as a deal could be made using only a player, or only a team. Executives and Teams have a 1-many relationship because Executives work for 1 team but a team can have many executives. Teams have a 1-many relationship with Seasons, as a Team can win many seasons, but a season can only have 1 team be the winner (which is our foreign key). Seasons and Games share a 1-many relationship because Games can only be in 1 season but a Season has many games. Teams and games share two 1-many relationships to partition two foreign keys. These foreign keys are named teamWinner and teamLoser, because each game only has one winner and one loser (demonstrating the 1 sides of the two 1-many relationships), but the many sides of the relationship represent that a single team can be a winner or a loser many times. Teams has a 1-many relationship with Cities, because 1 team can only have (play for) 1 city however a City can have multiple teams (ie: Los Angeles). Cities and Venues have a 1-many relationship for the same reason: 1 city can have multiple venues, but a venue is only located within 1 particular city. And the last relationship is a 1-many between Venues and Games. This is because 1 venue can host many games, but a game can only be located at 1 venue. 


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

## Query Matrix
<img width="684" alt="Screenshot 2025-03-20 at 9 46 04 PM" src="https://github.com/user-attachments/assets/a144bfbf-a663-4649-bf3c-0e7afd12cf86" />


## Query 1

<img width="323" alt="Screenshot 2025-03-20 at 6 57 33 PM" src="https://github.com/user-attachments/assets/5b32b781-fb5f-43d1-93bc-c6f9466b553b" />
<img width="192" alt="Screenshot 2025-03-20 at 6 58 04 PM" src="https://github.com/user-attachments/assets/0d027154-9fe9-409a-8820-d7ba8eb1cd41" />

Gives Team Name and seasonYear of teams who are seasonWinners and were formed before 1980 and also have less than 10000000 fans. (Shows significant smaller market teams who have been good recently, could be used to bump up league revenue distributed to these teams due to tenure in league and success level).

## Query 2

<img width="357" alt="Screenshot 2025-03-20 at 6 55 23 PM" src="https://github.com/user-attachments/assets/b8e4fbc3-8dc1-40fa-80eb-a473e9b09cdd" />
<img width="187" alt="Screenshot 2025-03-20 at 6 55 40 PM" src="https://github.com/user-attachments/assets/cd560968-77b8-4f4d-844c-b4028b638851" />

Displays execID, firstName, and lastName of Executives that work for teams which are located in cities with a population of 800,000 or more. The reason for this query is because if you are a player’s agent (person who tries to find a player a contract on a team) and are trying to find a large market team for your player to play for, you would want to contact one of these executives. 

## Query 3
 
<img width="689" alt="Screenshot 2025-03-20 at 6 52 28 PM" src="https://github.com/user-attachments/assets/bf49a0ee-9a7f-4e7f-aff7-71895939bac1" />
<img width="462" alt="Screenshot 2025-03-20 at 6 52 53 PM" src="https://github.com/user-attachments/assets/62821cd5-82c6-4251-b19e-1c876cf08a30" />

This query identifies the coaches that have similar specialties and what team they coach for. This is important for executives choosing a specific coach that they believe will be beneficial to the team and to be a better fit for a manager. From a ownership perspective, understanding which position the coach is in, and how successful their team has been under their tenure in their specialty will help to narrow down the options for a new coach for that specialty. 


## Query 4

<img width="817" alt="Screenshot 2025-03-20 at 7 29 04 PM" src="https://github.com/user-attachments/assets/d2eab963-dade-4686-b8d9-3c92d01cd054" />
<img width="404" alt="Screenshot 2025-03-20 at 7 29 30 PM" src="https://github.com/user-attachments/assets/2466e92f-4f64-4545-bf30-00de3a029fb3" />

This helps to narrow down the experience of players by filtering through the amount of years played and ordering the number of players who have played over 5 years. This helps Executives to select a player that has some more experience and give them a shot of winning a championship with that team. 



## Query 5

<img width="687" alt="Screenshot 2025-03-20 at 6 48 01 PM" src="https://github.com/user-attachments/assets/b941ed95-9ea6-4e38-b5c6-665635b6e459" />
<img width="536" alt="Screenshot 2025-03-20 at 6 48 23 PM" src="https://github.com/user-attachments/assets/ec064ff7-65f7-40b8-a52b-cce6982f260b" />

This query identifies teams with low fan engagement by comparing the average number of tickets sold per game to their total fan base. It helps executives understand which teams struggle to convert their fan base into actual attendees. 



## Query 6

<img width="904" alt="Screenshot 2025-03-20 at 6 44 49 PM" src="https://github.com/user-attachments/assets/53df871c-f3e7-41d2-8668-3e4cbeed587d" />
<img width="218" alt="Screenshot 2025-03-20 at 6 45 17 PM" src="https://github.com/user-attachments/assets/70a3a812-f7bd-4761-b0e1-cc11c32fca78" />

This query identifies the top sponsors based on the number of brand deals they have with teams. It filters out sponsors that have fewer than the average number of deals, ensuring the focus is on high-value sponsors. The subquery calculates the average number of deals per sponsor and excludes those below this threshold, allowing for a more meaningful analysis of sponsorship impact.



## Query 7

<img width="208" alt="Screenshot 2025-03-20 at 6 42 49 PM" src="https://github.com/user-attachments/assets/24cfbe35-a1ed-4167-85e6-e202bd6c6a81" />
<img width="193" alt="Screenshot 2025-03-20 at 6 43 02 PM" src="https://github.com/user-attachments/assets/63b49527-04ef-4fd6-9de5-f1ce1d34b83e" />

This query identifies teams with a large fan base, which is useful for understanding market size and fan engagement potential. Managers can use this data for strategic decisions, such as expanding merchandise distribution, planning fan engagement events, and negotiating sponsorship deals. Managers would care about this query because teams with larger fan bases represent greater revenue opportunities through merchandise, ticket sales, and sponsorships. Identifying these teams allows for targeted marketing and resource allocation.

## Query 8

<img width="415" alt="Screenshot 2025-03-20 at 9 28 42 PM" src="https://github.com/user-attachments/assets/afceb693-98c7-42df-af0a-20ecd89d0aad" />
<img width="275" alt="Screenshot 2025-03-20 at 9 29 00 PM" src="https://github.com/user-attachments/assets/373cc3b9-4e7e-445a-b285-0c0dcaf5e215" />

The goal of this query is to show which venues have an above average capacity, as well as what state they're located in. It orders the venues by capacity from greatest to smallest. This is helpful for managers to know as it gives them an understanding of what the upper quanities of capacity look like; If these stadiums are routinely selling to max capacity executives could use this information to properly size any new stadiums. In addition, if there were any random national events to be hosted they could choose a locale with a higher capacity from this list.

## Query 9

<img width="521" alt="Screenshot 2025-03-20 at 6 41 17 PM" src="https://github.com/user-attachments/assets/427ecc27-b2a7-4957-b4f0-f5070baec5fa" />
<img width="218" alt="Screenshot 2025-03-20 at 6 41 40 PM" src="https://github.com/user-attachments/assets/8afb2719-3644-45f9-9f8d-669d4285db74" />

the goal of this query is to find and return games that did not sell out their venue. It gives the ratio of tickets sold to the total capacity of the venue the game was held in, as well as the year the game took place in. Executives would appreciate this data as it shows how frequently (or infrequently) games are able to sell to full capacity, as well as how close each game got to a fully packed arena. An interesting thing to take note of for the data is the fact that the games in 2020 return a "0 percent filled" cell; that is because, over Covid, real tickets were not sold for NBA games. Instead, virtual, free "tickets" were allowed for people to watch the game.

## Query 10

<img width="581" alt="Screenshot 2025-03-20 at 6 39 27 PM" src="https://github.com/user-attachments/assets/f42a27f6-a337-4da6-a9be-e83c51ae0ac3" />
<img width="444" alt="Screenshot 2025-03-20 at 6 39 57 PM" src="https://github.com/user-attachments/assets/94979c7f-2b87-49e6-997e-9490c19cda6e" />

This query shows the name and specialty of coaches, as well as the number of players under their training and the team they both belong to. This data is important from a managerial perspective as it helps for booking: If one coach has been assigned a lot of players it may be smart to move new players to another coach to avoid overwhelming any one coach. In addition, executives can see who the most popular coaches are.



