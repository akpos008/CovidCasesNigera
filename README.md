# CovidCasesNigera

  ---total amount OF cases IN Nigeria

SELECT
  SUM(total_population)AS total_population,
  SUM(total_confirmed) AS total_confirmed_cases,
  SUM(total_deaths) AS total_deaths,
  SUM(total_recoveries) AS recovered_total,
 (
      SELECT 
 (total_deaths/total_population) * 100 AS total_death_population
    FROM  covid_19_nigeria.covid_deaths
    LIMIT  1
  ) AS percentage_total_death
FROM
  covid_19_nigeria.covid_deaths 




  --state with the highest number OF covid cases
  
  SELECT states, 
  MAX(total_confirmed) AS maximum_confimed_cases
  FROM covid_19_nigeria.covid_deaths
  GROUP BY states
  HAVING max(total_confirmed) > 50000
  ORDER BY 1 



---state with lowest number of covid cases

SELECT states, 
  MIN(total_confirmed) AS minimum_confimed_cases
FROM covid_19_nigeria.covid_deaths
  GROUP BY states
  HAVING MIN(total_confirmed) < 10



---percentage of death from each state

SELECT states,total_confirmed, total_deaths,(total_deaths/total_confirmed) * 100  AS percentage_death
FROM covid_19_nigeria.covid_deaths
ORDER BY total_deaths DESC 



---state with the highest death to the lowest death from covid

SELECT states,
        MAX(total_deaths) AS maximum_deaths, 
FROM covid_19_nigeria.covid_deaths
GROUP BY states
ORDER BY maximum_deaths DESC 






