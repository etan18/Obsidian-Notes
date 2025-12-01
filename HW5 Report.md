
1. Analysis for the predictions from both the finetuned model and few-shot prompting using semantically similar examples, including discussion of syntax errors (failure to execute) vs. semantic errors, and any similarities/differences in errors between the two approaches.


2. Discussion of execution accuracy vs. exact match accuracy.

**Exact match accuracy** overlooks cases where there may be more than one right way to query the database to answer the provided question (for example, if similar information is available in multiple columns or column values may be derived from one another). In instances where we may care about execution time/efficiency (such as in large databases), doing exact match accuracy to ensure the provided query is also the most efficient solution may be desired.

The opposite is true of **execution accuracy**. When we only care that the output correctly addresses the provided question, execution accuracy is a better metric. When multiple correct answers exist, but we strictly prefer one (e.g. the most efficient query), then execution accuracy alone does not give enough fidelity in evaluation.

### Bonus
Do some open-ended exploration to try to improve your performance on this dataset as much as possible (whether for finetuning or prompting). No hard requirement on how much to improve (or to improve at all), but please discuss the ideas you tried + how effective they were in your report. 150-300 words.

1. For fine-tuning, changed learning rate scheduler from linear to cosine annealing.
	- Minorly improved test accuracy to 0.491 from 0.48
2. For few shot, increase the number of provided prompts from 4 to 5.
	1. baseline: 0.35018050541516244
---
##### finetuned
where is the most populated area of new mexico
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "new mexico" ) AND CITYalias0.STATE_NAME = "new mexico" ;
[('alaska',)]
[('albuquerque',)]

Failed: near "COUNT": syntax error
Failed: near "COUNT": syntax error
Failed: near "COUNT": syntax error
what is the population of washington
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "washington" ;
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "washington" ;
[(638333,)]
[(4113200,)]

Failed: no such column: STATEalias0.LOWEST_POINT
tell me what cities are in texas
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "texas" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.STATE_NAME = "texas" ;
[('houston',), ('dallas',), ('san antonio',), ('el paso',), ('fort worth',), ('austin',), ('corpus christi',), ('lubbock',), ('arlington',)]
[('houston',), ('dallas',), ('san antonio',), ('el paso',), ('fort worth',), ('austin',), ('corpus christi',), ('lubbock',), ('arlington',), ('amarillo',), ('garland',), ('beaumont',), ('pasadena',), ('irving',), ('waco',), ('abilene',), ('wichita falls',), ('laredo',), ('odessa',), ('brownsville',), ('san angelo',), ('richardson',), ('plano',), ('grand prairie',), ('midland',), ('tyler',), ('mesquite',), ('mcallen',), ('longview',), ('port arthur',)]

which states border the missouri river
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "missouri" ;
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "missouri" ;
[('iowa',), ('illinois',), ('kentucky',), ('tennessee',), ('arkansas',), ('oklahoma',), ('kansas',), ('nebraska',)]
[('montana',), ('north dakota',), ('south dakota',), ('iowa',), ('nebraska',), ('missouri',)]

what is the most populous state
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
[('alaska',)]
[('california',)]

what state is the largest in population
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
[('alaska',)]
[('california',)]

how long is the longest river in the usa
SELECT DISTINCT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "usa" ;
SELECT DISTINCT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 ) ;
[]
[(3968,)]

Failed: near "RIVERalias0": syntax error
give me the number of rivers in california
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "california" ;
SELECT COUNT( RIVERalias0.RIVER_NAME ) FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "california" ;
[('colorado',)]
[(1,)]

Failed: near "COUNT": syntax error
what states surround kentucky
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "kentucky" ;
[('alaska',)]
[('indiana',), ('ohio',), ('west virginia',), ('virginia',), ('tennessee',), ('missouri',), ('illinois',)]

Failed: near "RIVERalias0": syntax error
san antonio is in what state
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "san antonio" ;
[('alaska',)]
[('texas',)]

what states have cities named salt lake city
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "salt lake" ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "salt lake city" ;
[]
[('utah',)]

which states does the longest river run through
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "longest river" ;
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 ) ;
[]
[('montana',), ('north dakota',), ('south dakota',), ('iowa',), ('nebraska',), ('missouri',)]

how tall is the highest point in montana
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "montana" ;
SELECT HIGHLOWalias0.HIGHEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "montana" ;
[('granite peak',)]
[(3901,)]

what is the highest point in nevada in meters
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "nevada" ;
SELECT HIGHLOWalias0.HIGHEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "nevada" ;
[('boundary peak',)]
[(4005,)]

which is the longest river in usa
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "usa" ) AND RIVERalias0.TRAVERSE = "usa" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 ) ;
[]
[('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',)]

what is the highest point in states bordering georgia
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "georgia" ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "georgia" ) ORDER BY HIGHLOWalias0.HIGHEST_ELEVATION DESC LIMIT 1 ;
[('brasstown bald',)]
[('mount mitchell',)]

what is the highest point in the states bordering colorado
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "colorado" ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "colorado" ) ORDER BY HIGHLOWalias0.HIGHEST_ELEVATION DESC LIMIT 1 ;
[('mount elbert',)]
[('gannett peak',)]

count the states which have elevations lower than what alabama has
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT COUNT( HIGHLOWalias0.STATE_NAME ) FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.LOWEST_ELEVATION < ( SELECT HIGHLOWalias1.LOWEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias1 WHERE HIGHLOWalias1.STATE_NAME = "alabama" ) ;
[('alaska',)]
[(2,)]

how high is mount mckinley
SELECT HIGHLOWalias0.HIGHEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "mckinley" ;
SELECT HIGHLOWalias0.HIGHEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_POINT = "mount mckinley" ;
[]
[(6194,)]

what is the maximum elevation of san francisco
SELECT MAX( HIGHLOWalias0.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias0 ;
SELECT HIGHLOWalias0.HIGHEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_POINT = "san francisco" ;
[(6194,)]
[]

Failed: near "HIGHLOWalias0": syntax error
what is the highest elevation in the united states
SELECT HIGHLOWalias0.HIGHEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "united states" ;
SELECT MAX( HIGHLOWalias0.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias0 ;
[]
[(6194,)]

Failed: near "DDL": syntax error
Failed: near "DISTINCT": syntax error
what is the length of the mississippi river
SELECT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "mississippi" ;
SELECT DISTINCT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "mississippi" ;
[(3778,), (3778,), (3778,), (3778,), (3778,), (3778,), (3778,), (3778,), (3778,), (3778,)]
[(3778,)]

Failed: near "DISTINCT": syntax error
what is the length of the longest river that runs through texas
SELECT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "texas" ;
SELECT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "texas" ) AND RIVERalias0.TRAVERSE = "texas" ;
[]
[(3033,)]

Failed: no such column: CITYalias0.CAPITAL
Failed: near "COUNT": syntax error
how many citizens does the biggest city have in the usa
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "usa" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
[]
[(7071639,)]

Failed: near "COUNT": syntax error
what is the population of erie pennsylvania
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "erie" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "erie" AND CITYalias0.STATE_NAME = "pennsylvania" ;
[]
[(119123,)]

what is the population of tempe arizona
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "tempe arizona" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "tempe" AND CITYalias0.STATE_NAME = "arizona" ;
[]
[(106919,)]

Failed: near "COUNT": syntax error
how many people live in the united states
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "united states" ;
SELECT SUM( STATEalias0.POPULATION ) FROM STATE AS STATEalias0 ;
[]
[(225195124,)]

Failed: near "COUNT": syntax error
how many states are in the usa
SELECT COUNT( STATEalias0.STATE_NAME ) FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT COUNT( STATEalias0.STATE_NAME ) FROM STATE AS STATEalias0 ;
[(1,)]
[(51,)]

how many states are there
SELECT COUNT( STATEalias0.STATE_NAME ) FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT COUNT( STATEalias0.STATE_NAME ) FROM STATE AS STATEalias0 ;
[(1,)]
[(51,)]

how many states are there in the usa
SELECT COUNT( STATEalias0.STATE_NAME ) FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT COUNT( STATEalias0.STATE_NAME ) FROM STATE AS STATEalias0 ;
[(1,)]
[(51,)]

how many states does usa have
SELECT COUNT( STATEalias0.STATE_NAME ) FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT COUNT( STATEalias0.STATE_NAME ) FROM STATE AS STATEalias0 ;
[(1,)]
[(51,)]

iowa borders how many states
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "iowa" ;
SELECT COUNT( BORDER_INFOalias0.BORDER ) FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "iowa" ;
[('minnesota',), ('wisconsin',), ('illinois',), ('missouri',), ('nebraska',), ('south dakota',)]
[(6,)]

how many states do not have rivers
SELECT COUNT( DISTINCT RIVERalias0.TRAVERSE ) FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "not-rivers" ;
SELECT COUNT( DISTINCT STATEalias0.STATE_NAME ) FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME NOT IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 ) ;
[(0,)]
[(4,)]

how many states have a higher point than the highest point of the state with the largest capital city in the us
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION = ( SELECT MAX( HIGHLOWalias1.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
SELECT COUNT( HIGHLOWalias0.STATE_NAME ) FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION > ( SELECT HIGHLOWalias1.HIGHEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias1 WHERE HIGHLOWalias1.STATE_NAME = ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = ( SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ) ) ) ;
[('alaska',)]
[(0,)]

name the major rivers in florida
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "florida" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH > 750 AND RIVERalias0.TRAVERSE = "florida" ;
[('chattahoochee',)]
[]

through which states does the longest river in texas run
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "texas" ;
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "texas" ) ;
[]
[('colorado',), ('new mexico',), ('texas',)]

what are the capitals of states that border missouri
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "missouri" ;
SELECT STATEalias0.CAPITAL FROM BORDER_INFO AS BORDER_INFOalias0 , STATE AS STATEalias0 WHERE BORDER_INFOalias0.STATE_NAME = "missouri" AND STATEalias0.STATE_NAME = BORDER_INFOalias0.BORDER ;
[('jefferson city',)]
[('des moines',), ('springfield',), ('frankfort',), ('nashville',), ('little rock',), ('oklahoma city',), ('topeka',), ('lincoln',)]

what are the cities in states through which the mississippi runs
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "mississippi" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "mississippi" ) ;
[('jackson',)]
[('little rock',), ('fort smith',), ('north little rock',), ('chicago',), ('rockford',), ('peoria',), ('springfield',), ('decatur',), ('aurora',), ('joliet',), ('evanston',), ('waukegan',), ('arlington heights',), ('elgin',), ('cicero',), ('oak lawn',), ('skokie',), ('champaign',), ('des moines',), ('cedar rapids',), ('davenport',), ('sioux city',), ('waterloo',), ('dubuque',), ('louisville',), ('lexington',), ('new orleans',), ('baton rouge',), ('shreveport',), ('metairie',), ('lafayette',), ('lake charles',), ('kenner',), ('monroe',), ('minneapolis',), ('st. paul',), ('duluth',), ('bloomington',), ('rochester',), ('jackson',), ('st. louis',), ('kansas city',), ('springfield',), ('independence',), ('st. joseph',), ('columbia',), ('memphis',), ('nashville',), ('knoxville',), ('chattanooga',), ('milwaukee',), ('madison',), ('green bay',), ('racine',), ('kenosha',), ('west allis',), ('appleton',)]

Failed: incomplete input
what are the highest points of all the states
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "maine" ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 ;
[('mount katahdin',)]
[('cheaha mountain',), ('mount mckinley',), ('humphreys peak',), ('magazine mountain',), ('mount whitney',), ('mount elbert',), ('mount frissell',), ('centerville',), ('tenleytown',), ('walton county',), ('brasstown bald',), ('mauna kea',), ('borah peak',), ('charles mound',), ('franklin township',), ('ocheyedan mound',), ('mount sunflower',), ('black mountain',), ('driskill mountain',), ('mount katahdin',), ('backbone mountain',), ('mount greylock',), ('mount curwood',), ('eagle mountain',), ('woodall mountain',), ('taum sauk mountain',), ('granite peak',), ('johnson township',), ('boundary peak',), ('mount washington',), ('high point',), ('wheeler peak',), ('mount marcy',), ('mount mitchell',), ('white butte',), ('campbell hill',), ('black mesa',), ('mount hood',), ('mount davis',), ('jerimoth hill',), ('sassafras mountain',), ('harney peak',), ('clingmans dome',), ('guadalupe peak',), ('kings peak',), ('mount mansfield',), ('mount rogers',), ('mount rainier',), ('spruce knob',), ('timms hill',), ('gannett peak',)]

what major cities are located in pennsylvania
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "pennsylvania" ) AND CITYalias0.STATE_NAME = "pennsylvania" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "pennsylvania" ;
[('philadelphia',)]
[('philadelphia',), ('pittsburgh',)]

