# Election Analysis 
## Overview of Election Audit 
The Colorado Board of Elections requires a tabulation of the election results.  The analysis will show:

1.	The total number of votes cast.
2.	The county results, showing the number of votes by county and percentage of the vote
3.	The county with the largest turnout
4.	A complete list of candidates who received votes.
5.	The candidate results, showing the total number of votes each candidate received and the percentage of votes each candidate won.
6.	The winner of the election.

## Resources
-	Data Source: election_results.csv
-	Software: Python 3.7, Visual Studio Code, l.63.2

## Election Audit Results

This section of the report focuses on the main sections of the election results python script to derive the results shown in ***figure 1***.  In addition this script writes the results to a results.txt file for future reference.

***Figure 1: Terminal Output of Election Results python script***
![Election Results Terminal](/resources/Terminal_Output.png)

The main sections of the code are:
-   Initializing and populating variables, lists and dictionaries
-   Tabulating the total number of votes cast
-   Tabulating the total number of votes by county
-   Tabulating the candidate results

### Initializing and Populating Variables, Lists, & Dictionaries
The election results python script, tabulates its results from a raw data file named ***election_results.csv***.  This file contains the following three columns of data: Ballot ID, Count, and Candidate Voted for. 

The first section of the script initializes a number of variables, lists & dictionaries to store values or results.  These are later used in the code for calculations.

````python
# Initialize a total vote counter.
total_votes = 0 

# Initialize a county vote
totalcounty_votes=0

# Candidate Options and candidate votes.
candidate_options = []
candidate_votes = {}

# 1: Create a county list and county votes dictionary.
county_list =[]
county_votes={}

# Track the winning candidate, vote count and percentage
winning_candidate = ""
winning_count = 0
winning_percentage = 0

# 2: Track the largest county and county voter turnout.
w_county =""
wcounty_count=0
wcounty_percentage=0
````
The next major section of the code initiates a nested **for loop** within a **with** clause.  This for loop iterates through the file rows getting the total votes, candidate name and county names.  

````python
    for row in reader:

        # Add to the total vote count
        total_votes = total_votes + 1

        # Get the candidate name from each row.
        candidate_name = row[2]

        # 3: Extract the county name from each row.
        county_name = row[1]
````
It then uses two **if** statements within the **for loop**.

The first **if** statement:
-   populate the candidates_options list with the candidate name and append if not found
-   initializes the candidate_votes dictionary counter to 0
-   adds the total number of votes to the candidate_votes dictionary per candidate as it loops

````python
        # If the candidate does not match any existing candidate add it to
        # the candidate list
        if candidate_name not in candidate_options:

            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0

        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1
````

The second **if** statement:
-   populates the county_list list with the county name
-   initializes the county_votes dictionary counter to 0
-   adds the total # of votes to the county_votes dictionary per candidate as it loops

````python

        # 4a: Write an if statement that checks that the
        # county does not match any existing county in the county list.
        if county_name not in county_list:
        
            # 4b: Add the existing county to the list of counties.
            county_list.append(county_name)

            # 4c: Begin tracking the county's vote count.
            county_votes[county_name] =0

        # 5: Add a vote to that county's vote count.
        county_votes[county_name] += 1
````

### Total Number of Votes Cast

- There were 369,711 votes cast in the election.  

- This result is derived from the code below which shows a total votes variable being incremented at each row.

````python
 # For each row in the CSV file.
    for row in reader:

        # Add to the total vote count
        total_votes = total_votes + 1
 ````
###  County Results

- The number of votes per county were:
  - ***Jefferson*** had ***10.%*** of the vote and ***38,855*** votes
  - ***Denver*** had ***82.8%*** of the vote and ***306,055*** votes.
  - ***Arapahoe*** had ***6.7%*** of the vote and ***24,801*** votes.

- In this code block we see a **for loop** being in used to iterate and calculate the total county votes variable.  The next statement uses the total county votes variable and divides it by the total votes variable calculated earlier to get the vote percentage.  The last statement then formats the results for output in the terminal

````python
    # 6a: Write a for loop to get the county from the county dictionary.
    for county_name in county_votes:
        # 6b: Retrieve the county vote count.
        totalcountyvotes = county_votes.get(county_name)
        # 6c: Calculate the percentage of votes for the county.
        
        countyvote_percentage = float(totalcountyvotes) / float(total_votes) *100

         # 6d: Print the county results to the terminal.
        county_results = (
            f"{county_name}: {countyvote_percentage:.1f}% ({totalcountyvotes:,})\n")
        print(county_results)
````

-   The county with the largest turnout was ***Denver***.
-   This code block calculates the largest turnout using a conditional **if** as well as the **And** operator.  This code block is nested within a **for loop** which is iterating to calculate the county votes and percentages.  

````python
         # 6f: Write an if statement to determine the winning county and get its vote count.
        if (totalcountyvotes > wcounty_count) and (countyvote_percentage > wcounty_percentage):
            wcounty_count = totalcountyvotes
            w_county = county_name
            wcounty_percentage = countyvote_percentage   
````
### Candidate Results

- The candidates were:
  - ***Charles Casper Stockham*** received ***23%"*** of the vote and ***85,213*** number of votes
  - ***Diana DeGette*** received ***73.8%*** of the vote and ***272,892*** number of votes
  - ***Raymon Anthony Doane*** received ***3.1%*** of the vote and ***11,606*** number of votes

-   This code block follows the same pattern as the one used to calculate the county results.

````python
# Save the final candidate vote count to the text file.
    for candidate_name in candidate_votes:

        # Retrieve vote count and percentage
        votes = candidate_votes.get(candidate_name)
        vote_percentage = float(votes) / float(total_votes) * 100
        candidate_results = (
            f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

        # Print each candidate's voter count and percentage to the
        # terminal.
        print(candidate_results)
        #  Save the candidate results to our text file.
````        
-   The winner of the election was ***Diana DeGette*** , who received ***73.8%*** of the vote and ***272,892*** number of votes.
-   This code block uses the same pattern used to determine the county with the largest turnout

````python
        # Determine winning vote count, winning percentage, and candidate.
        if (votes > winning_count) and (vote_percentage > winning_percentage):
            winning_count = votes
            winning_candidate = candidate_name
            winning_percentage = vote_percentage
````



## Election Audit Summary
In a summary statement, provide a business proposal to the election commission on how this script can be used—with some modifications—for any election. Give at least two examples of how this script can be modified to be used for other elections.




