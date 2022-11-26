# nornir_rich

## My branch (format_string_result)

If more than the one *Result* variable (*print_result(results, vars=["diff", "result", etc])*) is passed into ***print_result*** it renders (with *render_scope*) it as a dictionary resulting in the printed string output losing its formatting (new lines not honoured). This is only the case for multiple variables, if just use *print_result(results)* it doesnt render it so you dont have the problem.

As I am screen scraping command outputs and in some situations use multiple variables I have added a new *render_panelgroup* method to make the string look like it is a dictionary (using *rich.text*) grouping the different result variables under the one panel using [panel groups through the Rich group() decorator](https://rich.readthedocs.io/en/stable/group.html).

As this changes nornir_rich operation in way the output is displayed and is more custom to what I want to achieve didnt think was worth putting in as a pull request.

To install this branch:

```bash
pip install git+https://github.com/sjhloco/nornir_rich@format_string_result
```

To reference in a requirement file:

```bash
nornir-rich @ git+https://github.com/sjhloco/nornir_rich@849923339ac0ade999059b7cd2a28890dfcaf4b2
```

## Install

```bash
pip install nornir-rich
```

## Usage

Features

- Print functions
  - `print_result`
  - `print_failed_hosts`
  - `print_inventory`
- Processors
  - `progressbar`


### Print example

```python
from nornir_rich.functions import print_result

results = nr.run(
    task=hello_world
)

print_result(results)
print_result(results, vars=["diff", "result", "name", "exception", "severity_level"])
```

### Progress bar example

```python
from time import sleep
from nornir_rich.progress_bar import RichProgressBar


def random_sleep(task: Task) -> Result:
    delay = randrange(10)
    sleep(delay)
    return Result(host=task.host, result=f"{delay} seconds delay")


nr_with_processors = nr.with_processors([RichProgressBar()])
result = nr_with_processors.run(task=random_sleep)
```


## Images

### Print Inventory

![Print inventory](docs/imgs/print_inventory.png)

### Print Result

![Print Result](docs/imgs/print_result.png)

### Progress Bar

![Progress Bar](docs/imgs/progressbar.png)


More [examples](docs/imgs/print_functions.ipynb)
