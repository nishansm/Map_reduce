Consider, you have a text document as input. Count the number of times a word
occurs in the document. Develop a MapReduce framework based on Python
threads. The data will be read from a file, stored in-memory and will run on a
single computer.
You need to simulate MapReduce using the Python programming language. Use
the required libraries to solve the problem. Other than map and reduce, in
practice there need to exist other components, for example the results from a
map need to be shuffled before being sent to reduce processes: if the two
instances of the word ‘Apple’ were sent to distinct reduce processes, the count
would not be correct. Word counting could be implemented with a map function
that would emit an entry for every word found with a count of 1, and a reduce
function would sum all the map entries for the same word.
Let’s see this in action with a typical example of a MapReduce application: word
counting.
