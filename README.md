# Election-Analysis-

```

# Add our dependencies.
import csv
import os

# Add a variable to load a file from a path.
file_to_load = os.path.join("..", "Resources", "election_results.csv")
# Add a variable to save the file to a path.
file_to_save = os.path.join("..","Resources", "election_analysis.txt")

# Initialize a total vote counter.
total_votes = 0
total_county_votes = 0

# Candidate Options and candidate votes.
candidate_options = []
candidate_votes = {}

# 1: Create a county list and county votes dictionary.
county_votes = {}
county_options = []

# Track the winning candidate, vote count and percentage
winning_candidate = ""
winning_count = 0
winning_percentage = 0

#track the winning county, vote and percentage 
winning_county = ""
winning_county_count = 0
winning_county_percentage = 0

# 2: Track the largest county and county voter turnout.

# Read the csv and convert it into a list of dictionaries
with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    # Read the header
    header = next(reader)

    # For each row in the CSV file.
    for row in reader:
       

        # Get the candidate name from each row.
        candidate_name = row[2]

        # 3: Extract the county name from each row.
        county_option = row[1]

        # If the candidate does not match any existing candidate add it to
        # the candidate list
        if candidate_name not in candidate_options:

            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0

        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1

#Add to the total county vote count 
        total_votes = total_votes + 1

        # 4a: Write an if statement that checks that the
        

        # county does not match any existing county in the county list.
        if county_option not in county_options:

            # 4b: Add the existing county to the list of counties.
            county_options.append(county_option)

            # 4c: Begin tracking the county's vote count.
            county_votes[county_option] = 0

        county_votes[county_option] += 1

        # 5: Add a vote to that county's vote count.


        # Add to total county count


# Save the results to our text file.
with open(file_to_save, "w") as txt_file:

    # Print the final vote count (to terminal)
    election_results = (
        f"\nElection Results\n"
        f"-------------------------\n"
        f"Total Votes: {total_votes:,}\n"
        f"-------------------------\n\n"
        f"County Votes:\n")
    print(election_results, end="")

    txt_file.write(election_results)

    # 6a: Write a for loop to get the county from the county dictionary. 
    
        # 6b: Retrieve the county vote count.
    

        # 6c: Calculate the percentage of votes for the county.
    for county_name in county_votes:

        mycounty_votes = county_votes.get(county_name)
        county_vote_percentage = float(mycounty_votes) / float(total_votes)* 100
        county_results = (
            f"{county_name}: {county_vote_percentage:.1f}% ({mycounty_votes:,})\n")
         # 6d: Print the county results to the terminal.
        print(county_results)
         # 6e: Save the county votes to a text file.
        txt_file.write(county_results)

         # 6f: Write an if statement to determine the winning county and get its vote count.
        if (mycounty_votes > winning_county_count):
                winning_county_count = mycounty_votes
                winning_county = county_name

    # 7: Print the county with the largest turnout to the terminal.
        winning_county_summary = (
            f"-------------------------\n"
            f"Winner: {winning_county}\n"
            f"Winning Vote Count: {winning_county_count:,}\n"
            # f"Winning Percentage: {winning_count}%\n"
            f"-------------------------\n")
    print(winning_county_summary)

    # 8: Save the county with the largest turnout to a text file.
    txt_file.write(winning_county_summary)

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
        txt_file.write(candidate_results)

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

### Overview of Election Audit: Explain the purpose of this election audit analysis.

The purpose of thise challenge was to use python to extract election results by counties.

### Election-Audit Results: Using a bulleted list, address the following election outcomes. Use images or examples of your code as support where necessary.

These are the outcome of the election:
County Votes:
Jefferson: 10.5% (38,855)

Denver: 82.8% (306,055)

Arapahoe: 6.7% (24,801)

-------------------------
Winner: Denver
Winning Vote Count: 306,055
-------------------------

Charles Casper Stockham: 23.0% (85,213)

Diana DeGette: 73.8% (272,892)

Raymon Anthony Doane: 3.1% (11,606)

-------------------------
Winner: Diana DeGette
Winning Vote Count: 272,892
Winning Percentage: 73.8%

### How many votes were cast in this congressional election?

369,711 VOTES
Provide a breakdown of the number of votes and the percentage of total votes for each county in the precinct.
Which county had the largest number of votes?

DENVER HAD THE LARGEST NUMBER OF VOTES 


### Which candidate won the election, what was their vote count, and what was their percentage of the total votes?

DIANA HAD 73.8% OF THE VOTES WITH 272,892 VOTES 

Election-Audit Summary: In a summary statement, provide a business proposal to the election commission on how this script can be used—with some modifications—for any election. Give at least two examples of how this script can be modified to be used for other elections. 

THIS IS A GREAT SOURCE OF CODE AS WE CAN EASILY SUMAMRIZE HOW ANY CANDIDATE IS PERFORMING WITH A VERY NUANCED PERSPECTIVE. THIS CAN EVEN BE USED AT THE STATE LEVEL TO SEE HOW CANDIDATES ACROSS THE COUNTRY ARE DOING, WITH SMALL MODIFICATIONS TO THE NUMBER OF PLACES
