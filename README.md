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
-	Software: Python 3.6.1, Visual Studio Code, l.3B.l

## Election Audit Results
The analysis of the election show that: 

- There were 369,711 votes cast in the election.
- 
````python
 # For each row in the CSV file.
    for row in reader:

        # Add to the total vote count
        total_votes = total_votes + 1
 ````

- The number of votes per county were:
  - Jefferson had 10.% of the vote and 38,855 votes
  - Denver had 82.8% of the vote and 306,055 votes.
  - Arapahoe had 6.7% of the vote and 24,801

- The county with the largest turnout was Denver

````
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

         # 6e: Save the county votes to a text file.
        txt_file.write(county_results)

         # 6f: Write an if statement to determine the winning county and get its vote count.
        if (totalcountyvotes > wcounty_count) and (countyvote_percentage > wcounty_percentage):
            wcounty_count = totalcountyvotes
            w_county = county_name
            wcounty_percentage = countyvote_percentage   
````

- The candidates were:
  - Charles Casper Stockham
  - Diana DeGette
  - Raymon Anthony Doane

- The candidates were:
  - Charles Casper Stockham received 23%" of the vote and 85,213 number of votes
  - Diana DeGette received 73.8% of the vote and 272,892 number of votes
  - Raymon Anthony Doane received 3.1% of the vote and 11,606 number of votes
  
- The winner of the election was:
  - Diana DeGette , who received 73.8% of the vote and 272,892 number of votes.

The results were tabulated through a python script and are shown in ***figure 1***.  This script reads the raw election_results.csv data file and performs a number of calculations to produce the results.  In addition this script writes the results to a results.txt file for future reference.

***Figure 1: Terminal Output of Election Results python script***

![Election Results Terminal](/resources/Terminal_Output.png)

## Election Audit Summary
In a summary statement, provide a business proposal to the election commission on how this script can be used—with some modifications—for any election. Give at least two examples of how this script can be modified to be used for other elections.





