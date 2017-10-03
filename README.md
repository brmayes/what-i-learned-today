# what-i-learned-today

### 09-29-17
Topics: jupyter, pandas

To apply a function to all column headers, use `rename` with `lambda`.
Example:
```
def classify(string):
    classified = string.lower().strip().replace(' ','-')
    return classified

df.rename(columns=lambda c: classify(c), inplace=True)
df
```

### 10-02-17
Topics: python, argparse, make

Argparse is a built-in parser for command line options using python. Here's a quick example (via [PythonForBeginners.com](http://www.pythonforbeginners.com/argparse/argparse-tutorial)) that returns the max of a list of numbers or the sum using `--sum`.
`argparse_ex.py`
```
import argparse

parser = argparse.ArgumentParser(description='Process some integers.')
parser.add_argument('integers', metavar='N', type=int, nargs='+',
                    help='an integer for the accumulator')
parser.add_argument('--sum', dest='accumulate', action='store_const',
                    const=sum, default=max,
                    help='sum the integers (default: find the max)')

args = parser.parse_args()
print(args.accumulate(args.integers))
```

`command line`
```
python argparse_ex.py 1 2 3 4 5 15
# returns 15

python argparse_ex.py --sum 1 2 3 4 5 15
# returns 30
```

### 10-03-17
Topics: jupyter, pandas, regex

Using a regex to find and replace inline in python.
```
def classify(string):
    string = re.sub(r'\(|\)', '', string)
    classified = string.lower().strip().replace(' ','-')
    return classified

classify('Direct Loans Dollars Outstanding (in billions)')
# returns direct-loans-dollars-outstanding-in-billions
```
