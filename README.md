# what-i-learned-today

### 4-25-18
Topics: jupyter, python

If you need to export a json file with nested elements, you can use this:

```
json = (df.groupby(['TOP_LEVEL','TOP_LEVEL_1','TOP_LEVEL_2'], as_index=False)
                 .apply(lambda x: x[['SECOND_LEVEL','SECOND_LEVEL_2']].to_dict('r'))
                 .reset_index()
                 .rename(columns={0:'SECOND_LEVEL_OBJ_NAME'})
                 .to_json(orient='records'))
```

Get a more in-depth explanation [here](https://stackoverflow.com/questions/40470954/convert-pandas-dataframe-to-nested-json?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa).

### 2-11-18
Topics: MacOS, Ruby, xCode

If running `xcode-select --install` gives you an error that it "can't download the software because of a network problem", run:

```
sudo defaults delete /Library/Preferences/com.apple.SoftwareUpdate CatalogURL
```

Source: Nokogiri(http://www.nokogiri.org/tutorials/installing_nokogiri.html)

### 12-5-17
Topics: jupyter, python

To export your notebook to a python script, use `nbconvert`:

```
jupyter nbconvert --to script [NOTBOOK_NAME].ipynb
```

There are other options as well. Check the docs [here](http://nbconvert.readthedocs.io/en/stable/usage.html#).

### 12-1-17
Topics: jupyter, chrome

If you're getting a message like...

```
0:97: execution error: "http://localhost:8888/tree?token=[RANDOM_TOKEN_KEY_HERE]" doesn’t understand the “open location” message. (-1708)
```

...that means that when you type `jupyter notebook` in your terminal and it doesn't automatically open in chrome, there's a simple solution!

Open your `~/.bash_profile` and add `export BROWSER=open`. Source it and try to open your jupyter notebook again from the command line! I found the solution [here](https://github.com/conda/conda/issues/5408).

### 11-3-17
Topics: Pip

If you're getting a weird `Command "python setup.py egg_info" failed with error code 1` error when trying to use `pip install`, it's because something isn't up to date with pip.

To fix, you'll need to upgrade `Setuptools`:
```
pip install --upgrade setuptools
```

Then, just try to install the software again.

### 10-24-17
Topics: Illustrator, locator maps, SVG, QGIS, regex

After exporting from QGIS to a SVG, you can make updates and style changes to the map in Illustrator. Biggest thing I've learned: **SAVE ALL WORK AS AN AI FILE BEFORE MAKING EDITS**. If you continually save as an SVG and close the file, Illustrator will have a hard time opening it after encoding it to open in inkscape. But, if that does happen and you can't open the file in Illustrator, open the SVG using a text editor and use a regex to take out inkscape instances.

To fix SVG code:
```
inkscape:[^"]+"[^"]+"
```

### 10-23-17
Topics: QGIS, locator maps

To add a singular point at an exact coordinate, make a CSV with name/lat/long. Then, just import into QGIS as a delimited text layer.

To add a radius around a specific point or shape, use a buffer. To do so with a simple plugin, use `MMQGIS`. For more go [here](https://gis.stackexchange.com/questions/29509/how-to-draw-a-circle-with-a-set-radius).

To export a map, use the map composer. Here's a nice [walkthrough](http://docs.qgis.org/2.0/da/docs/training_manual/map_composer/map_composer.html).

### 10-18-17
Topics: jupyter, pandas

To group two rows, simply rename one or both of them to have a commonality then use `.groupby()` followed by `.sum()`. A simple way of doing this is using `.replace()` method to rename.

```
df.replace({'borrow_amt': {'<5K':'<10K','5K to 10K':'<10K'}}).groupby('borrow_amt',sort=False).sum().reset_index()
```

Here's an example on [Stack Overflow](https://stackoverflow.com/questions/37947479/pandas-sum-two-rows-of-dataframe-without-rearranging-dataframe).

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