what are the major cities in states through which the mississippi runs
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "mississippi" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH > 750 AND RIVERalias0.RIVER_NAME = "mississippi" ) ;
[('jackson',)]
[('little rock',), ('chicago',), ('des moines',), ('louisville',), ('lexington',), ('new orleans',), ('baton rouge',), ('shreveport',), ('metairie',), ('minneapolis',), ('st. paul',), ('jackson',), ('st. louis',), ('kansas city',), ('memphis',), ('nashville',), ('knoxville',), ('chattanooga',), ('milwaukee',), ('madison',)]

what are the major cities in the usa
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "usa" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 ;
[]
[('birmingham',), ('mobile',), ('montgomery',), ('anchorage',), ('phoenix',), ('tucson',), ('mesa',), ('little rock',), ('los angeles',), ('san diego',), ('san francisco',), ('san jose',), ('long beach',), ('oakland',), ('sacramento',), ('anaheim',), ('fresno',), ('santa ana',), ('riverside',), ('huntington beach',), ('denver',), ('colorado springs',), ('aurora',), ('washington',), ('jacksonville',), ('miami',), ('tampa',), ('st. petersburg',), ('fort lauderdale',), ('atlanta',), ('columbus',), ('honolulu',), ('ewa',), ('chicago',), ('indianapolis',), ('fort wayne',), ('gary',), ('des moines',), ('wichita',), ('kansas city',), ('louisville',), ('lexington',), ('new orleans',), ('baton rouge',), ('shreveport',), ('metairie',), ('baltimore',), ('boston',), ('worcester',), ('springfield',), ('detroit',), ('grand rapids',), ('warren',), ('flint',), ('minneapolis',), ('st. paul',), ('jackson',), ('st. louis',), ('kansas city',), ('omaha',), ('lincoln',), ('las vegas',), ('newark',), ('jersey city',), ('albuquerque',), ('new york',), ('buffalo',), ('rochester',), ('yonkers',), ('syracuse',), ('charlotte',), ('greensboro',), ('cleveland',), ('columbus',), ('cincinnati',), ('toledo',), ('akron',), ('dayton',), ('oklahoma city',), ('tulsa',), ('portland',), ('philadelphia',), ('pittsburgh',), ('providence',), ('memphis',), ('nashville',), ('knoxville',), ('chattanooga',), ('houston',), ('dallas',), ('san antonio',), ('el paso',), ('fort worth',), ('austin',), ('corpus christi',), ('lubbock',), ('arlington',), ('salt lake city',), ('norfolk',), ('virginia beach',), ('richmond',), ('arlington',), ('seattle',), ('spokane',), ('tacoma',), ('milwaukee',), ('madison',)]

what are the population densities of each us state
SELECT STATEalias0.DENSITY FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.DENSITY FROM STATE AS STATEalias0 ;
[(149.81012658227849,)]
[(75.31914893617021,), (0.6798646362098139,), (23.842105263157894,), (42.96992481203007,), (149.81012658227849,), (27.778846153846153,), (618.9243027888447,), (290.60665362035223,), (580.0,), (141.9375509728533,), (92.75042444821732,), (148.97233812393756,), (11.373493975903614,), (202.4866785079929,), (151.65745856353593,), (51.740674955595026,), (28.724179829890645,), (28.724179829890645,), (88.17610062893081,), (33.81932962573275,), (403.1548757170172,), (692.5398358281024,), (158.32478632478632,), (48.29383886255924,), (52.83018867924528,), (70.53084648493544,), (5.351700680272109,), (20.297542043984475,), (7.244343891402715,), (99.21327729281172,), (945.8071144214717,), (10.71546052631579,), (357.5967413441955,), (111.67647617239415,), (9.231966053748232,), (261.50121065375305,), (43.24517512508935,), (27.12391705211542,), (261.8301403725611,), (781.5181518151816,), (100.3374795101726,), (8.957505576015354,), (108.94636924537257,), (53.33068472716233,), (17.208480565371026,), (53.203661327231124,), (131.1776251226693,), (60.36484245439469,), (80.57851239669421,), (83.69989136822609,), (4.8007545317915525,)]

what are the populations of states through which the mississippi river run
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "mississippi" ;
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "mississippi" ) ;
[(2520000,)]
[(2286000,), (11400000,), (2913000,), (2364000,), (4206000,), (4076000,), (2520000,), (4916000,), (4591000,), (4700000,)]

what are the populations of states through which the mississippi runs
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "mississippi" ;
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "mississippi" ) ;
[(2520000,)]
[(2286000,), (11400000,), (2913000,), (2364000,), (4206000,), (4076000,), (2520000,), (4916000,), (4591000,), (4700000,)]

what are the populations of states which border texas
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "texas" ;
SELECT STATEalias0.POPULATION FROM BORDER_INFO AS BORDER_INFOalias0 , STATE AS STATEalias0 WHERE BORDER_INFOalias0.STATE_NAME = "texas" AND STATEalias0.STATE_NAME = BORDER_INFOalias0.BORDER ;
[(14229000,)]
[(3025000,), (2286000,), (4206000,), (1303000,)]

what are the populations of the major cities of texas
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "texas" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "texas" ;
[]
[(1595138,), (904078,), (785880,), (425259,), (385164,), (345496,), (231999,), (173979,), (160123,)]

what city has the most people
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "california" ) AND CITYalias0.STATE_NAME = "california" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
[('los angeles',)]
[('new york',)]

what city in the united states has the highest population
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "united states" ) AND CITYalias0.STATE_NAME = "united states" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
[]
[('new york',)]

what is the most populous city
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "california" ) AND CITYalias0.STATE_NAME = "california" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
[('los angeles',)]
[('new york',)]

which us city has the highest population
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "us" ) AND CITYalias0.STATE_NAME = "us" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
[]
[('new york',)]

Failed: no such column: STATEalias0.LOWEST_ELEVATION
Failed: incomplete input
what is the biggest capital city in the us
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "us" ) AND CITYalias0.STATE_NAME = "us" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 , STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = CITYalias1.CITY_NAME ) ;
[]
[('phoenix',)]

what is the largest capital city in the usa
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "usa" ) AND CITYalias0.STATE_NAME = "usa" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 , STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = CITYalias1.CITY_NAME ) ;
[]
[('phoenix',)]

what is the capital of states that have cities named durham
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "durham" ;
SELECT STATEalias0.CAPITAL FROM CITY AS CITYalias0 , STATE AS STATEalias0 WHERE CITYalias0.CITY_NAME = "durham" AND STATEalias0.STATE_NAME = CITYalias0.STATE_NAME ;
[]
[('raleigh',)]

what is the capital of the state with the most inhabitants
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
[('juneau',)]
[('sacramento',)]

Failed: no such column: STATEalias0.LENGTH
Failed: no such table: DENSITY
what is the highest mountain in the us
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "us" ;
SELECT MOUNTAINalias0.MOUNTAIN_NAME FROM MOUNTAIN AS MOUNTAINalias0 WHERE MOUNTAINalias0.MOUNTAIN_ALTITUDE = ( SELECT MAX( MOUNTAINalias1.MOUNTAIN_ALTITUDE ) FROM MOUNTAIN AS MOUNTAINalias1 ) ;
[]
[('mckinley',)]

what is the highest mountain in us
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "us" ;
SELECT MOUNTAINalias0.MOUNTAIN_NAME FROM MOUNTAIN AS MOUNTAINalias0 WHERE MOUNTAINalias0.MOUNTAIN_ALTITUDE = ( SELECT MAX( MOUNTAINalias1.MOUNTAIN_ALTITUDE ) FROM MOUNTAIN AS MOUNTAINalias1 ) ;
[]
[('mckinley',)]

what is the highest point in the state with capital austin
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "austin" ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME IN ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = "austin" ) ;
[]
[('guadalupe peak',)]

what is the highest point in the usa
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "usa" ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION = ( SELECT MAX( HIGHLOWalias1.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
[]
[('mount mckinley',)]

what is the highest point of the usa
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "usa" ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION = ( SELECT MAX( HIGHLOWalias1.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
[]
[('mount mckinley',)]

what is the highest point of the state with the smallest population density
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "maine" ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME IN ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.DENSITY = ( SELECT MIN( STATEalias1.DENSITY ) FROM STATE AS STATEalias1 ) ) ;
[('mount katahdin',)]
[('mount mckinley',)]

Failed: incomplete input
Failed: incomplete input
what is the largest state bordering arkansas
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 WHERE STATEalias1.STATE_NAME IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "arkansas" ) ) AND STATEalias0.STATE_NAME IN ( SELECT BORDER_INFOalias1.BORDER FROM BORDER_INFO AS BORDER_INFOalias1 WHERE BORDER_INFOalias1.STATE_NAME = "arkansas" ) ;
[('alaska',)]
[('texas',)]

what is the largest state that borders texas
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 WHERE STATEalias1.STATE_NAME IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "texas" ) ) AND STATEalias0.STATE_NAME IN ( SELECT BORDER_INFOalias1.BORDER FROM BORDER_INFO AS BORDER_INFOalias1 WHERE BORDER_INFOalias1.STATE_NAME = "texas" ) ;
[('alaska',)]
[('new mexico',)]

what is the length of the river that flows through the most states
SELECT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "rivers" ;
SELECT DISTINCT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = ( SELECT RIVER_NAME FROM ( SELECT COUNT( 1 ) AS DERIVED_FIELDalias0 , RIVERalias1.RIVER_NAME FROM RIVER AS RIVERalias1 GROUP BY RIVERalias1.RIVER_NAME ) AS DERIVED_TABLEalias0 WHERE DERIVED_TABLEalias0.DERIVED_FIELDalias0 = ( SELECT MAX( DERIVED_TABLEalias1.DERIVED_FIELDalias1 ) FROM ( SELECT COUNT( 1 ) AS DERIVED_FIELDalias1 , RIVERalias2.RIVER_NAME FROM RIVER AS RIVERalias2 GROUP BY RIVERalias2.RIVER_NAME ) AS DERIVED_TABLEalias1 ) ) ;
[]
[(3778,)]

what is the length of the river that runs through the most states
SELECT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "rivers" ;
SELECT DISTINCT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = ( SELECT RIVER_NAME FROM ( SELECT COUNT( 1 ) AS DERIVED_FIELDalias0 , RIVERalias1.RIVER_NAME FROM RIVER AS RIVERalias1 GROUP BY RIVERalias1.RIVER_NAME ) AS DERIVED_TABLEalias0 WHERE DERIVED_TABLEalias0.DERIVED_FIELDalias0 = ( SELECT MAX( DERIVED_TABLEalias1.DERIVED_FIELDalias1 ) FROM ( SELECT COUNT( 1 ) AS DERIVED_FIELDalias1 , RIVERalias2.RIVER_NAME FROM RIVER AS RIVERalias2 GROUP BY RIVERalias2.RIVER_NAME ) AS DERIVED_TABLEalias1 ) ) ;
[]
[(3778,)]

what is the longest river in the states that border nebraska
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "nebraska" ) AND RIVERalias0.TRAVERSE = "nebraska" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "nebraska" ) ) AND RIVERalias0.TRAVERSE IN ( SELECT BORDER_INFOalias1.BORDER FROM BORDER_INFO AS BORDER_INFOalias1 WHERE BORDER_INFOalias1.STATE_NAME = "nebraska" ) ;
[('missouri',)]
[('missouri',), ('missouri',), ('missouri',)]

what is the longest river that flows through a state that borders indiana
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "indiana" ) AND RIVERalias0.TRAVERSE = "indiana" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "indiana" ) ) AND RIVERalias0.TRAVERSE IN ( SELECT BORDER_INFOalias1.BORDER FROM BORDER_INFO AS BORDER_INFOalias1 WHERE BORDER_INFOalias1.STATE_NAME = "indiana" ) ;
[('ohio',)]
[('mississippi',), ('mississippi',)]

what is the longest river in the state with the most major cities
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "texas" ) AND RIVERalias0.TRAVERSE = "texas" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = ( SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 GROUP BY CITYalias0.STATE_NAME ORDER BY COUNT( CITYalias0.CITY_NAME ) DESC LIMIT 1 ) ORDER BY RIVERalias0.LENGTH DESC LIMIT 1 ;
[('rio grande',)]
[('colorado',)]

what is the lowest point in usa
SELECT HIGHLOWalias0.LOWEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "usa" ;
SELECT HIGHLOWalias0.LOWEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.LOWEST_ELEVATION = ( SELECT MIN( HIGHLOWalias1.LOWEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
[]
[('death valley',)]

what is the lowest point of all states through which the colorado river runs through
SELECT HIGHLOWalias0.LOWEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "colorado" ;
SELECT HIGHLOWalias0.LOWEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "colorado" ) ORDER BY HIGHLOWalias0.LOWEST_ELEVATION LIMIT 1 ;
[('arkansas river',)]
[('death valley',)]

what is the most dense state in the usa
SELECT STATEalias0.DENSITY FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "usa" ;
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.DENSITY = ( SELECT MAX( STATEalias1.DENSITY ) FROM STATE AS STATEalias1 ) ;
[]
[('new jersey',)]

what is the most populous state through which the mississippi runs
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 WHERE STATEalias1.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "mississippi" ) ) AND STATEalias0.STATE_NAME IN ( SELECT RIVERalias1.TRAVERSE FROM RIVER AS RIVERalias1 WHERE RIVERalias1.RIVER_NAME = "mississippi" ) ;
[('alaska',)]
[('illinois',)]

