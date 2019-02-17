# Friend Chatbot

This chatbot will initiate a conversation with the user, interacting with them like a friend. It will be able to understand the gist of what the user is saying, and (hopefully) respond in an appropriate way.

Usage:
All conversation topics are handled dynamically in [convo.dat]. The first line of a topic is structured as follows:
[. or ?][keywords]([^variable][.wordType] OR [+])
Explanation:
[. or ?]: Depending on whether the topic expects a statement (.) or question (?) from the user (although currently unused).
[keywords]: When looking for only one of a multiple set of similar keywords, separate them with /'s (eg, hi/hey/hello). When looking for another set/single keyword, separate with &'s (eg, i&like&ham). Note that they must all be lowercase. Combined example: do&you/u&like/enjoy&soccer/football
[^variable]: Used when expecting to detect a single word from the user to save in memory, referenced by the give name ('variable' in this case)
[.wordType]: Dictates which word type (as defined by the NLTK library. eg, NNP = proper noun, VB = verb) to look for in the user's response, in order to help determine which word to save as the answer 'variable'.
[+]: Used when expecting to detect the positivity of the user's following response.
Note: Only one of [^variable.wordType] and [+] may be used at a time. In other words, the chatbot cannot handle both determining the positivity of the user's next response as well as saving a certain answer from it.


The rest of the topic is separated by newlines, with the bot waiting a response between each line before printing the next line.
In order to reference a saved answer from the user [^variable from before], simply put [$variable] in the bot's response, which will be replaced by the saved answer. Note that an answer must first be saved before it can be called like this. Otherwise, it will return "NaN" instead.
When using the [+] operator, the following 3 lines must start with + (positive), - (negative), and 0 (neutral), in any order. The positivity score of the user's last response will be used to determine which of these three responses to output.

Restrictions:
convo.dat file must begin with an empty line, and end with two empty lines.
First 2 topics of convo.dat must be default statement response and default question response, respectively.
Correlation algorithm likely won't scale well when many more topics are added.
Doesn't handle context well; user must explicitly mention what they're referring to each time they ask a question.
Can't both save an answer and determine the positivity of a single user response.
If the [+] operator is used, the next 3 lines MUST start with each one of +, -, and 0.