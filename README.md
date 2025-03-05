# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
The goal of this project is to be able to analyze a large dataset that included five csv files that are generated from different sources and have a wide range of formats and consistency challenges. Additionally my objective was to learn how to use the tools that will enable analysis (connecting to and updating a repository on Github, importing csvs into PostgreSQL and creating tables, cleaning the information, and beginning to view it in a structured way to help glean insights that may be of use to an end user. 

## Process
**Step 1**- Import csv files into tables in PostgreSQL as text only fields with no keys or constraints. I've learned in a very slow fashion how important lowercase column names are when importing.  
**Step 2**- Look for keys that could be used to link tables and identify primary keys for each table.  
**Step 3**- Generate an ERD and read the questions to determine which table the information that I'd need would be located; in this case all_sessions.  
**Step 4** Given how important it is to not alter original data, I decided to create a cleaned view with only the columns that I actually needed information from that I could base my queries off of. I then determined the required data types for fields that would have functions performed on them and altered null fields or those with missing information to suit my needs.  
**Step 5**- Answered questions 1-5 using my cleaned view.  
**Step 6**- Created my own questions that I had as I viewed and engaged with the data.  
**Step 7**- Performed QA on my results to validate that my information was correct.

## Results
This data was able to tell me how a user got to a website (paid ad, direct typing into, organic search, or referral from another website), what they looked at, how long they look at it, where they were from, and what they purchased.

## Challenges 
One challenge is not knowing how the information was collected or where from. I can ascertain that it must be from webpage history, but I know little else. The result is making several assumptions, mainly that this source seems to focus on information from users in the United States and therefore is not very representative (unless it's for products manufactured in the US). I also don't really know what the end user is hoping to use this information for and had I the opportunity would ask some clarifying questions to the client about what they were hoping to use this information for.

## Future Goals
I focused my efforts on the all_sessions table and I did notice that sku was used in three other tables. I could use more time to join the tables by the primary/foreign keys and find other interesting trends. 