what is the population of the largest city in the state with the largest area
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "maine" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME IN ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ) ) AND CITYalias0.STATE_NAME IN ( SELECT STATEalias2.STATE_NAME FROM STATE AS STATEalias2 WHERE STATEalias2.AREA = ( SELECT MAX( STATEalias3.AREA ) FROM STATE AS STATEalias3 ) ) ;
[]
[(174431,)]

what is the population of the state that borders the most states
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "maine" ;
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 GROUP BY BORDER_INFOalias0.BORDER HAVING COUNT( 1 ) = ( SELECT MAX( DERIVED_TABLEalias0.DERIVED_FIELDalias0 ) FROM ( SELECT BORDER_INFOalias1.BORDER , COUNT( 1 ) AS DERIVED_FIELDalias0 FROM BORDER_INFO AS BORDER_INFOalias1 GROUP BY BORDER_INFOalias1.BORDER ) AS DERIVED_TABLEalias0 ) ) ;
[(1125000,)]
[(4916000,), (4591000,)]

what is the smallest city in the usa
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MIN( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "usa" ) AND CITYalias0.STATE_NAME = "usa" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MIN( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
[]
[('scotts valley',)]

what is the smallest city in the us
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MIN( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "us" ) AND CITYalias0.STATE_NAME = "us" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MIN( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
[]
[('scotts valley',)]

what is the smallest state that borders the most states
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MIN( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MIN( STATEalias1.AREA ) FROM STATE AS STATEalias1 WHERE STATEalias1.STATE_NAME IN ( SELECT DERIVED_TABLEalias0.STATE_NAME FROM ( SELECT BORDER_INFOalias0.STATE_NAME , COUNT( DISTINCT BORDER_INFOalias0.BORDER ) AS DERIVED_FIELDalias0 FROM BORDER_INFO AS BORDER_INFOalias0 GROUP BY BORDER_INFOalias0.STATE_NAME ) AS DERIVED_TABLEalias0 WHERE DERIVED_TABLEalias0.DERIVED_FIELDalias0 = ( SELECT MAX( DERIVED_TABLEalias1.DERIVED_FIELDalias1 ) FROM ( SELECT BORDER_INFOalias1.STATE_NAME , COUNT( DISTINCT BORDER_INFOalias1.BORDER ) AS DERIVED_FIELDalias1 FROM BORDER_INFO AS BORDER_INFOalias1 GROUP BY BORDER_INFOalias1.STATE_NAME ) AS DERIVED_TABLEalias1 ) ) ) ;
[('district of columbia',)]
[('tennessee',)]

what is the smallest state bordering wyoming
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MIN( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MIN( STATEalias1.AREA ) FROM STATE AS STATEalias1 WHERE STATEalias1.STATE_NAME IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "wyoming" ) ) AND STATEalias0.STATE_NAME IN ( SELECT BORDER_INFOalias1.BORDER FROM BORDER_INFO AS BORDER_INFOalias1 WHERE BORDER_INFOalias1.STATE_NAME = "wyoming" ) ;
[('district of columbia',)]
[('south dakota',)]

what is the smallest state that the mississippi river runs through
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MIN( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MIN( STATEalias1.AREA ) FROM STATE AS STATEalias1 WHERE STATEalias1.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "mississippi" ) ) AND STATEalias0.STATE_NAME IN ( SELECT RIVERalias1.TRAVERSE FROM RIVER AS RIVERalias1 WHERE RIVERalias1.RIVER_NAME = "mississippi" ) ;
[('district of columbia',)]
[('tennessee',)]

what is the total length of all rivers in the usa
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "usa" ) AND RIVERalias0.TRAVERSE = "usa" ;
SELECT SUM( DERIVED_TABLEalias0.LENGTH ) FROM ( SELECT DISTINCT RIVERalias0.RIVER_NAME , RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 ) AS DERIVED_TABLEalias0 ;
[]
[(51393,)]

what river flows through the most states
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "texas" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 GROUP BY ( RIVERalias0.RIVER_NAME ) ORDER BY COUNT( DISTINCT RIVERalias0.TRAVERSE ) DESC LIMIT 1 ;
[('red',), ('canadian',), ('rio grande',), ('pecos',), ('washita',)]
[('mississippi',)]

which river goes through the most states
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "texas" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 GROUP BY ( RIVERalias0.RIVER_NAME ) ORDER BY COUNT( DISTINCT RIVERalias0.TRAVERSE ) DESC LIMIT 1 ;
[('red',), ('canadian',), ('rio grande',), ('pecos',), ('washita',)]
[('mississippi',)]

which river runs through most states
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "most states" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 GROUP BY ( RIVERalias0.RIVER_NAME ) ORDER BY COUNT( DISTINCT RIVERalias0.TRAVERSE ) DESC LIMIT 1 ;
[]
[('mississippi',)]

which river traverses most states
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "most states" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 GROUP BY ( RIVERalias0.RIVER_NAME ) ORDER BY COUNT( DISTINCT RIVERalias0.TRAVERSE ) DESC LIMIT 1 ;
[]
[('mississippi',)]

what river runs through the state with the most cities
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "texas" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE IN ( SELECT DERIVED_TABLEalias0.STATE_NAME FROM ( SELECT CITYalias0.STATE_NAME , COUNT( 1 ) AS DERIVED_FIELDalias0 FROM CITY AS CITYalias0 GROUP BY CITYalias0.STATE_NAME ) AS DERIVED_TABLEalias0 WHERE DERIVED_TABLEalias0.DERIVED_FIELDalias0 = ( SELECT MAX( DERIVED_TABLEalias1.DERIVED_FIELDalias1 ) FROM ( SELECT COUNT( 1 ) AS DERIVED_FIELDalias1 FROM CITY AS CITYalias1 GROUP BY CITYalias1.STATE_NAME ) AS DERIVED_TABLEalias1 ) ) ;
[('red',), ('canadian',), ('rio grande',), ('pecos',), ('washita',)]
[('colorado',)]

what rivers are in states that border texas
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "texas" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "texas" ) ;
[('red',), ('canadian',), ('rio grande',), ('pecos',), ('washita',)]
[('mississippi',), ('mississippi',), ('red',), ('red',), ('red',), ('red',), ('arkansas',), ('arkansas',), ('canadian',), ('canadian',), ('cimarron',), ('cimarron',), ('rio grande',), ('san juan',), ('gila',), ('neosho',), ('ouachita',), ('ouachita',), ('pearl',), ('pecos',), ('st. francis',), ('washita',), ('white',)]

what rivers traverses the state which borders the most states
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "texas" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 GROUP BY BORDER_INFOalias0.BORDER HAVING COUNT( 1 ) = ( SELECT MAX( DERIVED_TABLEalias0.DERIVED_FIELDalias0 ) FROM ( SELECT BORDER_INFOalias1.BORDER , COUNT( 1 ) AS DERIVED_FIELDalias0 FROM BORDER_INFO AS BORDER_INFOalias1 GROUP BY BORDER_INFOalias1.BORDER ) AS DERIVED_TABLEalias0 ) ) ;
[('red',), ('canadian',), ('rio grande',), ('pecos',), ('washita',)]
[('mississippi',), ('mississippi',), ('missouri',), ('tennessee',), ('cumberland',), ('st. francis',), ('white',)]

what river traverses the state which borders the most states
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "texas" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 GROUP BY BORDER_INFOalias0.BORDER HAVING COUNT( 1 ) = ( SELECT MAX( DERIVED_TABLEalias0.DERIVED_FIELDalias0 ) FROM ( SELECT BORDER_INFOalias1.BORDER , COUNT( 1 ) AS DERIVED_FIELDalias0 FROM BORDER_INFO AS BORDER_INFOalias1 GROUP BY BORDER_INFOalias1.BORDER ) AS DERIVED_TABLEalias0 ) ) ;
[('red',), ('canadian',), ('rio grande',), ('pecos',), ('washita',)]
[('mississippi',), ('mississippi',), ('missouri',), ('tennessee',), ('cumberland',), ('st. francis',), ('white',)]

which of the states bordering pennsylvania has the largest population
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "pennsylvania" ) ORDER BY STATEalias0.POPULATION DESC LIMIT 1 ;
[('california',)]
[('new york',)]

what state contains the highest point of those the colorado river traverses
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION = ( SELECT MAX( HIGHLOWalias1.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION = ( SELECT MAX( HIGHLOWalias1.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 WHERE HIGHLOWalias1.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "colorado" ) ) ;
[('alaska',)]
[('california',)]

what state has the largest capital
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = ( SELECT MAX( STATEalias1.CAPITAL ) FROM STATE AS STATEalias1 ) ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 , STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = CITYalias1.CITY_NAME ) ;
[('district of columbia',)]
[('arizona',)]

which state 's capital city is the largest
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "new york" ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 , STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = CITYalias1.CITY_NAME ) ;
[('new york',)]
[('arizona',)]

Failed: incomplete input
what state has the most major cities
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "california" ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 GROUP BY CITYalias0.STATE_NAME ORDER BY COUNT( 1 ) DESC LIMIT 1 ;
[]
[('california',)]

which state has the most major cities
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "california" ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 GROUP BY CITYalias0.STATE_NAME ORDER BY COUNT( 1 ) DESC LIMIT 1 ;
[]
[('california',)]

what state has the smallest urban population
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MIN( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 GROUP BY CITYalias0.STATE_NAME ORDER BY SUM( CITYalias0.POPULATION ) LIMIT 1 ;
[('alaska',)]
[('wyoming',)]

what states border states that border mississippi
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "mississippi" ;
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT BORDER_INFOalias1.BORDER FROM BORDER_INFO AS BORDER_INFOalias1 WHERE BORDER_INFOalias1.STATE_NAME = "mississippi" ) ;
[('tennessee',), ('alabama',), ('louisiana',), ('arkansas',)]
[('tennessee',), ('georgia',), ('florida',), ('mississippi',), ('missouri',), ('tennessee',), ('mississippi',), ('louisiana',), ('texas',), ('oklahoma',), ('arkansas',), ('mississippi',), ('texas',), ('kentucky',), ('virginia',), ('north carolina',), ('georgia',), ('alabama',), ('mississippi',), ('arkansas',), ('missouri',)]

what states border states that the ohio runs through
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "ohio" ;
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "ohio" ) ;
[('michigan',), ('pennsylvania',), ('west virginia',), ('kentucky',), ('indiana',)]
[('wisconsin',), ('indiana',), ('kentucky',), ('missouri',), ('iowa',), ('michigan',), ('ohio',), ('kentucky',), ('illinois',), ('indiana',), ('ohio',), ('west virginia',), ('virginia',), ('tennessee',), ('missouri',), ('illinois',), ('michigan',), ('pennsylvania',), ('west virginia',), ('kentucky',), ('indiana',), ('new york',), ('new jersey',), ('delaware',), ('maryland',), ('west virginia',), ('ohio',), ('pennsylvania',), ('maryland',), ('virginia',), ('kentucky',), ('ohio',)]

what states border texas and have a major river
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "texas" ;
SELECT BORDER_INFOalias0.STATE_NAME FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.BORDER = "texas" AND BORDER_INFOalias0.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH > 750 ) ;
[('oklahoma',), ('arkansas',), ('louisiana',), ('new mexico',)]
[('arkansas',), ('louisiana',), ('new mexico',), ('oklahoma',)]

what states border the most populous state
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "maine" ;
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ) ;
[('new hampshire',)]
[('oregon',), ('nevada',), ('arizona',)]

Failed: incomplete input
what states border the state with the most cities
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = "california" ) ;
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT DERIVED_TABLEalias0.STATE_NAME FROM ( SELECT CITYalias0.STATE_NAME , COUNT( 1 ) AS DERIVED_FIELDalias0 FROM CITY AS CITYalias0 GROUP BY CITYalias0.STATE_NAME ) AS DERIVED_TABLEalias0 WHERE DERIVED_TABLEalias0.DERIVED_FIELDalias0 = ( SELECT MAX( DERIVED_TABLEalias1.DERIVED_FIELDalias1 ) FROM ( SELECT COUNT( 1 ) AS DERIVED_FIELDalias1 FROM CITY AS CITYalias1 GROUP BY CITYalias1.STATE_NAME ) AS DERIVED_TABLEalias1 ) ) ;
[]
[('oregon',), ('nevada',), ('arizona',)]

