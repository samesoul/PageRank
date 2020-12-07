# PageRank
Implementation of simple search engine for the website https://www.lawfareblog.com. 
Coursework for CSCI145: Data Mining.

## Task 1: Power Method 
**Part 1:** For my implementation on the `small.csv.gz` graph, I get the following output:
```
$ python3 pagerank.py --data=./small.csv.gz --verbose
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=6.0257e-01 url=4
INFO:root:rank=1 pagerank=4.6414e-01 url=6
INFO:root:rank=2 pagerank=3.4544e-01 url=5
INFO:root:rank=3 pagerank=1.2732e-01 url=2
INFO:root:rank=4 pagerank=9.9210e-02 url=3
INFO:root:rank=5 pagerank=8.9347e-02 url=1
```

**Part 2:** The `pagerank.py` file has option `--search_query`, which takes a string as a parameter.
This gives us the most important pages on the blog related to our query.

My results for the search queries `corona`, `trump`, and `iran` are as follows:
```
$ python3 pagerank.py --data=./lawfareblog.csv.gz --search_query='corona'
INFO:root:rank=0 pagerank=0.001003776676952839 url=www.lawfareblog.com/lawfare-podcast-united-nations-and-coronavirus-crisis
INFO:root:rank=1 pagerank=0.0008922395063564181 url=www.lawfareblog.com/house-oversight-committee-holds-day-two-hearing-government-coronavirus-response
INFO:root:rank=2 pagerank=0.0007039029151201248 url=www.lawfareblog.com/britains-coronavirus-response
INFO:root:rank=3 pagerank=0.0006915341946296394 url=www.lawfareblog.com/prosecuting-purposeful-coronavirus-exposure-terrorism
INFO:root:rank=4 pagerank=0.000670412031468004 url=www.lawfareblog.com/israeli-emergency-regulations-location-tracking-coronavirus-carriers
INFO:root:rank=5 pagerank=0.0006625585374422371 url=www.lawfareblog.com/why-congress-conducting-business-usual-face-coronavirus
INFO:root:rank=6 pagerank=0.0006504578050225973 url=www.lawfareblog.com/congressional-homeland-security-committees-seek-ways-support-state-federal-responses-coronavirus
INFO:root:rank=7 pagerank=0.0006361958803609014 url=www.lawfareblog.com/paper-hearing-experts-debate-digital-contact-tracing-and-coronavirus-privacy-concerns
INFO:root:rank=8 pagerank=0.000612482544966042 url=www.lawfareblog.com/house-subcommittee-voices-concerns-over-us-management-coronavirus
INFO:root:rank=9 pagerank=0.0006018723943270743 url=www.lawfareblog.com/livestream-house-oversight-committee-holds-hearing-government-coronavirus-response

$ python3 pagerank.py --data=./lawfareblog.csv.gz --search_query='trump'
INFO:root:rank=0 pagerank=0.005782557651400566 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=0.005233839154243469 url=www.lawfareblog.com/document-trump-revokes-obama-executive-order-counterterrorism-strike-casualty-reporting
INFO:root:rank=2 pagerank=0.005129670724272728 url=www.lawfareblog.com/trump-administrations-worrying-new-policy-israeli-settlements
INFO:root:rank=3 pagerank=0.004659898113459349 url=www.lawfareblog.com/dc-circuit-overrules-district-courts-due-process-ruling-qasim-v-trump
INFO:root:rank=4 pagerank=0.004593398422002792 url=www.lawfareblog.com/donald-trump-and-politically-weaponized-executive-branch
INFO:root:rank=5 pagerank=0.004307133611291647 url=www.lawfareblog.com/how-trumps-approach-middle-east-ignores-past-future-and-human-condition
INFO:root:rank=6 pagerank=0.0040934765711426735 url=www.lawfareblog.com/why-trump-cant-buy-greenland
INFO:root:rank=7 pagerank=0.0037590833380818367 url=www.lawfareblog.com/oral-argument-summary-qassim-v-trump
INFO:root:rank=8 pagerank=0.003450872143730521 url=www.lawfareblog.com/dc-circuit-court-denies-trump-rehearing-mazars-case
INFO:root:rank=9 pagerank=0.0034484383650124073 url=www.lawfareblog.com/second-circuit-rules-mazars-must-hand-over-trump-tax-returns-new-york-prosecutors

$ python3 pagerank.py --data=./lawfareblog.csv.gz --search_query='iran'
INFO:root:rank=0 pagerank=3.4969e-02 url=www.lawfareblog.com/trump-administrations-worrying-new-policy-israeli-settlements
INFO:root:rank=1 pagerank=3.4133e-02 url=www.lawfareblog.com/update-military-commissions-continued-health-issues-recusal-motion-and-new-cell-al-iraqi
INFO:root:rank=2 pagerank=2.9199e-02 url=www.lawfareblog.com/how-us-iran-tensions-could-disrupt-iraqs-fragile-peace
INFO:root:rank=3 pagerank=2.8807e-02 url=www.lawfareblog.com/haftar-attacking-tripoli-us-needs-re-engage-libya
INFO:root:rank=4 pagerank=2.3394e-02 url=www.lawfareblog.com/france-makes-play-try-foreign-fighters-iraq
INFO:root:rank=5 pagerank=1.4578e-02 url=www.lawfareblog.com/its-not-only-iraq-and-syria
INFO:root:rank=6 pagerank=1.2142e-02 url=www.lawfareblog.com/document-sens-kaine-and-young-introduce-bill-revoke-iraq-force-authorizations
INFO:root:rank=7 pagerank=9.0182e-03 url=www.lawfareblog.com/assessing-aclu-habeas-petition-behalf-unnamed-us-citizen-held-enemy-combatant-iraq
INFO:root:rank=8 pagerank=8.9187e-03 url=www.lawfareblog.com/primer-can-trump-administration-transfer-american-citizen-enemy-combatant-iraqi-custody
INFO:root:rank=9 pagerank=6.9855e-03 url=www.lawfareblog.com/what-cia-could-learn-uk-government-apology-over-libyan-rendition-case
```

