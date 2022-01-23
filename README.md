# Election Analysis 
## Overview of Election Audit 
The Colorado Board of Elections requires a tabulation of the election results.  The analysis will show:

1.	The total number of votes cast.
2.	The number of votes by county and percentage of the vote
3.	The County with the largest turnout
4.	A complete list of candidates who received votes.
5.	The total number of votes each candidate received and the percentage of votes each candidate won.
6.	The winner of the election based on popular vote.

## Resources
-	Data Source: election_results.csv
-	Software: Python 3.7, Visual Studio Code, l.63.2

## Election Audit Results
The election results python script, tabulates its results from a raw data file named ***election_results.csv***.  This file contains the following three columns of data: Ballot ID, Count, and Candidate Voted for. 

The first section of the script initializes a number of variables, lists & dictionaries to track:
- total_votes is a variable used to store the Total # of votes
- totalcounty_votes is a variable used to store the Total # of votes per county
- candidate_options is a list used to store a unique list of candidate names contained in the file
- candidate_votes is a dictionary used to store the candidate and number of votes they received
- county_list is a list used to store a unitque list of counties in the file
- county_votes is a dictionary used to store the county and number of votes it received
- winning_candidate
- winning_count is a variable used to store the count for the winning candidate
- winning_percentage is a variable used to store the percentage for the winning candidate
- w_county is a variable used to store the name of the winning county
- wcounty_count is a variable used to store the count for the winning county
- wcounty_percentage is a variable used to store the percentage for the winning candidate

````python
# Initialize a total vote counter.
total_votes = 0 #total_votes is a variable used to store the Total # of votes

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

### Total Number of Votes Cast

- There were 369,711 votes cast in the election.  

- This result is derived from the code below which shows a total votes variable being incremented at each row.

````python
 # For each row in the CSV file.
    for row in reader:

        # Add to the total vote count
        total_votes = total_votes + 1
 ````
###  Total Number of Votes by County

- The number of votes per county were:
  - ***Jefferson*** had ***10.%*** of the vote and ***38,855*** votes
  - ***Denver*** had ***82.8%*** of the vote and ***306,055*** votes.
  - ***Arapahoe*** had ***6.7%*** of the vote and ***24,801*** votes.

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

The county with the largest turnout was ***Denver***.

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
 The winner of the election was ***Diana DeGette*** , who received ***73.8%*** of the vote and ***272,892*** number of votes.

````python
        # Determine winning vote count, winning percentage, and candidate.
        if (votes > winning_count) and (vote_percentage > winning_percentage):
            winning_count = votes
            winning_candidate = candidate_name
            winning_percentage = vote_percentage
````
### Results Summary

The results were tabulated through a python script and are shown in ***figure 1***.  This script reads the raw election_results.csv data file and performs a number of calculations to produce the results.  In addition this script writes the results to a results.txt file for future reference.

***Figure 1: Terminal Output of Election Results python script***

![Election Results Terminal](/resources/Terminal_Output.png)

## Election Audit Summary
In a summary statement, provide a business proposal to the election commission on how this script can be used—with some modifications—for any election. Give at least two examples of how this script can be modified to be used for other elections.





