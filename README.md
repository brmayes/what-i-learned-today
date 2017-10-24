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

**Important discovery!**
`shift + tab` shows the docs of the function you called!

### 10-18-17
Topics: jupyter, pandas

To group two rows, simply rename one or both of them to have a commonality then use `.groupby()` followed by `.sum()`. A simple way of doing this is using `.replace()` method to rename.

```
df.replace({'borrow_amt': {'<5K':'<10K','5K to 10K':'<10K'}}).groupby('borrow_amt',sort=False).sum().reset_index()
```

Here's an example on [Stack Overflow](https://stackoverflow.com/questions/37947479/pandas-sum-two-rows-of-dataframe-without-rearranging-dataframe).

### 10-23-17
Topics: QGIS, locator maps

To add a singular point at an exact coordinate, make a CSV with name/lat/long. Then, just import into QGIS as a delimited text layer.

To add a radius around a specific point or shape, use a buffer. To do so with a simple plugin, use `MMQGIS`. For more go [here](https://gis.stackexchange.com/questions/29509/how-to-draw-a-circle-with-a-set-radius).

To export a map, use the map composer. Here's a nice [walkthrough](http://docs.qgis.org/2.0/da/docs/training_manual/map_composer/map_composer.html).

### 10-24-17
Topics: Illustrator, locator maps, SVG, QGIS, regex

After exporting from QGIS to a SVG, you can make updates and style changes to the map in Illustrator. Biggest thing I've learned: **SAVE ALL WORK AS AN AI FILE BEFORE MAKING EDITS**. If you continually save as an SVG and close the file, Illustrator will have a hard time opening it after encoding it to open in inkscape. But, if that does happen and you can't open the file in Illustrator, open the SVG using a text editor and use a regex to take out inkscape instances.

To fix SVG code:
```
inkscape:[^"]+"[^"]+"
```