**Part 3:**
The `--filter_ratio` argument (range from 0 to 1) removes all pages that have more links than the specified fraction.
To demonstrate this, compare the following two output.
```
$ python3 pagerank.py --data=./lawfareblog.csv.gz
INFO:root:rank=0 pagerank=0.2874051630496979 url=www.lawfareblog.com/about-lawfare-brief-history-term-and-site
INFO:root:rank=1 pagerank=0.2874051630496979 url=www.lawfareblog.com/lawfare-job-board
INFO:root:rank=2 pagerank=0.2874051630496979 url=www.lawfareblog.com/masthead
INFO:root:rank=3 pagerank=0.2874051630496979 url=www.lawfareblog.com/litigation-documents-resources-related-travel-ban
INFO:root:rank=4 pagerank=0.2874051630496979 url=www.lawfareblog.com/subscribe-lawfare
INFO:root:rank=5 pagerank=0.2874051630496979 url=www.lawfareblog.com/litigation-documents-related-appointment-matthew-whitaker-acting-attorney-general
INFO:root:rank=6 pagerank=0.2874051630496979 url=www.lawfareblog.com/documents-related-mueller-investigation
INFO:root:rank=7 pagerank=0.2874051630496979 url=www.lawfareblog.com/our-comments-policy
INFO:root:rank=8 pagerank=0.2874051630496979 url=www.lawfareblog.com/upcoming-events
INFO:root:rank=9 pagerank=0.2874051630496979 url=www.lawfareblog.com/topics
```

