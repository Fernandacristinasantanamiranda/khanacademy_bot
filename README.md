# I don't have a better name
An answer revealer.

  *This works as of 12/5/2020* 

If this script helped or interested you, please consider staring the repo above. That number looks cool when it's big

Written to be used with a userscript manager, like [TamperMonkey for Chrome](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=en) or [Greasemonkey for Firefox](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/). Download one of these, then click 

## Usage
The script will console log answers as the browser gets them. That's about it.


## Gotchas
- Khan Academy always requests the current and next question, so **expect the second to last console log message to be the correct answer**
- This works only for expression, free response, multiple choice, and dropdown questions.
- When there are multiple answers, fill in the boxes left-to-right and then down. Example below
  - answer: `[1, 2, 3, 4]`  question:  ![picture of question](readme/multiple_free_response.png)
- The script will do its best to find the answer in the question data (read below to understand the exploit)
- I am lazy, therefore this is buggy. Don't be surprised when you run into a question you'll actually have to do

## Exploit
It's pretty simple. On every 'quiz' you open in the app, your browser makes a request to `/getAssessmentItem`. The server responds with everything your client needs to draw **and grade** your question. Within this graphql response is a json blob containing a list of questions, most of them with a `correct: boolean` attribute.

## Implementation
I wrote this for tampermonkey, although all should work on gecko. It essentially hooks into the browser's `fetch`, which is what Khan Academy uses now (this is why the some old exploits no longer work, along with the endpoint change), and when `/getAssessmentItem` is requested, it logs the "important" part of the response.

## Licence
This has the GNU GPL 3.0 licence. I expect most users will be people like me who have AP Stats assignments and no will to do them. I don't care too much about what you do with it, but I like credit :)