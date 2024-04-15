# ****[Name-that-hash](https://github.com/HashPals/Name-That-Hash) api version****

## 🤔 What is this?

**Have you ever come across a hash such as `5f4dcc3b5aa765d61d8327deb882cf99` and wondered what type of hash that is? 🤔
**

**Name-that-hash will name that hash type!**

## Installing

### pip

``` bash
pip install nth_api
```

### poetry

``` bash
poetry add nth_api
```

### Example

```python
from nth_api.hashes import hashes_dict, popular_hashes_list
import re


def main(chash: str) -> str | list | None:
    # Initialize an empty list to store matching values
    output = []

    # Iterate over patterns in the dictionary
    for pattern in hashes_dict.keys():
        # Check if the hash matches the pattern
        if re.compile(pattern, re.IGNORECASE).match(chash.strip()):
            # Add the corresponding value to the output list
            output.append(hashes_dict[pattern])

    # If matching values are found
    if output:
        # Initialize an empty list to store popular matching values
        populars = []
        # Iterate over matching values
        for name in output:
            # Check if the value is popular
            if name in popular_hashes_list:
                # Add the popular value to the list
                populars.append(name)

        # Return the first popular value if found, otherwise return all matching values
        return populars[0] if populars else output


if __name__ == '__main__':
    try:
        # Call the main function with a sample hash (MD5)
        print(main("46f94c8de14fb36680850768ff1b7f2a"))

    # Handle KeyboardInterrupt gracefully
    except KeyboardInterrupt:
        exit()

```