```
$ python3 pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2
INFO:root:rank=0 pagerank=0.3469613492488861 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=0.29521211981773376 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=2 pagerank=0.29039666056632996 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=3 pagerank=0.15178653597831726 url=www.lawfareblog.com/lawfare-podcast-ben-nimmo-whack-mole-game-disinformation
INFO:root:rank=4 pagerank=0.15098513662815094 url=www.lawfareblog.com/todays-headlines-and-commentary-1964
INFO:root:rank=5 pagerank=0.15098513662815094 url=www.lawfareblog.com/todays-headlines-and-commentary-1963
INFO:root:rank=6 pagerank=0.15071173012256622 url=www.lawfareblog.com/lawfare-podcast-week-was-impeachment
INFO:root:rank=7 pagerank=0.14956679940223694 url=www.lawfareblog.com/todays-headlines-and-commentary-1962
INFO:root:rank=8 pagerank=0.14366623759269714 url=www.lawfareblog.com/cyberlaw-podcast-mistrusting-google
INFO:root:rank=9 pagerank=0.14239734411239624 url=www.lawfareblog.com/lawfare-podcast-bonus-edition-gordon-sondland-vs-committee-no-bull

```

**Part 4:**
The following output are the results from running the following four commands:
```
$ python3 pagerank.py --data=./lawfareblog.csv.gz --verbose 
$ python3 pagerank.py --data=./lawfareblog.csv.gz --verbose --alpha=0.99999
$ python3 pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2
$ python3 pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2 --alpha=0.99999
```

```
$ python3 pagerank.py --data=./lawfareblog.csv.gz --verbose 
INFO:root:rank=0 pagerank=0.2874051630496979 url=www.lawfareblog.com/about-lawfare-brief-history-term-and-site
INFO:root:rank=1 pagerank=0.2874051630496979 url=www.lawfareblog.com/lawfare-job-board
INFO:root:rank=2 pagerank=0.2874051630496979 url=www.lawfareblog.com/masthead
INFO:root:rank=3 pagerank=0.2874051630496979 url=www.lawfareblog.com/litigation-documents-resources-related-travel-ban
INFO:root:rank=4 pagerank=0.2874051630496979 url=www.lawfareblog.com/subscribe-lawfare
INFO:root:rank=5 pagerank=0.2874051630496979 url=www.lawfareblog.com/litigation-documents-related-appointment-matthew-whitaker-acting-attorney-general
INFO:root:rank=6 pagerank=0.2874051630496979 url=www.lawfareblog.com/documents-related-mueller-investigation
INFO:root:rank=7 pagerank=0.2874051630496979 url=www.lawfareblog.com/our-comments-policy
INFO:root:rank=8 pagerank=0.2874051630496979 url=www.lawfareblog.com/upcoming-events
INFO:root:rank=9 pagerank=0.2874051630496979 url=www.lawfareblog.com/topics
```

```
$ python3 pagerank.py --data=./lawfareblog.csv.gz --verbose --alpha=0.99999
INFO:root:rank=0 pagerank=0.28859302401542664 url=www.lawfareblog.com/snowden-revelations
INFO:root:rank=1 pagerank=0.28859302401542664 url=www.lawfareblog.com/lawfare-job-board
INFO:root:rank=2 pagerank=0.28859302401542664 url=www.lawfareblog.com/documents-related-mueller-investigation
INFO:root:rank=3 pagerank=0.28859302401542664 url=www.lawfareblog.com/litigation-documents-resources-related-travel-ban
INFO:root:rank=4 pagerank=0.28859302401542664 url=www.lawfareblog.com/subscribe-lawfare
INFO:root:rank=5 pagerank=0.28859302401542664 url=www.lawfareblog.com/topics
INFO:root:rank=6 pagerank=0.28859302401542664 url=www.lawfareblog.com/masthead
INFO:root:rank=7 pagerank=0.28859302401542664 url=www.lawfareblog.com/our-comments-policy
INFO:root:rank=8 pagerank=0.28859302401542664 url=www.lawfareblog.com/upcoming-events
INFO:root:rank=9 pagerank=0.28859302401542664 url=www.lawfareblog.com/litigation-documents-related-appointment-matthew-whitaker-acting-attorney-general
```

