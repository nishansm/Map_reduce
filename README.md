from threading import Thread
from collections import defaultdict
import re

def mapper(text):
    # split the text into words and count each word as 1
    words = re.findall('\w+', text)
    mapped_dict = defaultdict(int)
    for word in words:
        mapped_dict[word] += 1
    return mapped_dict

def reducer(mapped_dicts):
    # combine the mapped dictionaries and sum the counts for each word
    reduced_dict = defaultdict(int)
    for mapped_dict in mapped_dicts:
        for word, count in mapped_dict.items():
            reduced_dict[word] += count
    return reduced_dict

def map_reduce(text):
    # split the text into chunks and run mapper function on each chunk using threads
    chunk_size = len(text) // 4
    chunks = [text[i:i+chunk_size] for i in range(0, len(text), chunk_size)]
    threads = []
    for chunk in chunks:
        thread = Thread(target=mapper, args=(chunk,))
        threads.append(thread)
        thread.start()
    # wait for all threads to finish and collect their results
    mapped_dicts = []
    for thread in threads:
        thread.join()
        mapped_dicts.append(thread.result)
    # run the reducer function on the mapped dictionaries
    return reducer(mapped_dicts)

# read the text file
with open('"C:\Users\Nishan S M\Desktop\industry visit.docx", 'r') as f:
    text = f.read()
# run the map_reduce function on the text and print the result
result = map_reduce(text)
print(result)
