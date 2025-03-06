# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
The primary goal of this project is to develop proficiency in data analysis by working with data from five different CSV files. These files have significant inconsistencies, missing data, and formatting challenges. The project focuses on the tools and processes for data-driven decision-making: version control with GitHub, importing data into PostgreSQL, data cleaning and transformation, and the application of structured data views to make insights about the dataset.

## Process
**Step 1**- Import csv files into tables in PostgreSQL as text only fields with no keys or constraints. I've learned in a very slow fashion how important lowercase column names are when importing.  

**Step 2**- Look for keys that could be used to link tables and identify primary keys and foreign keys for each table as necessary.  

**Step 3**- Generate an ERD and read the questions to determine which table the information that I'd need would be located; in this case all_sessions. 
 
**Step 4** Given how important it is to not alter original data, I decided to create a cleaned view with only the columns that I actually needed information from that I could base my queries off of. I then determined the required data types for fields that would have functions performed on them and altered null fields or those with missing information to suit my needs.  

**Step 5**- Answered questions one to five using queries referencing my cleaned view.  

**Step 6**- Created my own questions that I had as I viewed and engaged with the data.  

**Step 7**- Performed QA on my results to validate that the cleaning steps performed as I had intended and understand more about my dataset that I was working with. 

## Results
This data was able to tell me how a user got to a website (paid ad, direct typing into, organic search, or referral from another website), what they looked at, how long they look at it, where they were from, and what they purchased.

## Challenges 
One challenge is not knowing how the information was collected or where from. I can ascertain that it must be from webpage history, but I know little else. The result is making several assumptions, mainly that this source seems to focus on information from users in the United States and therefore is not very representative (unless it's for products manufactured in the US). I also don't really know what the end user is hoping to use this information for and had I the opportunity would ask some clarifying questions to the client about what they were hoping to use this information for. There are several empty/null values as well as inconsistent formatting and incomplete information which makes me rely on my discretion when cleaning. 

## Future Goals
I focused my efforts on the all_sessions table and I did notice that sku was used in three other tables. I could use more time to join the tables by the primary/foreign keys and find other interesting trends. 