```
$ python3 pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=0.3469613492488861 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=0.29521211981773376 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=2 pagerank=0.29039666056632996 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=3 pagerank=0.15178653597831726 url=www.lawfareblog.com/lawfare-podcast-ben-nimmo-whack-mole-game-disinformation
INFO:root:rank=4 pagerank=0.15098513662815094 url=www.lawfareblog.com/todays-headlines-and-commentary-1964
INFO:root:rank=5 pagerank=0.15098513662815094 url=www.lawfareblog.com/todays-headlines-and-commentary-1963
INFO:root:rank=6 pagerank=0.15071173012256622 url=www.lawfareblog.com/lawfare-podcast-week-was-impeachment
INFO:root:rank=7 pagerank=0.14956679940223694 url=www.lawfareblog.com/todays-headlines-and-commentary-1962
INFO:root:rank=8 pagerank=0.14366623759269714 url=www.lawfareblog.com/cyberlaw-podcast-mistrusting-google
INFO:root:rank=9 pagerank=0.14239734411239624 url=www.lawfareblog.com/lawfare-podcast-bonus-edition-gordon-sondland-vs-committee-no-bull
```

```
$ python3 pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2 --alpha=0.99999
INFO:root:rank=0 pagerank=0.7014895677566528 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
INFO:root:rank=1 pagerank=0.7014873623847961 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
INFO:root:rank=2 pagerank=0.10551629960536957 url=www.lawfareblog.com/cost-using-zero-days
INFO:root:rank=3 pagerank=0.03175504133105278 url=www.lawfareblog.com/lawfare-podcast-former-congressman-brian-baird-and-daniel-schuman-how-congress-can-continue-function
INFO:root:rank=4 pagerank=0.022039713338017464 url=www.lawfareblog.com/events
INFO:root:rank=5 pagerank=0.01602667197585106 url=www.lawfareblog.com/water-wars-increased-us-focus-indo-pacific
INFO:root:rank=6 pagerank=0.016025930643081665 url=www.lawfareblog.com/water-wars-drill-maybe-drill
INFO:root:rank=7 pagerank=0.016022762283682823 url=www.lawfareblog.com/water-wars-disjointed-operations-south-china-sea
INFO:root:rank=8 pagerank=0.016019931063055992 url=www.lawfareblog.com/water-wars-song-oil-and-fire
INFO:root:rank=9 pagerank=0.016019923612475395 url=www.lawfareblog.com/water-wars-sinking-feeling-philippine-china-relations
```

My code took around 30, 70 iterations for the commands without the `alpha` arguments, while the calls with `alpha` arguments both took their respective `max_iteration` values.  

## Task 2: the personalization vector

**Part 1:**
Implemented the `WebGraph.make_personalization_vector` function.
This function enables the `--personlization_vector_query` command line argument, which provides an alternative method for searching by doing the filtering on the personalization vector.

An example implementation, with filtering with the query `corona` is shown:
```
$ python3 pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --personalization_vector_query='corona'
INFO:root:rank=0 pagerank=0.6321316361427307 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
INFO:root:rank=1 pagerank=0.6321078538894653 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
INFO:root:rank=2 pagerank=0.1496182531118393 url=www.lawfareblog.com/chinatalk-how-party-takes-its-propaganda-global
INFO:root:rank=3 pagerank=0.11625612527132034 url=www.lawfareblog.com/rational-security-my-corona-edition
INFO:root:rank=4 pagerank=0.11625612527132034 url=www.lawfareblog.com/brexit-not-immune-coronavirus
INFO:root:rank=5 pagerank=0.08883301168680191 url=www.lawfareblog.com/trump-cant-reopen-country-over-state-objections
INFO:root:rank=6 pagerank=0.08544307202100754 url=www.lawfareblog.com/prosecuting-purposeful-coronavirus-exposure-terrorism
INFO:root:rank=7 pagerank=0.08544307202100754 url=www.lawfareblog.com/britains-coronavirus-response
INFO:root:rank=8 pagerank=0.07188324630260468 url=www.lawfareblog.com/lawfare-podcast-united-nations-and-coronavirus-crisis
INFO:root:rank=9 pagerank=0.06896847486495972 url=www.lawfareblog.com/house-oversight-committee-holds-day-two-hearing-government-coronavirus-response
```

