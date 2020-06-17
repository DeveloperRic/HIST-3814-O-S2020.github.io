# Analysing Virginia Woolf's Diaries

## Overview

This is a quick static website I made to host my progress in week 6. For this week I downloaded Virginia Woolf's diary entires from 17 October 1924 to 25 November 1929. I performed a number of actions, procedures and visualisations on the data. What did I do?

- I used REGEX patterns and python to sanitize and transform all the text in every entry of the diary into a dictionary, qualitative tsv file and csv quanititative csv file
- I used [Open Refine](openrefine.org) to brush up the edges of my tsv file and remove any excess columns and whitespace
- I used [Voyant Tools](voyant-tools.org) to visualise my data and gain some insights into the patterns in Woolf's diary
- I used the [Topic Modeling Tool](https://github.com/senderle/topic-modeling-tool) to learn 7 general themes in the diary, each (luckly) came with their own tuple of grounding emotions
- I used [TwoTone](twotone.io) to sonify my csv file, giving me even more insight into the patterns of what Virginia Woolf wrote in her diary
- And of course, I used GitHub pages to make this homepage

You can find the full account of my proccess on my progress repository. There, I have all my (ncessary) files uploaded, so you can clone it and take a deep-dive for yourself.

## List of things I did

1.  1-by-1 copy and pasted each diary entry into it's own text file. I could have written a script to do this with wget but that would have taken more time than it was worth because each diary entry was centered within other elements on the HTML page.
2. Manually ensured every diary entry has a date at the top
3. Wrote a Python script ([parse_entries.py](https://github.com/DeveloperRic/HIST-3814-O-S2020/blob/master/week6/parse_entries.py)) to parse all entires into a single [`parsed-entires.tsv`](https://github.com/DeveloperRic/HIST-3814-O-S2020/blob/master/week6/diary-entries/parsed-entries.tsv) file
4. (Partially) used OpenRefine on the data [[project tar]](https://github.com/DeveloperRic/HIST-3814-O-S2020/blob/master/week6/virginia-woolf-diary.openrefine.tar.gz)
- Visualise and find trends with Voyant [[view project]](https://voyant-tools.org/?panels=collocatesgraph%2Creader%2Ctrends%2Cknots%2Ccontexts&corpus=26eb9c0774002fa1ad8725fabf31ae6d)
- Use the TopicModeling tool to learn about the topics in Virginia Woolf's diary [[results page]](https://github.com/DeveloperRic/HIST-3814-O-S2020/blob/master/week6/topic_modelling/output/output_html/all_topics.html)
- Sonify Woolf's diary based on topics identified in the previous step [[audio file (min 6- is pretty interesting)]](https://github.com/DeveloperRic/HIST-3814-O-S2020/blob/master/week6/sonification/audio.mp3)
- Publish this week's work to [GitHub pages](https://HIST-3814-O-S2020.github.io)

## So how did I do all that?

### Downloading Orlando Data

As I was about to begin work on developing my corpus of work for this week. I encountered a paywall barring me from being able to access the data relating to the "understanding of literature, focusing particularly on the part women have played in its development".

With me already being behind schedule this issue threw a real monkey wrench into the gears of my workflow.

In response, I pivoted -- whilst still focusing on the same theme of feminism -- to the [diaraies of Viginia Woolf](http://woolfonline.com/?node=diary_overview). Woolf is accreddited as the main source of inspiration for [Orlando](http://orlando.cambridge.org/public/svDocumentation?formname=t&d_id=ABOUTTHEPROJECT) and as such I have chosen her diaries as the focus of my analysis. _(Talk about turning an L into a W)_

### Regex patterns used in parsed-entries.tsv

_`&nbsp;` represents a space_

| Pattern&emsp;&emsp;&emsp;&emsp;&emsp; | Replacement | Explanation |
|---------|-------------|-------------|
| `'^[0-9]+\.txt$'` | | only match diary entry-files |
| `(^ +)|( +$)` | | trim line |
| `&nbsp;&nbsp;+` | `&nbsp;` | reduce any lengthy spaces to just one space |
| `\n\n*` | | reduce all multi-newlines to just one newline |

### OpenRefine operations

1. Define column headings as `'date', 'column 2', ...`
2. Apply `trim leading and trailing whitespace` as well as `collapse consecutive whitespace` transformations
3. Remove empty columns
4. Save project as [`virginia-woolf-diary.tsv`](diary-entries\virginia-woolf-diary.tsv)

### OpenRefine

It was kind of funny trying to use OpenRefine for my data. Because each row was an entry and each entry was a diary log, the columns (exluding the date column) were all cluttered with arbitrary amounts of text.

![open refine loading](https://raw.githubusercontent.com/DeveloperRic/HIST-3814-O-S2020/master/week6/snippets/load-open-refine.PNGg)

![open refine facet](https://raw.githubusercontent.com/DeveloperRic/HIST-3814-O-S2020/master/week6/snippets/open-refine-facet.PNG)

The columns proved to be too diverse for me to use OpenRefine on them and so I decided to just perform some basic operations on the entires -- trimming & colapsing whitespace and removing empty columns.

![open refine history](https://raw.githubusercontent.com/DeveloperRic/HIST-3814-O-S2020/master/week6/snippets/open-refine-history.PNG)

### Voyant actions

1. Load [virginia-woolf-diary.tsv](diary-entries\virginia-woolf-diary.tsv) directly into Voyant
2. In 'Contexts' view, search for collocates of 'England'
3. In 'Trends' view, show `'wom*'` and `'men*|man` using 25 document segements

    !['(?wo)m[ae]n' trends](https://raw.githubusercontent.com/DeveloperRic/HIST-3814-O-S2020/master/week6/voyant/woman-man-trends.png)

### Reflections from Voyant

#### England

It seems like Virgina Woolf was a very passionate Englishwoman. By investivating the conexts in which Woolf used the word 'England' and reading the surrounding diary entries, I could see that Woolf felt very invovled in the growth of England, so much so that she felt it was important for her to celebrate the voices of those who built the nation. Specifically, in a diary entry where Woolf described feeling sentimental, she mentions that she want's to "gather material for the Lives of the Obscure" -- a book written to recount the history of England through 'obscure' lives.

_contexts of 'England':_
<iframe style='width: 638px; height: 183px;' src='https://voyant-tools.org/tool/Contexts/?query=england*&context=10&corpus=26eb9c0774002fa1ad8725fabf31ae6d'></iframe>

#### Woman/Man

Taking a hint from [this exercise](https://programminghistorian.org/en/lessons/corpus-analysis-with-antconc) in week 4, I searched for the trend graph of `'wom*'` and `'men*|man` to see how Virginia Woolf's use of both words changed over time, and what came up was quite interesting. At 5 document segments, Woolf mentioned men significantly more than she did women and at 1 document segment she did the same but for women. This didn't mean much to me but I used that information as a heuristic for what to look for when topic modelling and using Antconc.

<iframe style='width: 424px; height: 291px;' src='https://voyant-tools.org/tool/Trends/?query=man*%7Cmen&query=wom*&bins=25&mode=document&corpus=26eb9c0774002fa1ad8725fabf31ae6d'></iframe>

### TopicModelling steps

1. Write Python script ([sanitize_entries.py](sanitize_entries.py)) to sanitize all diary entry text files and write them back into a different `'input'` directory
2. Set the TopicModelintTool input dir to `topic_modelling/input`
3. Set the TopicModelintTool output dir to `topic_modelling/output`
4. Set number of topics to 7 _**| >> learn topics**_

### TopicModeling Tool

By running the TopicModeling tool, I discovered 7 general themes of Virginia Woolf's diary, which I named:

0. expressing emotions about country/location
1. life & economics
2. writing
3. home, colour & femininity
4. movement & masculinity
5. darkness, work & creativity
6. clothing & joy

The fact that 'writing' surfaced up as a topic proved my assumption that Woolf was a lover of books, particularly those about patriotism and class. It seems like a lot of what Woolf wrote in her diary expressed her highly emotive perspective on life which perhaps, was needed in the "Roaring Twenties", the age right after the first world war.

I ended up using the diary entries that heavily featured topics 1 and 3 as a possible measure for sonification.

### Sonification tracks

Here is a list of the tracks used in TwoTone to sonify Virginia Woolf's diary (from heighest to lowest track). I modified each track to better express the emotion of the topics that they portray. Sadder topics have their track in a minor scale; topics relating to dynamics (movement) have their tracks played in faster tempos. All tempos are factors of 2 (to preserve the consistency of the audio).

![sonify tracks snippet](https://raw.githubusercontent.com/DeveloperRic/HIST-3814-O-S2020/master/week6/snippets/sonify-tracks.PNG)

1. Recorded audio detailing the instrument of each following track and the topic that it represents
    - volume: 66%
    - filter: by line_number 0-191

2. Double bass - line_number
    - volume: 21%
    - C Major; 2 octaves; auto; 6x; ascending

3. glockenspiel - expressing emotions about country/location
    - volume: 81%
    - C Major; 2 octaves; auto; 1x

4. curch organ - life & economics
    - volume: 84%
    - C Major; 2 octaves; auto; 1x

5. marimba - writing
    - volume: 72%
    - C Major; 2 octaves; auto; 4x; ascending

6. piano - home, colour & femininity
    - volume: 80%
    - C Major; 2 octaves; auto; 2x; ascending

7. electric guitar - movement & masculinity
    - volume: 84%
    - C Major; 2 octaves; auto; 2x; descending

8. violin - darkness, work & creativity
    - volume: 80%
    - C Minor; 2 octaves; auto; 1x

9. trumpet - clothing & joy
    - volume: 84%
    - C Major; 2 octaves; auto; 4x; ascending

## Errors

[_back to top_](#contents)

### Sonification

The TwoTone app seems to be really buggy. If I change any track, I have to reload the page before I can actually listen to the audio again. Also, I tried exporting the audio twice and both audio files have no sound (but they have all the metadata and megabytes). I loaded the created audio file into Audacity and sure enough, there was nothing in the file.

![sonify muted file snippet](https://raw.githubusercontent.com/DeveloperRic/HIST-3814-O-S2020/master/week6/snippets/sonify-mute.PNG)

### Sonification

I tried to really utilise my coding expertise as a Computer Science major in this weeks work. Hence, I made a Python script ([prepare_to_sonify.py](prepare_to_sonify.py)) to parse the output of the TopicModeling tool into a single tsv that I can use for sonification.

After listening to the track, I could see that Virginia Woolf wrote a lot about _clothing & joy_ in the earlier entires of her diary but not so much in the later ones. Woolf also seems to write a whole lot about _writing_, itself. Perhaps writing in her diary was more than just record keeping for her, it may have been an beloved hobby. However, when it comes to the instruments of the other topics, their notes are fleeting but consistent and loud. It could be possible that those other topics weren't discussed as frequently but more heavily than _clothing & joy_ and _writing_.

## Downloads

[_back to top_](#contents)

### Data

- `(collection)` [Diaries of Virginia Woolf](http://woolfonline.com/?node=content/contextual/transcriptions&project=1&parent=41&taxa=42)
  - 17 October 1924 - 25 November 1929
