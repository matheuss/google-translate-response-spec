#Google Translate "f.txt" Specification

***

First of all, let's make some things clear. __f.txt is valid JS array__. So if you're using JS, you can start using it _instantly_. Otherwise, you have to change it to appropriate for your language format.

Here's an example of changing this array to Python list. The steps are: 

1. Change all implicit "undefined" types ([,,] is equal to [,undefined,] in JS) to None:
 * Comma right after opening bracket: '[,' -> '[None,'
 * Multiple commas: ',,,' -> ',None,None,'
 * Comma right before closing bracket:  ',]' -> ',None]'
2. Change all unicode characters in hex form to actual characters: '\u003c' -> '<'

Also, this specification shows response to standard web-translate's request with __following options__:
 ```dt = [at,bd,ex,ld,md,qca,rw,rm,ss,t]```

We don't know what they mean (yet).

Actual specification is using python highlighting: couldn't find more convenient way of formatting.  

Some notes and symbols of specification:

*	#something - optional data, that could not be at all (if it's response's data, then it's "undefined" in JS)
	*	0: list: main translation - this list always exists
	*	#1: list: translations - be aware, that this list can be missing sometimes (for specific request, to be precise)
*	'sometext' - some string (no explicit designation of type, yes)
*	int, float, and other types - guess what
*	(? {some comment}) - I am not sure about definition of data I gave.
*	(some comment) - just comment
*	??? - I do not have any idea what the heck is this 
*	{3-1-2} - reference to another element in the array, in this example to array[3][1][2]
*	Reverse translation - translation of translation back to the source language
	*	e.g. English -> Russian -> English: like 'get' -> 'получать' -> 'receive'. 'receive' is reverse translation

=======================================================
SPECIFICATION of f.txt
=======================================================

```python


0: list: main translation
	lists:
		0: 'way of writing'
		1: 'translated phrase'
		#2: int: range = [0-2], appears only in {0-0}
				assumption:		0 - no pronunciation in {0-1}
								1 - dunno
								2 - verbose pronunciation, like 'fəˈtēg'

#1: list: translations
		lists: translation for exact part of speech
			0: 'part of speech'
			1: list: 'translation options of this part of speech'
			2: list: reverse translation of options
				lists: 
					0: 'translation option'
					1: list of 'reverse translations', float: frequency of usage in language (?)]
			3: 'original phrase'
			4: int: priority of using(? I REALLY DO NOT KNOW WHAT IS THIS)

2: 'target language (?)'

#3: ???

#4: ???

5: list: improve our translation
	0: list
		0: 'original phrase'
		1: int: number of parts of phrase available for changing (?)
		2: list
			lists:
				0: 'option'
				1: int: sort of priority (?)
				2: bool: ??? 
				3: bool: ??? 
		3: list
			0: list with 2 ints: position of substring to replace 
		4: 'original phrase' (?)
		5: int: ???
		6: int: ???

6: float or int: propotion of using this phrase in source language relatively to others

#7: list: misspelling
	0: '<b><i>correct phrase</i></b>' (i've seen only this kind of formatting)
	1: 'correct phrase?'
	2: list with single int: ???
	3: bool: ???

8: list: word's appearing in languages
	0: list of 'shorten names of languages where word appears' ('en', 'ru', etc.)
	1: list of floats or ints: propotion of using this phrase in this language relatively to others
		e.g. if there are 0.9 for 'en' and 0.1 for 'fr', it means, 
			that this phrase refers 9 times more to english than to french 
		note: first number is always (i guess) equal to {4}
	2: list of 'shorten names of languages where word appears (the same as {6-0})'

#9: ???

#10: ???

#11: list: synonyms
	lists: synonyms for exact part of speech
		0: 'part of speech'
		1: list: synonyms for exact meaning
			lists:
				0: list of 'synonims'
				1: 'Something like m_en_usNUMBER1_NUMBER2 some kind of dictionary ID, 
					where NUMBER1 is word, and NUMBER2 is meaning. Wonder what dictionary'
		2: 'original phrase' (?)

#12: list: definitions
	lists: definitions for exact part of speech
		0: 'part of speech'
		1: list: definitions
			lists:
				0: 'definition'
				1: 'meaning ID (look above)' (?)
				2: 'example of using'
		2: 'orginal phrase' (?)

#13: list: examples (? i do not know why is there nested lists)
	list: examples
		lists:
			0: 'example'
			1: int: ???
			2: 'meaning ID'

#14: list: see also
	list of 'ALSOs'

```

