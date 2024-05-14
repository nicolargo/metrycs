# Metrycs

Manage metrics through this Python lib.

Example:

```
from metrics import Metric

foo = Metric()
foo.add(80)
foo.last() # return 80
foo.add(82)
foo.last() # return 82
foo.get() # return [80, 82]
foo.reset()
foo.last() # return None

rate = Metric(rate=True)
foo.add(80)
foo.last() # return None
foo.add(82)
foor.last() # return 2
foor.add(86)
foo.last() # return 4
foo.get() # return [2, 4]
```

Possible implementation:

```
from metrics import Metric

class Metric:
    def __init__(self, rate=False):
        self.values = []
        self.rates = []  # New list to store calculated rates
        self.rate = rate

    def add(self, value):
        self.values.append(value)
        if self.rate:
            if len(self.values) > 1:  # Calculate rate only after more than one value
                previous_value = self.values[0]
                current_rate = (value - previous_value) / len(self.values)
                self.rates.append(current_rate)

    def last(self):
        if not self.values:
            return None
        return self.values[-1] if not self.rate else self.rates[-1]

    def get(self):
        if not self.rate:
            return self.values
        else:
            return self.rates  # Return the list of calculated rates

    def reset(self):
        self.values = []
        self.rates = []  # Reset the rates list as well
```