what states border the state with the most major cities
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ) ;
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT DERIVED_TABLEalias0.STATE_NAME FROM ( SELECT CITYalias0.STATE_NAME , COUNT( 1 ) AS DERIVED_FIELDalias0 FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 GROUP BY CITYalias0.STATE_NAME ) AS DERIVED_TABLEalias0 WHERE DERIVED_TABLEalias0.DERIVED_FIELDalias0 = ( SELECT MAX( DERIVED_TABLEalias1.DERIVED_FIELDalias1 ) FROM ( SELECT COUNT( 1 ) AS DERIVED_FIELDalias1 FROM CITY AS CITYalias1 WHERE CITYalias1.POPULATION > 150000 GROUP BY CITYalias1.STATE_NAME ) AS DERIVED_TABLEalias1 ) ) ;
[]
[('oregon',), ('nevada',), ('arizona',)]

what states contain at least one major rivers
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "rivers" ;
SELECT DISTINCT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH > 750 ;
[]
[('minnesota',), ('wisconsin',), ('iowa',), ('illinois',), ('missouri',), ('kentucky',), ('tennessee',), ('arkansas',), ('mississippi',), ('louisiana',), ('montana',), ('north dakota',), ('south dakota',), ('nebraska',), ('colorado',), ('utah',), ('arizona',), ('nevada',), ('california',), ('pennsylvania',), ('west virginia',), ('indiana',), ('ohio',), ('new mexico',), ('texas',), ('oklahoma',), ('kansas',), ('wyoming',), ('idaho',), ('oregon',), ('washington',), ('alabama',), ('michigan',)]

where are mountains
SELECT MOUNTAINalias0.MOUNTAIN_NAME FROM MOUNTAIN AS MOUNTAINalias0 WHERE MOUNTAINalias0.MOUNTAIN_ALTITUDE = ( SELECT MAX( MOUNTAINalias1.MOUNTAIN_ALTITUDE ) FROM MOUNTAIN AS MOUNTAINalias1 ) ;
SELECT MOUNTAINalias0.STATE_NAME FROM MOUNTAIN AS MOUNTAINalias0 ;
[('mckinley',)]
[('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('washington',)]

where is the highest mountain of the united states
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "united states" ;
SELECT MOUNTAINalias0.STATE_NAME FROM MOUNTAIN AS MOUNTAINalias0 WHERE MOUNTAINalias0.MOUNTAIN_ALTITUDE = ( SELECT MAX( MOUNTAINalias1.MOUNTAIN_ALTITUDE ) FROM MOUNTAIN AS MOUNTAINalias1 ) ;
[]
[('alaska',)]

where is the smallest city
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MIN( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "smallest city" ) AND CITYalias0.STATE_NAME = "smallest city" ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MIN( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
[]
[('california',)]

which is the density of the state that the largest river in the united states runs through
SELECT STATEalias0.DENSITY FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "united states" ;
SELECT STATEalias0.DENSITY FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 ) ) ;
[]
[(51.740674955595026,), (70.53084648493544,), (5.351700680272109,), (20.297542043984475,), (9.231966053748232,), (8.957505576015354,)]

which is the highest peak not in alaska
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "alaska" ;
SELECT MOUNTAINalias0.MOUNTAIN_NAME FROM MOUNTAIN AS MOUNTAINalias0 WHERE MOUNTAINalias0.MOUNTAIN_ALTITUDE = ( SELECT MAX( MOUNTAINalias1.MOUNTAIN_ALTITUDE ) FROM MOUNTAIN AS MOUNTAINalias1 WHERE MOUNTAINalias1.STATE_NAME <> "alaska" ) ;
[('mount mckinley',)]
[('whitney',)]

which rivers do not run through texas
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "texas" ;
SELECT DISTINCT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME NOT IN ( SELECT RIVERalias1.RIVER_NAME FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "texas" ) ;
[('red',), ('canadian',), ('rio grande',), ('pecos',), ('washita',)]
[('mississippi',), ('missouri',), ('colorado',), ('ohio',), ('arkansas',), ('connecticut',), ('delaware',), ('little missouri',), ('snake',), ('chattahoochee',), ('cimarron',), ('green',), ('north platte',), ('potomac',), ('republican',), ('san juan',), ('tennessee',), ('wabash',), ('yellowstone',), ('allegheny',), ('bighorn',), ('cheyenne',), ('clark fork',), ('columbia',), ('cumberland',), ('dakota',), ('gila',), ('hudson',), ('neosho',), ('niobrara',), ('ouachita',), ('pearl',), ('powder',), ('roanoke',), ('rock',), ('smoky hill',), ('south platte',), ('st. francis',), ('tombigbee',), ('wateree catawba',), ('white',)]

which rivers run through states that border the state with the capital austin
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "austin" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = "austin" ) ) ;
[]
[('mississippi',), ('mississippi',), ('red',), ('red',), ('red',), ('red',), ('arkansas',), ('arkansas',), ('canadian',), ('canadian',), ('cimarron',), ('cimarron',), ('rio grande',), ('san juan',), ('gila',), ('neosho',), ('ouachita',), ('ouachita',), ('pearl',), ('pecos',), ('st. francis',), ('washita',), ('white',)]

which rivers run through states with fewest cities
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "states" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE IN ( SELECT DERIVED_TABLEalias0.STATE_NAME FROM ( SELECT CITYalias0.STATE_NAME , COUNT( 1 ) AS DERIVED_FIELDalias0 FROM CITY AS CITYalias0 GROUP BY CITYalias0.STATE_NAME ) AS DERIVED_TABLEalias0 WHERE DERIVED_TABLEalias0.DERIVED_FIELDalias0 = ( SELECT MIN( DERIVED_TABLEalias1.DERIVED_FIELDalias1 ) FROM ( SELECT COUNT( 1 ) AS DERIVED_FIELDalias1 FROM CITY AS CITYalias1 GROUP BY CITYalias1.STATE_NAME ) AS DERIVED_TABLEalias1 ) ) ;
[]
[('mississippi',), ('missouri',), ('missouri',), ('red',), ('canadian',), ('delaware',), ('little missouri',), ('little missouri',), ('little missouri',), ('snake',), ('snake',), ('cimarron',), ('green',), ('north platte',), ('potomac',), ('rio grande',), ('san juan',), ('yellowstone',), ('yellowstone',), ('bighorn',), ('cheyenne',), ('cheyenne',), ('clark fork',), ('dakota',), ('dakota',), ('gila',), ('niobrara',), ('pecos',), ('powder',), ('tombigbee',)]

which state capital has the smallest population
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MIN( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MIN( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 , STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = CITYalias1.CITY_NAME ) ;
[('alaska',)]
[('columbia',)]

which state has the lowest point that borders idaho
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.LOWEST_ELEVATION = ( SELECT MIN( HIGHLOWalias1.LOWEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.LOWEST_ELEVATION = ( SELECT MIN( HIGHLOWalias1.LOWEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 WHERE HIGHLOWalias1.STATE_NAME IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "idaho" ) ) AND HIGHLOWalias0.STATE_NAME IN ( SELECT BORDER_INFOalias1.BORDER FROM BORDER_INFO AS BORDER_INFOalias1 WHERE BORDER_INFOalias1.STATE_NAME = "idaho" ) ;
[('california',)]
[('oregon',), ('washington',)]

which state has the most major rivers
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "texas" ;
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH > 750 GROUP BY RIVERalias0.TRAVERSE ORDER BY COUNT( RIVERalias0.RIVER_NAME ) DESC LIMIT 1 ;
[]
[('colorado',)]

which state has the most major rivers running through it
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "texas" ;
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH > 750 GROUP BY RIVERalias0.TRAVERSE ORDER BY COUNT( RIVERalias0.RIVER_NAME ) DESC LIMIT 1 ;
[]
[('colorado',)]

which state has the smallest average urban population
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MIN( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 GROUP BY CITYalias0.STATE_NAME ORDER BY AVG ( CITYalias0.POPULATION ) LIMIT 1 ;
[('district of columbia',)]
[('wyoming',)]

which state is mount mckinley in
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME NOT IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "mckinley" ) ;
SELECT MOUNTAINalias0.STATE_NAME FROM MOUNTAIN AS MOUNTAINalias0 WHERE MOUNTAINalias0.MOUNTAIN_NAME = "mckinley" ;
[('alabama',), ('alaska',), ('arizona',), ('arkansas',), ('california',), ('colorado',), ('connecticut',), ('delaware',), ('district of columbia',), ('florida',), ('georgia',), ('hawaii',), ('idaho',), ('illinois',), ('indiana',), ('iowa',), ('kansas',), ('kentucky',), ('louisiana',), ('maine',), ('maryland',), ('massachusetts',), ('michigan',), ('minnesota',), ('mississippi',), ('missouri',), ('montana',), ('nebraska',), ('nevada',), ('new hampshire',), ('new jersey',), ('new mexico',), ('new york',), ('north carolina',), ('north dakota',), ('ohio',), ('oklahoma',), ('oregon',), ('pennsylvania',), ('rhode island',), ('south carolina',), ('south dakota',), ('tennessee',), ('texas',), ('utah',), ('vermont',), ('virginia',), ('washington',), ('west virginia',), ('wisconsin',), ('wyoming',)]
[('alaska',)]

which states have a river
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "rivers" ;
SELECT DISTINCT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 ;
[]
[('minnesota',), ('wisconsin',), ('iowa',), ('illinois',), ('missouri',), ('kentucky',), ('tennessee',), ('arkansas',), ('mississippi',), ('louisiana',), ('montana',), ('north dakota',), ('south dakota',), ('nebraska',), ('colorado',), ('utah',), ('arizona',), ('nevada',), ('california',), ('pennsylvania',), ('west virginia',), ('indiana',), ('ohio',), ('new mexico',), ('texas',), ('oklahoma',), ('kansas',), ('new hampshire',), ('vermont',), ('massachusetts',), ('connecticut',), ('new york',), ('new jersey',), ('delaware',), ('wyoming',), ('idaho',), ('oregon',), ('washington',), ('georgia',), ('florida',), ('maryland',), ('virginia',), ('district of columbia',), ('alabama',), ('michigan',), ('north carolina',), ('south carolina',)]

what state has the most rivers
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "rivers" ;
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 GROUP BY RIVERalias0.TRAVERSE ORDER BY COUNT( RIVERalias0.RIVER_NAME ) DESC LIMIT 1 ;
[]
[('colorado',)]

which state has the most rivers
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "texas" ;
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 GROUP BY RIVERalias0.TRAVERSE ORDER BY COUNT( RIVERalias0.RIVER_NAME ) DESC LIMIT 1 ;
[]
[('colorado',)]

finetuned execution acc: 0.48014440433212996

---
### fewshot

what is the biggest city in kansas
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "kansas" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "kansas" ) AND CITYalias0.STATE_NAME = "kansas" ;
[('wichita',), ('kansas city',)]
[('wichita',)]

what is the biggest city in louisiana
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.STATE_NAME = "louisiana" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "louisiana" ) AND CITYalias0.STATE_NAME = "louisiana" ;
[('new orleans',), ('baton rouge',), ('shreveport',), ('metairie',), ('lafayette',), ('lake charles',), ('kenner',), ('monroe',)]
[('new orleans',)]

what is the largest city in california
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "california" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "california" ) AND CITYalias0.STATE_NAME = "california" ;
[('los angeles',), ('san diego',), ('san francisco',), ('san jose',), ('long beach',), ('oakland',), ('sacramento',), ('anaheim',), ('fresno',), ('santa ana',), ('riverside',), ('huntington beach',)]
[('los angeles',)]

where is the most populated area of new mexico
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "new mexico" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "new mexico" ) AND CITYalias0.STATE_NAME = "new mexico" ;
[(1303000,)]
[('albuquerque',)]

which city in california has the largest population
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "california" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "california" ) AND CITYalias0.STATE_NAME = "california" ;
[('los angeles',), ('san diego',), ('san francisco',), ('san jose',), ('long beach',), ('oakland',), ('sacramento',), ('anaheim',), ('fresno',), ('santa ana',), ('riverside',), ('huntington beach',)]
[('los angeles',)]

how large is texas
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "texas" ) AND CITYalias0.STATE_NAME = "texas" ;
SELECT STATEalias0.AREA FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "texas" ;
[('houston',)]
[(266807.0,)]

Failed: no such table: AREA
Failed: no such table: AREA
Failed: no such column: CITYalias0.AIM
Failed: no such table: RIVERASRIVER
how many people reside in utah
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "utah" ;
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "utah" ;
[('utah',)]
[(1461000,)]

what are the population of mississippi
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "mississippi" ) ;
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "mississippi" ;
[('arkansas',), ('illinois',), ('iowa',), ('kentucky',), ('louisiana',), ('minnesota',), ('mississippi',), ('missouri',), ('tennessee',), ('wisconsin',)]
[(2520000,)]

what is the population of washington
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "washington" AND CITYalias0.STATE_NAME = "dc" ;
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "washington" ;
[]
[(4113200,)]

what states does the delaware river run through
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 GROUP BY RIVERalias0.TRAVERSE ORDER BY COUNT( DISTINCT RIVERalias0.TRAVERSE ) DESC LIMIT 1 ;
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "delaware" ;
[('wyoming',)]
[('new york',), ('pennsylvania',), ('new jersey',), ('delaware',)]

