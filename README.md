# Lebanon Elections Datasets
Datasets pertaining to Lebanese parliamentary elections

## Table Reference

### agg_results_by_candidate
Contains metadata pertaining to all candidates that ran in Beirut II in 2022 and 2018 (list and sect), as well as the number of votes received in that election year.

Columns:
- **candidate_name_en** (STRING): The name of the candidate in English
- **candidate_name_ar** (STRING): The name of the candidate in Arabic
- **candidate_list_en** (STRING): The name of the list on which the candidate ran in English
- **candidate_list_ar** (STRING): The name of the list on which the candidate ran in Arabic
- **seat** (STRING): The confessional seat being contested by the candidate in that election year
- **num_votes** (INTEGER): The # of votes received by that candidate in that election year
- **num_votes_list** (INTEGER): The # of votes received by that candidate’s entire list in that election year
- **district** (STRING): Electoral district (الدائرة) (beirut_2)
- **election_year** (STRING): Election year (’2022’ / ’2018’)
- **elected** (BOOLEAN): Whether the candidate was elected in that election year (TRUE / FALSE)

### district_overview
Contains aggregated election results on the district level for all electoral districts in Lebanon in 2022 and 2018, including the first and second calculations of the threshold (حاصل) for seat allocation.

Columns:
- **district** (STRING): Electoral district (الدائرة)
- **election_year** (STRING): Election year (’2022’ / ’2018’)
- **num_seats** (INTEGER): The number of seats allocated for that district in that election year
- **num_eligible_voters** (INTEGER): The number of eligible voters in that district in that election year
- **num_eligible_voters_lebanon_v2** (INTEGER): The number of eligible voters in Lebanon in that election year (from different source as num_eligible_voters, resulting in a slight discrepancy)
- **num_eligible_voters_diaspora_v2** (INTEGER): The number of eligible voters in the diaspora in that election year (from different source as num_eligible_voters, resulting in a slight discrepancy)
- **num_votes** (INTEGER): The number of people that voted in that district in that election year
- **num_blank_votes** (INTEGER): The # of blank votes in that district in that election year
- **num_invalid_votes** (INTEGER): The # of invalid votes in that district in that election year
- **num_valid_votes** (INTEGER): The total # of eligible votes, calculated as the # of valid votes + # of blank votes
- **hasel_round_1** (FLOAT): The initial hasel for the district, calculated as num_valid_votes / num_seats
- **num_cancelled_votes** (INTEGER): The number of votes excluded from the final hasel, defined as the sum of votes from parties that receive less than the amount of votes calculated in hasel_round_1
- **num_valid_votes_round_2** (INTEGER): The number of votes used to calculate the final hasel for the district, calculated as num_valid_votes - num_cancelled_votes
- **hasel_round_2** (FLOAT): The final hasel for the district, calculated as num_valid_votes_round_2 / num_seats

### qalam_reference
Contains detailed information for every qalam (قلم الإقتراع) in Beirut II in the 2022 elections: the registration committee (لجنة القيد), the local district (المحلة / الحي), the name of the polling place and room number, and where available, the sect and gender of voters from that qalam. Also included is the total number of votes in that qalam.

Columns:
- **qalam_index** (INTEGER): Index number for the qalam (note: this is NOT analogous to the official qalam number, but is only used as an index to join these tables)
- **committee** (INTEGER): Registration committee of the qalam (لجنة القيد)
- **voter_category** (STRING): Whether the qalam is in Lebanon or abroad (‘lebanon’ / ‘diaspora’)
- **district** (STRING): Electoral district (الدائرة)
- **local_district** (STRING): Coalescence of either 1) the local district in Lebanon for that qalam (المحلة / الحي) or 2) the country outside Lebanon where that qalam is located
- **qalam_num** (INTEGER): The official qalam number (رقم قلم الإقتراع) for that qalam as defined by the Ministry of the Interior and Municipalities
- **polling_place** (STRING): Detailed polling location for that qalam
- **room_number** (INTEGER): Room number for that qalam
- **gender** (STRING):Gender of voters for that qalam (where available)
- **sect** (STRING): Sect of voters for that qalam (where available)
- **num_eligible_voters** (INTEGER): Total # of eligible voters in that qalam (only available for 2018)
- **num_votes** (INTEGER): Total # of voters in that qalam in that election year
- **num_blank_votes** (INTEGER): Number of votes left blank
- **num_invalid_votes** (INTEGER): Number of invalid votes
- **num_valid_votes** (INTEGER): Number of votes eligible to be counted (filled ballots + blank ballots)
- **election_year** (STRING): Election year (’2022’ / ’2018’)

results_by_qalam_candidate
The number of votes obtained by every candidate in each qalam in Beirut II in the 2022 election.

- **qalam_index** (INTEGER): Index number for the qalam (note: this is NOT analogous to the official qalam number, but is only used as an index to join these tables)
- **candidate_name_en** (STRING): The candidate’s name in English (can be joined with agg_results_by_candidate.candidate_name_en) 
- **votes** (INTEGER): The number of votes received by that candidate in that qalam in that election year
- **election_year** (STRING): Election year (’2022’ / ’2018’)

parse_key
A helpful translation table containing English - Arabic translations for all the candidate names, countries in which voting took place, and local districts in Beirut II.

- **arabic** (STRING): The text in Arabic
- **english** (STRING): The text in English

Note: agg_results_by_candidate and district_overview contain data for all districts in Lebanon in 2022 and 2018, however qalam_reference and results_by_qalam_candidate only contain data for Beirut II in 2022.
