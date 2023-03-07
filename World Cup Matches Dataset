--- Win percentage: the proportion of matches won by each team out of all matches played


SELECT 
  Teams,
  Total_Wins,
  Total_Matches,
  (Total_Wins/Total_Matches)*100 as Wins_Percentage
FROM
  (SELECT
     CASE WHEN Away_Team_Name = 'West Germany' THEN 'Germany' 
     ELSE Away_Team_Name END as Teams,
     SUM(Away_Team_Win) as Total_away_win,
     SUM(Home_Team_Win) as Total_home_win,
     SUM (Home_Team_Win) + SUM(Away_Team_Win) as Total_Wins,
     COUNT(Away_Team_Name)+ COUNT(Home_Team_Name) as Total_Matches
   FROM `noble-linker-375314.World_Cup.World_Cup_Matches`
   GROUP BY Teams)
WHERE Total_Matches> 50
   ORDER BY Wins_Percentage DESC
   
   
-----------------------------------------------------------------------------------------------------------------------------------------
--- World Cup Performance by Goals: the difference between the total number of goals scored and conceded by each team


SELECT 
 Teams,
 SUM(Goals) AS Total_Scored_Goals,
 SUM(Margin_Goals) as Total_Margin_Goals,
 SUM(Goals)- SUM(Margin_Goals) as Goals_Conceded
FROM
 (SELECT
     CASE WHEN Home_team_name = 'West Germany' THEN 'Germany'
         ELSE Home_Team_Name END AS Teams,
     Home_Team_Score as Goals, 
     Home_Team_Score_Margin as Margin_Goals
   FROM `noble-linker-375314.World_Cup.World_Cup_Matches`
   UNION All
   SELECT 
     Away_Team_Name as Teams, 
     Away_Team_Score as Goals, 
     Away_Team_Score_Margin as Margin_Goals
   FROM `noble-linker-375314.World_Cup.World_Cup_Matches`) as T1
GROUP BY Teams
ORDER BY Total_Margin_Goals DESC
LIMIT 10


-----------------------------------------------------------------------------------------------------------------------------------------
---Number of championships: the number of times each team has won the World Cup


SELECT
  CASE WHEN Home_team_name = 'West Germany' THEN 'Germany' 
    ELSE Home_Team_Name END as Teams, 
  SUM(Home_team_win) + SUM(Away_Team_Win) as Wins
FROM `noble-linker-375314.World_Cup.World_Cup_Matches`
WHERE Stage_Name = 'final'
GROUP BY Teams
ORDER BY Wins DESC
