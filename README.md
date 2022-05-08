# Election_Analysis for a US Congressional race in Colorado

## Election Audit overview
An employee from the Colorado Board of Elections has requested information about a recent congressional election in their state. The information is intended to audit the results of the election, so the results can be certified.

### For the Module 3 activity, we created a base code that outputs the following information:
1. The total number of votes cast in the election
2. A list of candidates who received votes
3. The total number of votes each candidate received
4. The percentage of votes each candidate won
5. The winner of the election based on the popular vote

### For the challenge portion of this assignment, we were asked to modify our existing code, so that we can also output the following information:
1. A  breakdown of the number of votes and the percentage of total votes for each county in the precinct.
2. The county with the largest number of votes.
- - - -
## Election-Audit Results

### Total votes cast: 
369,711 total votes were cast in the election

* This code helps tally our votes:
```
# For each row in the CSV file.
   for row in reader:
 
       # Add to the total vote count
       total_votes = total_votes + 1
```
### County Votes(% of total votes and number of votes):
1. Jefferson: 10.5% (38,855)
2. Denver: 82.8% (306,055)
3. Arapahoe: 6.7% (24,801)

* This code helps us tally the votes for each county
```
if county_name not in county_list:    
 
           # 4b: Add the existing county to the list of counties.
           county_list.append(county_name)
 
           # 4c: Begin tracking the county's vote count.
           county_votes[county_name] = 0
 
       # 5: Add a vote to that county's vote count.
       county_votes[county_name] += 1
```
* And this part of the code calculates the % of the vote secured by county and displays the results in the terminal and in the txt file:
```
# 6a: Write a for loop to get the county from the county dictionary.
   for county_name in county_votes:
 
       # 6b: Retrieve the county vote count.
       votes = county_votes[county_name]
 
       # 6c: Calculate the percentage of votes for the county.
       vote_percentage = float(votes) / float(total_votes) * 100
 
       # 6d: Print the county results to the terminal.
       county_results = (
           f"{county_name}: {vote_percentage:.1f}% ({votes:,})\n")
       print(county_results)  
 
       # 6e: Save the county votes to a text file.
       txt_file.write(county_results)
```
### Largest County Turnout: 
Denver

### Candidate Votes(% of total votes and number of votes):
1. Charles Casper Stockham: 23.0% (85,213)
2. Diana DeGette: 73.8% (272,892)
3. Raymon Anthony Doane: 3.1% (11,606)

* This code helps us tally the votes for each candidate:
```
# If the candidate does not match any existing candidate add it to
       # the candidate list
       if candidate_name not in candidate_options:
 
           # Add the candidate name to the candidate list.
           candidate_options.append(candidate_name)
 
           # And begin tracking that candidate's voter count.
           candidate_votes[candidate_name] = 0
 
       # Add a vote to that candidate's count
       candidate_votes[candidate_name] += 1
```
* And this part of the code calculates the % of the vote secured by candidate and displays the results in the terminal and in the txt file:
```
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
       txt_file.write(candidate_results)
```
### Winning candidate, their vote count, and their percentage of the total votes:
* Winner: Diana DeGette
* Winning Vote Count: 272,892
* Winning Percentage: 73.8%


* This code outlines the winner of the election, their vote count and the percentage of the total vote count that they secured. Then, it prints the results to the terminal and in the txt file:
```
# Determine winning vote count, winning percentage, and candidate.
       if (votes > winning_count) and (vote_percentage > winning_percentage):
           winning_count = votes
           winning_candidate = candidate_name
           winning_percentage = vote_percentage
 
   # Print the winning candidate (to terminal)
   winning_candidate_summary = (
       f"-------------------------\n"
       f"Winner: {winning_candidate}\n"
       f"Winning Vote Count: {winning_count:,}\n"
       f"Winning Percentage: {winning_percentage:.1f}%\n"
       f"-------------------------\n")
   print(winning_candidate_summary)
 
   # Save the winning candidate's name to the text file
   txt_file.write(winning_candidate_summary)
```
### Results printed to the Command Line
<img width="605" alt="Screen Shot 2022-05-08 at 10 46 50 AM" src="https://user-images.githubusercontent.com/103781847/167304124-50ec0161-4b02-4938-b4c3-1fef582eb0c9.png">

- - - -

## Election-Audit Summary
We’ve completed the more time-consuming task of building a set of code to tally election results and segment it by candidate, county, etc. Now, we can use the code as a template to use for other elections. Here are a couple different ways we can modify the code to use it for other elections.
1. Most simply, we can update the data source this code is pulling from, in order to pull in a similar data set for another election. More specifically, we can update this portion at the beginning of the code and change the path to pull in a different csv file with election data. As long as the data is structured similarly (Ballot Id, County, Candidate), then we really don’t need to modify the code much.
### Code to change: 
``` 
file_to_load = os.path.join("Resources", "election_results.csv")
```
2. We could also modify this code in order to use it to look at votes in a national election. Instead of separating the data out by different counties, the data might include which state the ballot is from and who they voted for. In that case, we would be creating a list of states and a dictionary of state votes.
### Code to change: 
```
county_list = []
county_votes = {}
```
- - - -
### Resources
* Data Source: election_results.csv
* Software: Python (3.8.9 64-bit), Visual Studio Code (Version: 1.66.2 - Universal)