**Part 2:**
The `--personalization_vector_query` option also allows us to find what webpages are related to a query that don't explicitly mention the query, which can help us map out similar topics.

Below is an example of webpage ranking by their `corona` importance, but removing webpages explicitly mentioning `corona` from the results.
```
$ python3 pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --personalization_vector_query='corona' --search_query='-corona'
INFO:root:rank=0 pagerank=0.6321316361427307 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
INFO:root:rank=1 pagerank=0.6321078538894653 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
INFO:root:rank=2 pagerank=0.1496182531118393 url=www.lawfareblog.com/chinatalk-how-party-takes-its-propaganda-global
INFO:root:rank=3 pagerank=0.08883301168680191 url=www.lawfareblog.com/trump-cant-reopen-country-over-state-objections
INFO:root:rank=4 pagerank=0.06856223940849304 url=www.lawfareblog.com/lawfare-podcast-mom-and-dad-talk-clinical-trials-pandemic
INFO:root:rank=5 pagerank=0.06583793461322784 url=www.lawfareblog.com/fault-lines-foreign-policy-quarantined
INFO:root:rank=6 pagerank=0.06138917803764343 url=www.lawfareblog.com/limits-world-health-organization
INFO:root:rank=7 pagerank=0.05593918263912201 url=www.lawfareblog.com/chinatalk-dispatches-shanghai-beijing-and-hong-kong
INFO:root:rank=8 pagerank=0.054060198366642 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=9 pagerank=0.04936344921588898 url=www.lawfareblog.com/us-moves-dismiss-case-against-company-linked-ira-troll-farm
```

**Part 3:**
To explore a national security topic other than coronavirus, I searched articles related to `guantanamo` but did not explicitly contain the word `guantanamo`. The related articles were largely comprised of hearings, briefings, and congressional documents, in addition to prolific cases of unethical detention such as [Al Alawai vs. Trump](https://www.supremecourt.gov/opinions/18pdf/18-740_2c8f.pdf). 
```
$ python3 pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --personalization_vector_query='guantanamo' --search_query='-guantanamo'
INFO:root:rank=0 pagerank=0.3552566170692444 url=www.lawfareblog.com/justice-breyers-question-al-alwi-detention-still-justified
INFO:root:rank=1 pagerank=0.33640775084495544 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=2 pagerank=0.25916406512260437 url=www.lawfareblog.com/dc-circuit-overrules-district-courts-due-process-ruling-qasim-v-trump
INFO:root:rank=3 pagerank=0.2367464154958725 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=4 pagerank=0.23674610257148743 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=5 pagerank=0.20767821371555328 url=www.lawfareblog.com/document-government-briefing-opposing-supreme-court-review-al-alwi
INFO:root:rank=6 pagerank=0.15983335673809052 url=www.lawfareblog.com/oral-argument-summary-qassim-v-trump
INFO:root:rank=7 pagerank=0.11743602901697159 url=www.lawfareblog.com/summary-david-holmess-deposition-testimony
INFO:root:rank=8 pagerank=0.1137523278594017 url=www.lawfareblog.com/livestream-justice-department-inspector-general-testifies-senate-committee
INFO:root:rank=9 pagerank=0.11220303177833557 url=www.lawfareblog.com/france-makes-play-try-foreign-fighters-iraq
```