what states does the ohio river run through
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "ohio" ;
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "ohio" ;
[('ohio',), ('ohio',)]
[('pennsylvania',), ('west virginia',), ('kentucky',), ('indiana',), ('illinois',), ('ohio',)]

where is the chattahoochee river
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "chattahoochee" ;
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "chattahoochee" ;
[]
[('georgia',), ('florida',)]

which states does the chattahoochee river run through
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 GROUP BY ( RIVERalias0.TRAVERSE ) ORDER BY COUNT( DISTINCT RIVERalias0.TRAVERSE ) DESC LIMIT 1 ;
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "chattahoochee" ;
[('wyoming',)]
[('georgia',), ('florida',)]

what state is the largest in population
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
[(23670000,)]
[('california',)]

which state has the biggest population
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
[(23670000,)]
[('california',)]

how long is the longest river in the usa
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 ) ;
SELECT DISTINCT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 ) ;
[('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',)]
[(3968,)]

what is the largest river in washington state
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE IN ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ) ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "washington" ) AND RIVERalias0.TRAVERSE = "washington" ;
[('colorado',)]
[('columbia',)]

what is the longest river in florida
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 ) ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "florida" ) AND RIVERalias0.TRAVERSE = "florida" ;
[('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',)]
[('chattahoochee',)]

give me the number of rivers in california
SELECT COUNT( DISTINCT RIVERalias0.TRAVERSE ) FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH > 750 ;
SELECT COUNT( RIVERalias0.RIVER_NAME ) FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "california" ;
[(33,)]
[(1,)]

how many rivers are in iowa
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MIN( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "iowa" ) AND RIVERalias0.TRAVERSE = "iowa" ;
SELECT COUNT( RIVERalias0.RIVER_NAME ) FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "iowa" ;
[('mississippi',)]
[(2,)]

give me the states that border utah
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME NOT IN ( SELECT BORDER_INFOalias0.STATE_NAME FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "utah" ) ;
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "utah" ;
[('alabama',), ('alaska',), ('arizona',), ('arkansas',), ('california',), ('colorado',), ('connecticut',), ('delaware',), ('district of columbia',), ('florida',), ('georgia',), ('hawaii',), ('idaho',), ('illinois',), ('indiana',), ('iowa',), ('kansas',), ('kentucky',), ('louisiana',), ('maine',), ('maryland',), ('massachusetts',), ('michigan',), ('minnesota',), ('mississippi',), ('missouri',), ('montana',), ('nebraska',), ('nevada',), ('new hampshire',), ('new jersey',), ('new mexico',), ('new york',), ('north carolina',), ('north dakota',), ('ohio',), ('oklahoma',), ('oregon',), ('pennsylvania',), ('rhode island',), ('south carolina',), ('south dakota',), ('tennessee',), ('texas',), ('vermont',), ('virginia',), ('washington',), ('west virginia',), ('wisconsin',), ('wyoming',)]
[('wyoming',), ('colorado',), ('new mexico',), ('arizona',), ('nevada',), ('idaho',)]

Failed: no such column: BORDER_INFOalias0.STATE_NAME
what states are next to arizona
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "texas" ;
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "arizona" ;
[('oklahoma',), ('arkansas',), ('louisiana',), ('new mexico',)]
[('utah',), ('colorado',), ('new mexico',), ('california',), ('nevada',)]

what states border florida
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT BORDER_INFOalias1.BORDER FROM BORDER_INFO AS BORDER_INFOalias1 WHERE BORDER_INFOalias1.STATE_NAME IN ( SELECT BORDER_INFOalias2.BORDER FROM BORDER_INFO AS BORDER_INFOalias2 WHERE BORDER_INFOalias2.STATE_NAME = "florida" ) ) ;
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "florida" ;
[('tennessee',), ('georgia',), ('florida',), ('mississippi',), ('georgia',), ('alabama',), ('north carolina',), ('south carolina',), ('florida',), ('alabama',), ('tennessee',), ('tennessee',), ('alabama',), ('louisiana',), ('arkansas',), ('virginia',), ('south carolina',), ('georgia',), ('tennessee',), ('north carolina',), ('georgia',), ('kentucky',), ('virginia',), ('north carolina',), ('georgia',), ('alabama',), ('mississippi',), ('arkansas',), ('missouri',)]
[('georgia',), ('alabama',)]

what states border montana
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT BORDER_INFOalias1.BORDER FROM BORDER_INFO AS BORDER_INFOalias1 WHERE BORDER_INFOalias1.STATE_NAME = "montana" ) ;
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "montana" ;
[('montana',), ('wyoming',), ('utah',), ('nevada',), ('oregon',), ('washington',), ('minnesota',), ('south dakota',), ('montana',), ('north dakota',), ('minnesota',), ('iowa',), ('nebraska',), ('wyoming',), ('montana',), ('montana',), ('south dakota',), ('nebraska',), ('colorado',), ('utah',), ('idaho',)]
[('north dakota',), ('south dakota',), ('wyoming',), ('idaho',)]

what states surround kentucky
SELECT COUNT( BORDER_INFOalias0.BORDER ) FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "kentucky" ;
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "kentucky" ;
[(7,)]
[('indiana',), ('ohio',), ('west virginia',), ('virginia',), ('tennessee',), ('missouri',), ('illinois',)]

rivers in new york
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH > 750 ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "new york" ;
[('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('red',), ('red',), ('red',), ('red',), ('red',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('canadian',), ('canadian',), ('canadian',), ('canadian',), ('little missouri',), ('little missouri',), ('little missouri',), ('little missouri',), ('snake',), ('snake',), ('snake',), ('snake',), ('cimarron',), ('cimarron',), ('cimarron',), ('green',), ('green',), ('green',), ('north platte',), ('north platte',), ('north platte',), ('rio grande',), ('rio grande',), ('rio grande',), ('tennessee',), ('tennessee',), ('tennessee',), ('wabash',), ('wabash',), ('wabash',), ('yellowstone',), ('yellowstone',), ('yellowstone',), ('cheyenne',), ('cheyenne',), ('columbia',), ('columbia',), ('cumberland',), ('cumberland',), ('dakota',), ('dakota',), ('gila',), ('gila',), ('ouachita',), ('ouachita',), ('pearl',), ('pearl',), ('pecos',), ('pecos',), ('smoky hill',), ('smoky hill',), ('washita',), ('washita',), ('white',), ('white',)]
[('delaware',), ('allegheny',), ('hudson',)]

san antonio is in what state
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "san antonio" ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "san antonio" ;
[]
[('texas',)]

what state is miami in
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME IN ( SELECT STATEalias1.STATE_NAME FROM STATE AS STATEalias1 WHERE STATEalias1.STATE_NAME IN ( SELECT STATEalias2.STATE_NAME FROM STATE AS STATEalias2 WHERE STATEalias2.STATE_NAME = "miami" ) ) ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "miami" ;
[]
[('florida',)]

what states have cities named dallas
SELECT COUNT( CITYalias0.STATE_NAME ) FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "dallas" ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "dallas" ;
[(1,)]
[('texas',)]

what states have cities named rochester
SELECT COUNT( CITYalias0.STATE_NAME ) FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "rochester" ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "rochester" ;
[(2,)]
[('minnesota',), ('new york',)]

what states have cities named salt lake city
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "salt lake" ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "salt lake city" ;
[]
[('utah',)]

where is dallas
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.STATE_NAME = "dallas" ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "dallas" ;
[]
[('texas',)]

where is portland
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.STATE_NAME = "portland" AND CITYalias0.STATE_NAME = "maine" ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "portland" ;
[]
[('maine',), ('oregon',)]

which states have cities named austin
SELECT COUNT( CITYalias0.STATE_NAME ) FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "austin" ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "austin" ;
[(1,)]
[('texas',)]

how many people live in detroit
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "detroit" ) AND CITYalias0.STATE_NAME = "detroit" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "detroit" ;
[]
[(1203339,)]

how many people live in houston
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "houston" AND CITYalias0.STATE_NAME = "texas" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "houston" ;
[('texas',)]
[(1595138,)]

what is the population of houston
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "houston" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "houston" ;
[]
[(1595138,)]

what is the population of new york city
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "new york city" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "new york" ;
[]
[(7071639,)]

what is the population of tucson
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "tucson" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "tucson" ;
[]
[(330537,)]

what is the highest point in nevada in meters
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "nevada" ;
SELECT HIGHLOWalias0.HIGHEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "nevada" ;
[(800500,)]
[(4005,)]

what is the state with the largest area
SELECT MAX( STATEalias0.AREA ) FROM STATE AS STATEalias0 ;
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
[(591000.0,)]
[('alaska',)]

what is the highest point in states bordering georgia
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "georgia" ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "georgia" ) ORDER BY HIGHLOWalias0.HIGHEST_ELEVATION DESC LIMIT 1 ;
[('georgia',)]
[('mount mitchell',)]

what is the highest point in the states bordering colorado
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "colorado" ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "colorado" ) ORDER BY HIGHLOWalias0.HIGHEST_ELEVATION DESC LIMIT 1 ;
[('colorado',)]
[('gannett peak',)]

what is the highest point in iowa
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME IN ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = "iowa" ) ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "iowa" ;
[]
[('ocheyedan mound',)]

what is the highest point in maine
SELECT STATEalias0.AREA FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "maine" ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "maine" ;
[(33265.0,)]
[('mount katahdin',)]

what is the highest point in montana
SELECT HIGHLOWalias0.HIGHEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "montana" ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "montana" ;
[(3901,)]
[('granite peak',)]

