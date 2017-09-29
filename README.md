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