===========================================================================================
Example (python version): english 'fatige' (yes, with a typo) to russian:
===========================================================================================


```python
[

0:	[
		['усталость', 'fatigue', None, None, 2], [[], None, "ustalost'", 'fəˈtēg']
	], 


1:	[
		['noun', 
			['усталость', 'утомление', 'утомительная работа', 'утомительность', 'рабочая команда', 'нестроевой наряд'], 
			[
				['усталость', 
					['fatigue', 'weariness', 'tiredness', 'lassitude', 'languor'], None, 0.70910621], 
				['утомление', 
					['fatigue', 'tiredness', 'distress', 'wear and tear'], 
					None, 
					0.025428746], 
				['утомительная работа', 
					['slog', 'fatigue', 'fag'], 
					None, 
					0.00015846132], 
				['утомительность', 
					['tediousness', 'tedium', 'fatigue', 'weariness'], 
					None, 
					0.00011775846], 
				['рабочая команда', 
					['fatigue party', 'fatigue'], 
					None, 
					7.8444042e-05], 
				['нестроевой наряд', 
					['fatigue duty', 'fatigue'], 
					None, 
					3.9444141e-05]
				], 
				'fatigue', 
				1],
		['verb', 
			['утомлять', 'изнурять'], 
				[
					['утомлять', 
						['tire', 'weary', 'fatigue', 'wear', 'tax', 'wear down'], 
						None, 
						0.041274928], 
					['изнурять', 
						['run down', 'exhaust', 'wear', 'harass', 'fatigue', 'poop'], 
						None, 
						3.9444141e-05]
				], 
				'fatigue', 
				2
		]
	], 
	

2:	'en', 
	

3:	None, 
	

4:	None, 
	
	[

5:		['fatigue', 32000, 
			[
				['усталость', 1000, True, False], 
				['усталости', 0, True, False],
				['усталостной', 0, True, False],
				['слабость', 0, True, False], 
				['усталостная', 0, True, False]
			], 
			[[0, 7]], 
			'fatigue', 
			0, 
			0]
		], 
	

6	1, 
	

7:	['<b><i>fatigue</i></b>', 'fatigue', [1], None, None, True], 


8:	[['ht'], None, [1], ['ht']], 


9:	None, 


10:	None, 


11:	[
		['noun', 
			[
				[
					['tiredness', 'weariness', 'sleepiness', 'drowsiness', 'exhaustion', 'enervation', 'languor', 'lethargy', 'torpor', 'prostration', 'war-weariness'], 
					'm_en_us1246403.001'
				], 
				[
					['fatigue duty'], ''
				], 
				[
					['weariness', 'tiredness'], 
					''
				]
			], 
			'fatigue'
		], 
		['verb', 
			[
				[
					['tire (out)', 'exhaust', 'wear out', 'drain', 'weary', 'wash out', 'overtire', 'prostrate', 'enervate', 'knock out', 'take it out of', 'do in', 'poop', 'bush', 'wear to a frazzle'], 
					'm_en_us1246403.007'
				], 
				[
					['jade', 'tire', 'weary', 'pall'], 
					''
				], 
				[
					['wear down', 'tire out', 'fag', 'jade', 'wear', 'tire', 'wear out', 'weary', 'outwear', 'fag out'], 
					''
				]
			], 
			'fatigue'
		]
	], 


12:	[
		['noun', 
			[
				['extreme tiredness, typically resulting from mental or physical exertion or illness.', 'm_en_us1246403.001', 'he was nearly dead with fatigue'], 
				['a group of soldiers ordered to perform menial, nonmilitary tasks, sometimes as a punishment.', 'm_en_us1246403.005']
			], 
			'fatigue'], 
		['verb', 
			[
				['cause (someone) to feel tired or exhausted.', 'm_en_us1246403.007', 'they were fatigued by their journey']
			], 
			'fatigue']
	], 
	

13:	[
		[
			['Do these exercises at the end of your regular strength-training workout because you will fully <b>fatigue</b> your abs performing these exercises.', None, None, None, 3, 'm_en_us1246403.008'], 
			['metal <b>fatigue</b>', None, None, None, 3, 'm_en_gb0289000.004'], 
			['The spar had actually twisted as a result of metal <b>fatigue</b> and failure.', None, None, None, 3, 'm_en_us1246403.003'], 
			['Symptoms of hepatitis include chronic <b>fatigue</b> and liver problems.', None, None, None, 3, 'm_en_us1246403.001'], 
			["However, we're close to the limit in terms of metal <b>fatigue</b> and durability.", None, None, None, 3, 'm_en_us1246403.003'], 
			['Glutamine helps to prevent muscle <b>fatigue</b> , thus allowing you to rip out more reps.', None, None, None, 3, 'm_en_us1246403.002'], ['Other medical conditions can cause extreme <b>fatigue</b> or changes in appetite and sleep.', None, None, None, 3, 'm_en_us1246403.001'], ['metal <b>fatigue</b>', None, None, None, 3, 'm_en_us1246403.003'], ['This could make the inspiratory muscles vulnerable to the development of muscle <b>fatigue</b> .', None, None, None, 3, 'm_en_us1246403.002'], ['Even now a certain amount of election <b>fatigue</b> is beginning to set in.', None, None, None, 3, 'm_en_us1246403.004'], ['There are different kinds of <b>fatigue</b> associated with cancer therapies.', None, None, None, 3, 'm_en_us1246403.001'], ['Slip bands have been observed at stresses below the <b>fatigue</b> limit of ferrous materials.', None, None, None, 3, 'm_en_us1246403.003'], ['That along with corrosion and metal <b>fatigue</b> cased the bridge to fail.', None, None, None, 3, 'm_en_us1246403.003'], ['Unfortunately, metal <b>fatigue</b> kept causing it to crash.', None, None, None, 3, 'm_en_us1246403.003'], ['Increased muscle creatine also buffers the lactic acid produced during exercise, delaying muscle <b>fatigue</b> and soreness.', None, None, None, 3, 'm_en_us1246403.002'], ['Two major causes of premature <b>fatigue</b> during exercise are dehydration and carbohydrate depletion.', None, None, None, 3, 'm_en_us1246403.001'], ['The news from Lone Star Park, Texas is that all is well, and that the local media, doubtless suffering from presidential election <b>fatigue</b> , is lapping her up.', None, None, None, 3, 'm_en_us1246403.004'], ['In mild cases it may be necessary to <b>fatigue</b> the symptomatic muscle.', None, None, None, 3, 'm_en_us1246403.008'], ['Engineers have also been looking at the threat of lightning, metal <b>fatigue</b> and noise.', None, None, None, 3, 'm_en_us1246403.003'], ['He revealed a bit of fundraiser <b>fatigue</b> in response.', None, None, None, 3, 'm_en_us1246403.004'], ['The remaining patients complained of leg <b>fatigue</b> as the predominant symptom limiting exercise.', None, None, None, 3, 'm_en_us1246403.002'], ['Acute pancreatitis and <b>fatigue</b> of the diaphragm muscle are also associated with damage caused by ROS.', None, None, None, 3, 'm_en_us1246403.002'], ['Always use enough weight to <b>fatigue</b> your muscles by the final rep of each set.', None, None, None, 3, 'm_en_us1246403.008'], ['Research shows that driver <b>fatigue</b> is a factor in approximately 25 % of all accidents on motorways and trunk roads.', None, None, None, 3, 'm_en_us1246403.001'], ['How will the parties defeat election <b>fatigue</b> and boost declining turn-out numbers?', None, None, None, 3, 'm_en_us1246403.004'], ['buccinator and orbicularis oris muscles showing signs of <b>fatigue</b>', None, None, None, 3, 'm_en_gb0289000.002'], ['Three well-planned exercises performed properly will always fully <b>fatigue</b> the triceps.', None, None, None, 3, 'm_en_us1246403.008'], ['Even so, the job saps the vitality, and a referee gets mental <b>fatigue</b> as well as physical.', None, None, None, 3, 'm_en_us1246403.001'], ['You should also be aware of the increased <b>fatigue</b> associated with this transition.', None, None, None, 3, 'm_en_us1246403.001'], ['Respiratory muscle <b>fatigue</b> develops when demand for energy exceeds the supply of energy.', None, None, None, 3, 'm_en_us1246403.002']
		]
	], 

14:	[
		['fatigue strength', 'chronic fatigue syndrome', 'metal fatigue', 'compassion fatigue', 'mental fatigue']
	]
]
```