what is the highest point in virginia
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION = ( SELECT MAX( HIGHLOWalias1.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "virginia" ;
[('alaska',)]
[('mount rogers',)]

what is the high point of wyoming
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "wyoming" ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "wyoming" ;
[('wyoming',)]
[('gannett peak',)]

where is the highest point in hawaii
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = HIGHLOWalias0.STATE_NAME ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "hawaii" ;
[('alabama',), ('alaska',), ('arizona',), ('arkansas',), ('california',), ('colorado',), ('connecticut',), ('delaware',), ('district of columbia',), ('florida',), ('georgia',), ('hawaii',), ('idaho',), ('illinois',), ('indiana',), ('iowa',), ('kansas',), ('kentucky',), ('louisiana',), ('maine',), ('maryland',), ('massachusetts',), ('michigan',), ('minnesota',), ('mississippi',), ('missouri',), ('montana',), ('nebraska',), ('nevada',), ('new hampshire',), ('new jersey',), ('new mexico',), ('new york',), ('north carolina',), ('north dakota',), ('ohio',), ('oklahoma',), ('oregon',), ('pennsylvania',), ('rhode island',), ('south carolina',), ('south dakota',), ('tennessee',), ('texas',), ('utah',), ('vermont',), ('virginia',), ('washington',), ('west virginia',), ('wisconsin',), ('wyoming',)]
[('mauna kea',)]

what is the highest point in delaware
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "delaware" ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "delaware" ;
[('delaware',)]
[('centerville',)]

count the states which have elevations lower than what alabama has
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION = ( SELECT MAX( HIGHLOWalias1.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
SELECT COUNT( HIGHLOWalias0.STATE_NAME ) FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.LOWEST_ELEVATION < ( SELECT HIGHLOWalias1.LOWEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias1 WHERE HIGHLOWalias1.STATE_NAME = "alabama" ) ;
[('alaska',)]
[(2,)]

how high is mount mckinley
SELECT MOUNTAINalias0.MOUNTAIN_NAME FROM MOUNTAIN AS MOUNTAINalias0 WHERE MOUNTAINalias0.MOUNTAIN_NAME = "mckinley" ;
SELECT HIGHLOWalias0.HIGHEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_POINT = "mount mckinley" ;
[('mckinley',)]
[(6194,)]

how tall is mount mckinley
SELECT MOUNTAINalias0.MOUNTAIN_NAME FROM MOUNTAIN AS MOUNTAINalias0 WHERE MOUNTAINalias0.MOUNTAIN_NAME = "mckinley" ;
SELECT HIGHLOWalias0.HIGHEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_POINT = "mount mckinley" ;
[('mckinley',)]
[(6194,)]

what is the maximum elevation of san francisco
SELECT MAX( HIGHLOWalias0.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION = ( SELECT MAX( HIGHLOWalias1.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
SELECT HIGHLOWalias0.HIGHEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_POINT = "san francisco" ;
[(6194,)]
[]

what is the highest elevation in the united states
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION = ( SELECT MAX( HIGHLOWalias1.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
SELECT MAX( HIGHLOWalias0.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias0 ;
[('alaska',)]
[(6194,)]

how long is the colorado river
SELECT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "colorado" ) AND RIVERalias0.TRAVERSE = "colorado" ;
SELECT DISTINCT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "colorado" ;
[(3033,)]
[(2333,)]

Failed: incomplete input
how long is the north platte river
SELECT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "north platte" ;
SELECT DISTINCT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "north platte" ;
[(1094,), (1094,), (1094,)]
[(1094,)]

what is the length of the colorado river
SELECT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "colorado" ) AND RIVERalias0.TRAVERSE = "colorado" ;
SELECT DISTINCT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "colorado" ;
[(3033,)]
[(2333,)]

how long is the longest river in california
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 ) ;
SELECT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "california" ) AND RIVERalias0.TRAVERSE = "california" ;
[('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',)]
[(2333,)]

what is the length of the longest river that runs through texas
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MIN( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "texas" ) AND RIVERalias0.TRAVERSE = "texas" ;
SELECT RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "texas" ) AND RIVERalias0.TRAVERSE = "texas" ;
[('pecos',), ('washita',)]
[(3033,)]

how many capitals does rhode island have
SELECT COUNT(*) FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "rhode island" ;
SELECT COUNT( STATEalias0.CAPITAL ) FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "rhode island" ;
[(0,)]
[(1,)]

Failed: no such column: CITYalias0.CITY_CITY
how many colorado rivers are there
SELECT COUNT( RIVERalias0.RIVER_NAME ) FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "colorado" ;
SELECT COUNT( RIVERalias0.RIVER_NAME ) FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "colorado" ;
[(10,)]
[(5,)]

how many people live in minneapolis minnesota
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "minneapolis" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "minneapolis" AND CITYalias0.STATE_NAME = "minnesota" ;
[]
[(370951,)]

what is the population of erie pennsylvania
SELECT COUNT( CITYalias0.CITY_NAME ) FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "erie" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "erie" AND CITYalias0.STATE_NAME = "pennsylvania" ;
[(0,)]
[(119123,)]

what is the population of tempe arizona
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "tempe" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "tempe" AND CITYalias0.STATE_NAME = "arizona" ;
[]
[(106919,)]

how many people live in the biggest city in new york state
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "new york" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "new york" ) AND CITYalias0.STATE_NAME = "new york" ;
[(17558000,)]
[(7071639,)]

how many people live in the capital of texas
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "texas" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = ( SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "texas" ) ;
[('austin',)]
[(345496,)]

how many people live in the united states
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "united states" ;
SELECT SUM( STATEalias0.POPULATION ) FROM STATE AS STATEalias0 ;
[]
[(225195124,)]

iowa borders how many states
SELECT BORDER_INFOalias0.STATE_NAME FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "iowa" ;
SELECT COUNT( BORDER_INFOalias0.BORDER ) FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "iowa" ;
[('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',)]
[(6,)]

number of states bordering iowa
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "iowa" ;
SELECT COUNT( BORDER_INFOalias0.BORDER ) FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "iowa" ;
[('minnesota',), ('wisconsin',), ('illinois',), ('missouri',), ('nebraska',), ('south dakota',)]
[(6,)]

how many states border the state with the largest population
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ) ;
SELECT COUNT( BORDER_INFOalias0.BORDER ) FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ) ;
[]
[(3,)]

Failed: incomplete input
how many states have a higher point than the highest point of the state with the largest capital city in the us
SELECT STATEalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 , STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = STATEalias0.CAPITAL ;
SELECT COUNT( HIGHLOWalias0.STATE_NAME ) FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION > ( SELECT HIGHLOWalias1.HIGHEST_ELEVATION FROM HIGHLOW AS HIGHLOWalias1 WHERE HIGHLOWalias1.STATE_NAME = ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = ( SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ) ) ) ;
[('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alabama',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arizona',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('arkansas',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('connecticut',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('delaware',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('district of columbia',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('florida',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('georgia',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('hawaii',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('idaho',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('illinois',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('indiana',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('iowa',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kansas',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('kentucky',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('louisiana',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maine',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('maryland',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('massachusetts',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('michigan',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('minnesota',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('mississippi',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('missouri',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('montana',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nebraska',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('nevada',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new hampshire',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new jersey',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new mexico',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('new york',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north carolina',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('north dakota',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('ohio',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oklahoma',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('oregon',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('pennsylvania',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('rhode island',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south carolina',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('south dakota',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('tennessee',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('texas',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('utah',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('vermont',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('virginia',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('washington',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('west virginia',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wisconsin',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',), ('wyoming',)]
[(0,)]

name the major rivers in florida
SELECT DISTINCT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH > 750 ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH > 750 AND RIVERalias0.TRAVERSE = "florida" ;
[('mississippi',), ('missouri',), ('colorado',), ('ohio',), ('red',), ('arkansas',), ('canadian',), ('little missouri',), ('snake',), ('cimarron',), ('green',), ('north platte',), ('rio grande',), ('tennessee',), ('wabash',), ('yellowstone',), ('cheyenne',), ('columbia',), ('cumberland',), ('dakota',), ('gila',), ('ouachita',), ('pearl',), ('pecos',), ('smoky hill',), ('washita',), ('white',)]
[]

through which states does the longest river in texas run
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "texas" ) AND RIVERalias0.TRAVERSE = "texas" ;
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "texas" ) ;
[('rio grande',)]
[('colorado',), ('new mexico',), ('texas',)]

what is the capital of california
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = "sacramento" ;
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "california" ;
[('california',)]
[('sacramento',)]

what is the capital of colorado
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "colorado" ;
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "colorado" ;
[]
[('denver',)]

what is the capital of illinois
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.STATE_NAME = "illinois" ;
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "illinois" ;
[('chicago',), ('rockford',), ('peoria',), ('springfield',), ('decatur',), ('aurora',), ('joliet',), ('evanston',), ('waukegan',), ('arlington heights',), ('elgin',), ('cicero',), ('oak lawn',), ('skokie',), ('champaign',)]
[('springfield',)]

what is the capital of massachusetts
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "massachusetts" ;
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "massachusetts" ;
[]
[('boston',)]

what is the capital of new york
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "new york" ;
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "new york" ;
[('new york',)]
[('albany',)]

what is the capital of ohio
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "ohio" ;
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "ohio" ;
[('cleveland',), ('columbus',), ('cincinnati',), ('toledo',), ('akron',), ('dayton',)]
[('columbus',)]

what is the capital of the florida state
SELECT COUNT( CITYalias0.CITY_NAME ) FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "florida" ;
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "florida" ;
[(5,)]
[('tallahassee',)]

Failed: incomplete input
what are the cities in states through which the mississippi runs
SELECT COUNT( RIVERalias0.TRAVERSE ) FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "mississippi" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "mississippi" ) ;
[(10,)]
[('little rock',), ('fort smith',), ('north little rock',), ('chicago',), ('rockford',), ('peoria',), ('springfield',), ('decatur',), ('aurora',), ('joliet',), ('evanston',), ('waukegan',), ('arlington heights',), ('elgin',), ('cicero',), ('oak lawn',), ('skokie',), ('champaign',), ('des moines',), ('cedar rapids',), ('davenport',), ('sioux city',), ('waterloo',), ('dubuque',), ('louisville',), ('lexington',), ('new orleans',), ('baton rouge',), ('shreveport',), ('metairie',), ('lafayette',), ('lake charles',), ('kenner',), ('monroe',), ('minneapolis',), ('st. paul',), ('duluth',), ('bloomington',), ('rochester',), ('jackson',), ('st. louis',), ('kansas city',), ('springfield',), ('independence',), ('st. joseph',), ('columbia',), ('memphis',), ('nashville',), ('knoxville',), ('chattanooga',), ('milwaukee',), ('madison',), ('green bay',), ('racine',), ('kenosha',), ('west allis',), ('appleton',)]

Failed: no such column: STATEalias0.CITIES
what are the highest points of all the states
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION = ( SELECT MAX( HIGHLOWalias1.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 ;
[('alaska',)]
[('cheaha mountain',), ('mount mckinley',), ('humphreys peak',), ('magazine mountain',), ('mount whitney',), ('mount elbert',), ('mount frissell',), ('centerville',), ('tenleytown',), ('walton county',), ('brasstown bald',), ('mauna kea',), ('borah peak',), ('charles mound',), ('franklin township',), ('ocheyedan mound',), ('mount sunflower',), ('black mountain',), ('driskill mountain',), ('mount katahdin',), ('backbone mountain',), ('mount greylock',), ('mount curwood',), ('eagle mountain',), ('woodall mountain',), ('taum sauk mountain',), ('granite peak',), ('johnson township',), ('boundary peak',), ('mount washington',), ('high point',), ('wheeler peak',), ('mount marcy',), ('mount mitchell',), ('white butte',), ('campbell hill',), ('black mesa',), ('mount hood',), ('mount davis',), ('jerimoth hill',), ('sassafras mountain',), ('harney peak',), ('clingmans dome',), ('guadalupe peak',), ('kings peak',), ('mount mansfield',), ('mount rogers',), ('mount rainier',), ('spruce knob',), ('timms hill',), ('gannett peak',)]

what are the major cities in alabama
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME = "alabama" ) AND CITYalias0.STATE_NAME = "alabama" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "alabama" ;
[('birmingham',)]
[('birmingham',), ('mobile',), ('montgomery',)]

what are the major cities in alaska
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = "alaska" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "alaska" ;
[]
[('anchorage',)]

what are the major cities in new york
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "new york" ;
[('birmingham',), ('mobile',), ('montgomery',), ('anchorage',), ('phoenix',), ('tucson',), ('mesa',), ('little rock',), ('los angeles',), ('san diego',), ('san francisco',), ('san jose',), ('long beach',), ('oakland',), ('sacramento',), ('anaheim',), ('fresno',), ('santa ana',), ('riverside',), ('huntington beach',), ('denver',), ('colorado springs',), ('aurora',), ('washington',), ('jacksonville',), ('miami',), ('tampa',), ('st. petersburg',), ('fort lauderdale',), ('atlanta',), ('columbus',), ('honolulu',), ('ewa',), ('chicago',), ('indianapolis',), ('fort wayne',), ('gary',), ('des moines',), ('wichita',), ('kansas city',), ('louisville',), ('lexington',), ('new orleans',), ('baton rouge',), ('shreveport',), ('metairie',), ('baltimore',), ('boston',), ('worcester',), ('springfield',), ('detroit',), ('grand rapids',), ('warren',), ('flint',), ('minneapolis',), ('st. paul',), ('jackson',), ('st. louis',), ('kansas city',), ('omaha',), ('lincoln',), ('las vegas',), ('newark',), ('jersey city',), ('albuquerque',), ('new york',), ('buffalo',), ('rochester',), ('yonkers',), ('syracuse',), ('charlotte',), ('greensboro',), ('cleveland',), ('columbus',), ('cincinnati',), ('toledo',), ('akron',), ('dayton',), ('oklahoma city',), ('tulsa',), ('portland',), ('philadelphia',), ('pittsburgh',), ('providence',), ('memphis',), ('nashville',), ('knoxville',), ('chattanooga',), ('houston',), ('dallas',), ('san antonio',), ('el paso',), ('fort worth',), ('austin',), ('corpus christi',), ('lubbock',), ('arlington',), ('salt lake city',), ('norfolk',), ('virginia beach',), ('richmond',), ('arlington',), ('seattle',), ('spokane',), ('tacoma',), ('milwaukee',), ('madison',)]
[('new york',), ('buffalo',), ('rochester',), ('yonkers',), ('syracuse',)]

what are the major cities in the state of california
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.STATE_NAME = "california" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "california" ;
[('los angeles',), ('san diego',), ('san francisco',), ('san jose',), ('long beach',), ('oakland',), ('sacramento',), ('anaheim',), ('fresno',), ('santa ana',), ('riverside',), ('huntington beach',), ('stockton',), ('glendale',), ('fremont',), ('torrance',), ('garden grove',), ('san bernardino',), ('pasadena',), ('east los angeles',), ('oxnard',), ('modesto',), ('sunnyvale',), ('bakersfield',), ('concord',), ('berkeley',), ('fullerton',), ('inglewood',), ('hayward',), ('pomona',), ('orange',), ('ontario',), ('santa monica',), ('santa clara',), ('citrus heights',), ('norwalk',), ('burbank',), ('chula vista',), ('santa rosa',), ('downey',), ('costa mesa',), ('compton',), ('carson',), ('salinas',), ('west covina',), ('vallejo',), ('el monte',), ('daly city',), ('thousand oaks',), ('san mateo',), ('simi valley',), ('oceanside',), ('richmond',), ('lakewood',), ('santa barbara',), ('el cajon',), ('ventura',), ('westminster',), ('whittier',), ('south gate',), ('alhambra',), ('buena park',), ('san leandro',), ('alameda',), ('newport beach',), ('escondido',), ('irvine',), ('mountain view',), ('fairfield',), ('redondo beach',), ('scotts valley',)]
[('los angeles',), ('san diego',), ('san francisco',), ('san jose',), ('long beach',), ('oakland',), ('sacramento',), ('anaheim',), ('fresno',), ('santa ana',), ('riverside',), ('huntington beach',)]

what are the major cities in vermont
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "vermont" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "vermont" ;
[('montpelier',)]
[]

what major cities are located in pennsylvania
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.STATE_NAME = "pennsylvania" ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "pennsylvania" ;
[('philadelphia',), ('pittsburgh',), ('erie',), ('allentown',), ('scranton',), ('upper darby',), ('reading',), ('bethlehem',), ('lower merion',), ('abingdon',), ('bristol township',), ('penn hills',), ('altoona',)]
[('philadelphia',), ('pittsburgh',)]

Failed: no such table: RIVERASRIVERalias0
what are the population densities of each us state
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.DENSITY = ( SELECT MAX( STATEalias1.DENSITY ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.DENSITY FROM STATE AS STATEalias0 ;
[(7365000,)]
[(75.31914893617021,), (0.6798646362098139,), (23.842105263157894,), (42.96992481203007,), (149.81012658227849,), (27.778846153846153,), (618.9243027888447,), (290.60665362035223,), (580.0,), (141.9375509728533,), (92.75042444821732,), (148.97233812393756,), (11.373493975903614,), (202.4866785079929,), (151.65745856353593,), (51.740674955595026,), (28.724179829890645,), (28.724179829890645,), (88.17610062893081,), (33.81932962573275,), (403.1548757170172,), (692.5398358281024,), (158.32478632478632,), (48.29383886255924,), (52.83018867924528,), (70.53084648493544,), (5.351700680272109,), (20.297542043984475,), (7.244343891402715,), (99.21327729281172,), (945.8071144214717,), (10.71546052631579,), (357.5967413441955,), (111.67647617239415,), (9.231966053748232,), (261.50121065375305,), (43.24517512508935,), (27.12391705211542,), (261.8301403725611,), (781.5181518151816,), (100.3374795101726,), (8.957505576015354,), (108.94636924537257,), (53.33068472716233,), (17.208480565371026,), (53.203661327231124,), (131.1776251226693,), (60.36484245439469,), (80.57851239669421,), (83.69989136822609,), (4.8007545317915525,)]

Failed: near "RIVERAS": syntax error
Failed: near "RIVERAS": syntax error
what are the populations of states which border texas
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "texas" AND STATEalias0.STATE_NAME = STATEalias0.STATE_NAME ;
SELECT STATEalias0.POPULATION FROM BORDER_INFO AS BORDER_INFOalias0 , STATE AS STATEalias0 WHERE BORDER_INFOalias0.STATE_NAME = "texas" AND STATEalias0.STATE_NAME = BORDER_INFOalias0.BORDER ;
[(14229000,)]
[(3025000,), (2286000,), (4206000,), (1303000,)]

what are the populations of the major cities of texas
SELECT COUNT( CITYalias0.CITY_NAME ) FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "texas" ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = "texas" ;
[(9,)]
[(1595138,), (904078,), (785880,), (425259,), (385164,), (345496,), (231999,), (173979,), (160123,)]

what city has the most people
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 GROUP BY CITYalias0.STATE_NAME ORDER BY COUNT( 1 ) DESC LIMIT 1 ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
[('california',)]
[('new york',)]

what city in the united states has the highest population
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
[('california',)]
[('new york',)]

which us city has the highest population
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
[('california',)]
[('new york',)]

Failed: no such column: HIGHLOWalias0.CAPITAL
what is the biggest american city in a state with a river
SELECT COUNT( RIVERalias0.RIVER_NAME ) FROM RIVER AS RIVERalias0 GROUP BY ( RIVERalias0.RIVER_NAME ) ORDER BY COUNT( DISTINCT RIVERalias0.TRAVERSE ) DESC LIMIT 1 ;
SELECT DISTINCT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 , RIVER AS RIVERalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 , RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = CITYalias1.STATE_NAME ) AND RIVERalias0.TRAVERSE = CITYalias0.STATE_NAME ;
[(10,)]
[('new york',)]

Failed: no such column: STATEalias0.CAPITAL
Failed: no such column: CITYalias0.CAPITAL
what is the capital of the state with the largest population density
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
SELECT DISTINCT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.DENSITY = ( SELECT MAX( STATEalias1.DENSITY ) FROM STATE AS STATEalias1 ) ;
[('california',)]
[('trenton',)]

what is the capital of the state with the largest population
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
[('juneau',)]
[('sacramento',)]

what is the capital of the state with the most inhabitants
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
[('juneau',)]
[('sacramento',)]

what is the capital of the state with the longest river
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 ) ;
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 ) ) ;
[('montana',), ('north dakota',), ('south dakota',), ('iowa',), ('nebraska',), ('missouri',)]
[('des moines',), ('jefferson city',), ('helena',), ('lincoln',), ('bismarck',), ('pierre',)]

what is the combined area of all 50 states
SELECT SUM( STATEalias0.POPULATION ) FROM STATE AS STATEalias0 ;
SELECT SUM( STATEalias0.AREA ) FROM STATE AS STATEalias0 ;
[(225195124,)]
[(3670038.0,)]

Failed: no such table: Density
what is the population density of maine
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "maine" ;
SELECT STATEalias0.DENSITY FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = "maine" ;
[(1125000,)]
[(33.81932962573275,)]

what is the highest point in the state with capital austin
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = "austin" ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME IN ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = "austin" ) ;
[('texas',)]
[('guadalupe peak',)]

what is the highest point in the usa
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION = ( SELECT MAX( HIGHLOWalias1.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION = ( SELECT MAX( HIGHLOWalias1.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
[('alaska',)]
[('mount mckinley',)]

Failed: incomplete input
Failed: incomplete input
Failed: incomplete input
Failed: incomplete input
Failed: incomplete input
Failed: incomplete input
what is the longest river in the states that border nebraska
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MIN( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "nebraska" ) AND RIVERalias0.TRAVERSE = "nebraska" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "nebraska" ) ) AND RIVERalias0.TRAVERSE IN ( SELECT BORDER_INFOalias1.BORDER FROM BORDER_INFO AS BORDER_INFOalias1 WHERE BORDER_INFOalias1.STATE_NAME = "nebraska" ) ;
[('republican',)]
[('missouri',), ('missouri',), ('missouri',)]

what is the longest river that flows through a state that borders indiana
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "indiana" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "indiana" ) ) AND RIVERalias0.TRAVERSE IN ( SELECT BORDER_INFOalias1.BORDER FROM BORDER_INFO AS BORDER_INFOalias1 WHERE BORDER_INFOalias1.STATE_NAME = "indiana" ) ;
[('indiana',), ('indiana',)]
[('mississippi',), ('mississippi',)]

Failed: no such table: HIGHLOWas
what is the lowest point in massachusetts
SELECT HIGHLOWalias0.LOWEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.LOWEST_ELEVATION = ( SELECT MIN( HIGHLOWalias1.LOWEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
SELECT HIGHLOWalias0.LOWEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "massachusetts" ;
[('death valley',)]
[('atlantic ocean',)]

Failed: no such table: RIVERASRIVER
what is the lowest point in nebraska in meters
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MIN( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "nebraska" ) AND RIVERalias0.TRAVERSE = "nebraska" ;
SELECT HIGHLOWalias0.LOWEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "nebraska" ;
[('republican',)]
[('southeast corner',)]

what is the lowest point in the state of california
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.LOWEST_ELEVATION = ( SELECT MIN( HIGHLOWalias1.LOWEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
SELECT HIGHLOWalias0.LOWEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "california" ;
[('california',)]
[('death valley',)]

where is the lowest point in maryland
SELECT HIGHLOWalias0.LOWEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.LOWEST_ELEVATION = ( SELECT MIN( HIGHLOWalias1.LOWEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ;
SELECT HIGHLOWalias0.LOWEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "maryland" ;
[('death valley',)]
[('atlantic ocean',)]

what is the lowest point of all states through which the colorado river runs through
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE IN ( SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.LOWEST_ELEVATION = ( SELECT MIN( HIGHLOWalias1.LOWEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 ) ) ;
SELECT HIGHLOWalias0.LOWEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "colorado" ) ORDER BY HIGHLOWalias0.LOWEST_ELEVATION LIMIT 1 ;
[('california',)]
[('death valley',)]

Failed: no such table: RIVERASRIVER
what is the population density of the largest state
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.DENSITY FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
[(23670000,)]
[(0.6798646362098139,)]

what is the population of the largest city in the state with the largest area
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 WHERE CITYalias1.STATE_NAME IN ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ) ) AND CITYalias0.STATE_NAME IN ( SELECT STATEalias2.STATE_NAME FROM STATE AS STATEalias2 WHERE STATEalias2.AREA = ( SELECT MAX( STATEalias3.AREA ) FROM STATE AS STATEalias3 ) ) ;
[(401800,)]
[(174431,)]

what is the population of the smallest state
SELECT CITYalias0.POPULATION FROM CITY AS CITYalias0 WHERE CITYalias0.CITY_NAME = ( SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MIN( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ) ;
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MIN( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
[(638333,)]
[(638000,)]

Failed: incomplete input
what is the population of the state with the highest population density
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.POPULATION FROM STATE AS STATEalias0 WHERE STATEalias0.DENSITY = ( SELECT MAX( STATEalias1.DENSITY ) FROM STATE AS STATEalias1 ) ;
[('california',)]
[(7365000,)]

what is the smallest city in the usa
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MIN( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ) ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MIN( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
[('washington',)]
[('scotts valley',)]

what is the smallest city in the us
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION > 150000 AND CITYalias0.STATE_NAME = ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MIN( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ) ;
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MIN( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
[('washington',)]
[('scotts valley',)]

Failed: incomplete input
what is the smallest state bordering wyoming
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME = ( SELECT MIN( STATEalias1.STATE_NAME ) FROM STATE AS STATEalias1 ) ;
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MIN( STATEalias1.AREA ) FROM STATE AS STATEalias1 WHERE STATEalias1.STATE_NAME IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "wyoming" ) ) AND STATEalias0.STATE_NAME IN ( SELECT BORDER_INFOalias1.BORDER FROM BORDER_INFO AS BORDER_INFOalias1 WHERE BORDER_INFOalias1.STATE_NAME = "wyoming" ) ;
[('alabama',)]
[('south dakota',)]

Failed: incomplete input
what is the total length of all rivers in the usa
SELECT COUNT( DISTINCT RIVERalias0.RIVER_NAME ) FROM RIVER AS RIVERalias0 ;
SELECT SUM( DERIVED_TABLEalias0.LENGTH ) FROM ( SELECT DISTINCT RIVERalias0.RIVER_NAME , RIVERalias0.LENGTH FROM RIVER AS RIVERalias0 ) AS DERIVED_TABLEalias0 ;
[(46,)]
[(51393,)]

Failed: no such column: RIVERalias0.CITY
what rivers are in states that border texas
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "texas" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "texas" ) ;
[('red',), ('canadian',), ('rio grande',), ('pecos',), ('washita',)]
[('mississippi',), ('mississippi',), ('red',), ('red',), ('red',), ('red',), ('arkansas',), ('arkansas',), ('canadian',), ('canadian',), ('cimarron',), ('cimarron',), ('rio grande',), ('san juan',), ('gila',), ('neosho',), ('ouachita',), ('ouachita',), ('pearl',), ('pecos',), ('st. francis',), ('washita',), ('white',)]

what rivers traverses the state which borders the most states
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 GROUP BY ( RIVERalias0.RIVER_NAME ) ORDER BY COUNT( DISTINCT RIVERalias0.TRAVERSE ) DESC LIMIT 1 ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 GROUP BY BORDER_INFOalias0.BORDER HAVING COUNT( 1 ) = ( SELECT MAX( DERIVED_TABLEalias0.DERIVED_FIELDalias0 ) FROM ( SELECT BORDER_INFOalias1.BORDER , COUNT( 1 ) AS DERIVED_FIELDalias0 FROM BORDER_INFO AS BORDER_INFOalias1 GROUP BY BORDER_INFOalias1.BORDER ) AS DERIVED_TABLEalias0 ) ) ;
[('mississippi',)]
[('mississippi',), ('mississippi',), ('missouri',), ('tennessee',), ('cumberland',), ('st. francis',), ('white',)]

what river traverses the state which borders the most states
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 GROUP BY ( RIVERalias0.RIVER_NAME ) ORDER BY COUNT( DISTINCT RIVERalias0.TRAVERSE ) DESC LIMIT 1 ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 GROUP BY BORDER_INFOalias0.BORDER HAVING COUNT( 1 ) = ( SELECT MAX( DERIVED_TABLEalias0.DERIVED_FIELDalias0 ) FROM ( SELECT BORDER_INFOalias1.BORDER , COUNT( 1 ) AS DERIVED_FIELDalias0 FROM BORDER_INFO AS BORDER_INFOalias1 GROUP BY BORDER_INFOalias1.BORDER ) AS DERIVED_TABLEalias0 ) ) ;
[('mississippi',)]
[('mississippi',), ('mississippi',), ('missouri',), ('tennessee',), ('cumberland',), ('st. francis',), ('white',)]

Failed: incomplete input
Failed: incomplete input
what state contains the highest point of those the colorado river traverses
SELECT HIGHLOWalias0.HIGHEST_POINT FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "colorado" ;
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.HIGHEST_ELEVATION = ( SELECT MAX( HIGHLOWalias1.HIGHEST_ELEVATION ) FROM HIGHLOW AS HIGHLOWalias1 WHERE HIGHLOWalias1.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "colorado" ) ) ;
[('mount elbert',)]
[('california',)]

what state has the largest capital
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = STATEalias0.CAPITAL ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 , STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = CITYalias1.CITY_NAME ) ;
[('montgomery',), ('juneau',), ('phoenix',), ('little rock',), ('sacramento',), ('denver',), ('hartford',), ('dover',), ('washington',), ('tallahassee',), ('atlanta',), ('honolulu',), ('boise',), ('springfield',), ('indianapolis',), ('des moines',), ('topeka',), ('frankfort',), ('baton rouge',), ('augusta',), ('annapolis',), ('boston',), ('lansing',), ('st. paul',), ('jackson',), ('jefferson city',), ('helena',), ('lincoln',), ('carson city',), ('concord',), ('trenton',), ('santa fe',), ('albany',), ('raleigh',), ('bismarck',), ('columbus',), ('oklahoma city',), ('salem',), ('harrisburg',), ('providence',), ('columbia',), ('pierre',), ('nashville',), ('austin',), ('salt lake city',), ('montpelier',), ('richmond',), ('olympia',), ('charleston',), ('madison',), ('cheyenne',)]
[('arizona',)]

which state 's capital city is the largest
SELECT STATEalias0.CAPITAL FROM STATE AS STATEalias0 WHERE STATEalias0.AREA = ( SELECT MAX( STATEalias1.AREA ) FROM STATE AS STATEalias1 ) ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MAX( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 , STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = CITYalias1.CITY_NAME ) ;
[('juneau',)]
[('arizona',)]

Failed: incomplete input
Failed: near "AS": syntax error
what states border states that the ohio runs through
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME = "ohio" ) ;
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME = "ohio" ) ;
[('indiana',), ('kentucky',), ('michigan',), ('pennsylvania',), ('west virginia',)]
[('wisconsin',), ('indiana',), ('kentucky',), ('missouri',), ('iowa',), ('michigan',), ('ohio',), ('kentucky',), ('illinois',), ('indiana',), ('ohio',), ('west virginia',), ('virginia',), ('tennessee',), ('missouri',), ('illinois',), ('michigan',), ('pennsylvania',), ('west virginia',), ('kentucky',), ('indiana',), ('new york',), ('new jersey',), ('delaware',), ('maryland',), ('west virginia',), ('ohio',), ('pennsylvania',), ('maryland',), ('virginia',), ('kentucky',), ('ohio',)]

Failed: incomplete input
what states border the state that borders the most states
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ) ;
SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT BORDER_INFOalias1.BORDER FROM BORDER_INFO AS BORDER_INFOalias1 GROUP BY BORDER_INFOalias1.BORDER HAVING COUNT( 1 ) = ( SELECT MAX( DERIVED_TABLEalias0.DERIVED_FIELDalias0 ) FROM ( SELECT BORDER_INFOalias2.BORDER , COUNT( 1 ) AS DERIVED_FIELDalias0 FROM BORDER_INFO AS BORDER_INFOalias2 GROUP BY BORDER_INFOalias2.BORDER ) AS DERIVED_TABLEalias0 ) ) ;
[('oregon',), ('nevada',), ('arizona',)]
[('iowa',), ('illinois',), ('kentucky',), ('tennessee',), ('arkansas',), ('oklahoma',), ('kansas',), ('nebraska',), ('kentucky',), ('virginia',), ('north carolina',), ('georgia',), ('alabama',), ('mississippi',), ('arkansas',), ('missouri',)]

Failed: incomplete input
Failed: incomplete input
Failed: incomplete input
Failed: incomplete input
what states contain at least one major rivers
SELECT COUNT( DISTINCT RIVERalias0.TRAVERSE ) FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH > 750 ;
SELECT DISTINCT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH > 750 ;
[(33,)]
[('minnesota',), ('wisconsin',), ('iowa',), ('illinois',), ('missouri',), ('kentucky',), ('tennessee',), ('arkansas',), ('mississippi',), ('louisiana',), ('montana',), ('north dakota',), ('south dakota',), ('nebraska',), ('colorado',), ('utah',), ('arizona',), ('nevada',), ('california',), ('pennsylvania',), ('west virginia',), ('indiana',), ('ohio',), ('new mexico',), ('texas',), ('oklahoma',), ('kansas',), ('wyoming',), ('idaho',), ('oregon',), ('washington',), ('alabama',), ('michigan',)]

where are mountains
SELECT MOUNTAINalias0.STATE_NAME FROM MOUNTAIN AS MOUNTAINalias0 WHERE MOUNTAINalias0.STATE_NAME = "whitney" ;
SELECT MOUNTAINalias0.STATE_NAME FROM MOUNTAIN AS MOUNTAINalias0 ;
[]
[('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('alaska',), ('california',), ('california',), ('california',), ('california',), ('california',), ('california',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('colorado',), ('washington',)]

where is the highest mountain of the united states
SELECT MOUNTAINalias0.MOUNTAIN_NAME FROM MOUNTAIN AS MOUNTAINalias0 WHERE MOUNTAINalias0.MOUNTAIN_ALTITUDE = ( SELECT MAX( MOUNTAINalias1.MOUNTAIN_ALTITUDE ) FROM MOUNTAIN AS MOUNTAINalias1 ) ;
SELECT MOUNTAINalias0.STATE_NAME FROM MOUNTAIN AS MOUNTAINalias0 WHERE MOUNTAINalias0.MOUNTAIN_ALTITUDE = ( SELECT MAX( MOUNTAINalias1.MOUNTAIN_ALTITUDE ) FROM MOUNTAIN AS MOUNTAINalias1 ) ;
[('mckinley',)]
[('alaska',)]

where is the smallest city
SELECT CITYalias0.CITY_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MIN( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 WHERE CITYalias0.POPULATION = ( SELECT MIN( CITYalias1.POPULATION ) FROM CITY AS CITYalias1 ) ;
[('scotts valley',)]
[('california',)]

which is the density of the state that the largest river in the united states runs through
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ) ) ;
SELECT STATEalias0.DENSITY FROM STATE AS STATEalias0 WHERE STATEalias0.STATE_NAME IN ( SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 WHERE RIVERalias0.LENGTH = ( SELECT MAX( RIVERalias1.LENGTH ) FROM RIVER AS RIVERalias1 ) ) ;
[('arizona',), ('nevada',), ('oregon',), ('oregon',), ('arizona',)]
[(51.740674955595026,), (70.53084648493544,), (5.351700680272109,), (20.297542043984475,), (9.231966053748232,), (8.957505576015354,)]

which is the highest peak not in alaska
SELECT HIGHLOWalias0.STATE_NAME FROM HIGHLOW AS HIGHLOWalias0 WHERE HIGHLOWalias0.STATE_NAME = "alaska" ;
SELECT MOUNTAINalias0.MOUNTAIN_NAME FROM MOUNTAIN AS MOUNTAINalias0 WHERE MOUNTAINalias0.MOUNTAIN_ALTITUDE = ( SELECT MAX( MOUNTAINalias1.MOUNTAIN_ALTITUDE ) FROM MOUNTAIN AS MOUNTAINalias1 WHERE MOUNTAINalias1.STATE_NAME <> "alaska" ) ;
[('alaska',)]
[('whitney',)]

which rivers do not run through texas
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "texas" ;
SELECT DISTINCT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.RIVER_NAME NOT IN ( SELECT RIVERalias1.RIVER_NAME FROM RIVER AS RIVERalias1 WHERE RIVERalias1.TRAVERSE = "texas" ) ;
[('red',), ('canadian',), ('rio grande',), ('pecos',), ('washita',)]
[('mississippi',), ('missouri',), ('colorado',), ('ohio',), ('arkansas',), ('connecticut',), ('delaware',), ('little missouri',), ('snake',), ('chattahoochee',), ('cimarron',), ('green',), ('north platte',), ('potomac',), ('republican',), ('san juan',), ('tennessee',), ('wabash',), ('yellowstone',), ('allegheny',), ('bighorn',), ('cheyenne',), ('clark fork',), ('columbia',), ('cumberland',), ('dakota',), ('gila',), ('hudson',), ('neosho',), ('niobrara',), ('ouachita',), ('pearl',), ('powder',), ('roanoke',), ('rock',), ('smoky hill',), ('south platte',), ('st. francis',), ('tombigbee',), ('wateree catawba',), ('white',)]

which rivers do not run through usa
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 GROUP BY ( RIVERalias0.RIVER_NAME ) ORDER BY COUNT( DISTINCT RIVERalias0.TRAVERSE ) DESC LIMIT 1 ;
SELECT DISTINCT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.COUNTRY_NAME <> "usa" ;
[('mississippi',)]
[]

which rivers run through states that border the state with the capital austin
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE = "austin" ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE IN ( SELECT BORDER_INFOalias0.BORDER FROM BORDER_INFO AS BORDER_INFOalias0 WHERE BORDER_INFOalias0.STATE_NAME IN ( SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.CAPITAL = "austin" ) ) ;
[]
[('mississippi',), ('mississippi',), ('red',), ('red',), ('red',), ('red',), ('arkansas',), ('arkansas',), ('canadian',), ('canadian',), ('cimarron',), ('cimarron',), ('rio grande',), ('san juan',), ('gila',), ('neosho',), ('ouachita',), ('ouachita',), ('pearl',), ('pecos',), ('st. francis',), ('washita',), ('white',)]

which rivers run through states with fewest cities
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 GROUP BY ( RIVERalias0.TRAVERSE ) ORDER BY COUNT( DISTINCT RIVERalias0.TRAVERSE ) DESC LIMIT 1 ;
SELECT RIVERalias0.RIVER_NAME FROM RIVER AS RIVERalias0 WHERE RIVERalias0.TRAVERSE IN ( SELECT DERIVED_TABLEalias0.STATE_NAME FROM ( SELECT CITYalias0.STATE_NAME , COUNT( 1 ) AS DERIVED_FIELDalias0 FROM CITY AS CITYalias0 GROUP BY CITYalias0.STATE_NAME ) AS DERIVED_TABLEalias0 WHERE DERIVED_TABLEalias0.DERIVED_FIELDalias0 = ( SELECT MIN( DERIVED_TABLEalias1.DERIVED_FIELDalias1 ) FROM ( SELECT COUNT( 1 ) AS DERIVED_FIELDalias1 FROM CITY AS CITYalias1 GROUP BY CITYalias1.STATE_NAME ) AS DERIVED_TABLEalias1 ) ) ;
[('wyoming',)]
[('mississippi',), ('missouri',), ('missouri',), ('red',), ('canadian',), ('delaware',), ('little missouri',), ('little missouri',), ('little missouri',), ('snake',), ('snake',), ('cimarron',), ('green',), ('north platte',), ('potomac',), ('rio grande',), ('san juan',), ('yellowstone',), ('yellowstone',), ('bighorn',), ('cheyenne',), ('cheyenne',), ('clark fork',), ('dakota',), ('dakota',), ('gila',), ('niobrara',), ('pecos',), ('powder',), ('tombigbee',)]

Failed: no such column: CITYalias0.CAPITAL
Failed: incomplete input
which state has the smallest average urban population
SELECT STATEalias0.STATE_NAME FROM STATE AS STATEalias0 WHERE STATEalias0.POPULATION = ( SELECT MAX( STATEalias1.POPULATION ) FROM STATE AS STATEalias1 ) ;
SELECT CITYalias0.STATE_NAME FROM CITY AS CITYalias0 GROUP BY CITYalias0.STATE_NAME ORDER BY AVG ( CITYalias0.POPULATION ) LIMIT 1 ;
[('california',)]
[('wyoming',)]

which states have a river
SELECT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 GROUP BY RIVERalias0.TRAVERSE ORDER BY COUNT( DISTINCT RIVERalias0.TRAVERSE ) DESC LIMIT 1 ;
SELECT DISTINCT RIVERalias0.TRAVERSE FROM RIVER AS RIVERalias0 ;
[('wyoming',)]
[('minnesota',), ('wisconsin',), ('iowa',), ('illinois',), ('missouri',), ('kentucky',), ('tennessee',), ('arkansas',), ('mississippi',), ('louisiana',), ('montana',), ('north dakota',), ('south dakota',), ('nebraska',), ('colorado',), ('utah',), ('arizona',), ('nevada',), ('california',), ('pennsylvania',), ('west virginia',), ('indiana',), ('ohio',), ('new mexico',), ('texas',), ('oklahoma',), ('kansas',), ('new hampshire',), ('vermont',), ('massachusetts',), ('connecticut',), ('new york',), ('new jersey',), ('delaware',), ('wyoming',), ('idaho',), ('oregon',), ('washington',), ('georgia',), ('florida',), ('maryland',), ('virginia',), ('district of columbia',), ('alabama',), ('michigan',), ('north carolina',), ('south carolina',)]

4-shot prompting with similar examples, execution acc: 0.35018050541516244