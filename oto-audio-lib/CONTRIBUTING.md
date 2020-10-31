# Contributors Guidelines to oto-audio

## Getting Started

### Learn Git and Github

All our development is done using Git and Github. If you're not too familiar with Git and Github, start by reviewing this guide. <https://guides.github.com/activities/hello-world/>

### Issues

On <https://github.com/vrook-co/oto-audio/issues> you can find all open Issues. You can find a detailed explanation on how to work with issues below under [Issue Allocation](#issue-allocation).

## Setup

### Forking a Repository

To contribute to oto-audio you will need to fork the this repository.
Then you can work risk-free on your fork.

You will just need to fork once. After that you can call `git fetch upstream` and `git pull 'branch-name'` before you do your local changes to get the remote changes and be up-to-date

### Setting up Pre-Commit Hook

You can install it with the command `pip install pre-commit`

Then you just need to call `pre-commit install`

This can all also be done by running `make install_hooks`

### Syncing a Forked Repository

To sync your fork with this repository please see this [Guide](https://help.github.com/articles/syncing-a-fork/) on how to sync your fork.

## Contributing

### Issue Allocation

If you want to work on an open issue, please post a comment telling that you will work on that issue, we will assign you as the assignee then.

**Caution**: We try our best to keep the assignee up-to-date, but as we are all humans with our own schedule delays are possible, so make sure to check the comments once before you start working on an issue even when no one is assigned to it.

### Writing Test Cases

It's important to write test cases, and test the code before submitting a Pull Request (PR).

Oto-audio is using `pytest` to execute the test cases.

#### Parametrize your Test Cases

Sometimes you want to test functions that hold multiple arguments, which again can have multiple values. To test this, please parametrize your tests.

Example:

```python
@pytest.mark.parametrize(
       "compress, compressScheme", [(True, "lz4"), (False, "lz4")]
    )
def test_hooked_tensor(self, compress, compressScheme):
    TorchHook(torch)

    t = Tensor(numpy.random.random((100, 100)))
    t_serialized = serialize(t, compress=compress, compressScheme=compressScheme)
    t_serialized_deserialized = deserialize(
        t_serialized, compressed=compress, compressScheme=compressScheme
        )
    assert (t == t_serialized_deserialized).all()
```
### Documentation and Codestyle

To ensure code quality and make sure other people can understand your changes, you have to document your code. For documentation we are using the Google Python Style Rules which can be found [here](https://github.com/google/styleguide/blob/gh-pages/pyguide.md). A well wrote example can we viewed [here](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html).

You documentation should not describe the obvious, but explain what's the intention behind the code and how you tried to realize your intention.

You should also document non self-explanatory code fragments e.g. complicated for-loops. Again please do not just describe what each line is doing but also explain the idea behind the code fragment and why you decided to use that exact solution.

#### Type Checking

The codebase contains [static type hints](https://docs.python.org/3/library/typing.html) for code clarity and catching errors prior to runtime. If you're adding type hints, please run the static type checker to ensure the type annotations you added are correct via:

```bash
mypy filename
```

### Keep it DRY (Don't repeat yourself)

As with any software project, it's important to keep the amount of code to a minimum, so keep code duplication to a minimum!

### Creating a Pull Request

At any point in time you can create a pull request, so others can see your changes and give you feedback.
Please create all pull requests to the `master` branch.

### Check and Wait for Reviews

We will only merge PRs that pass the tests.

If your check fails, don't worry, you will still be able to make changes and make your code pass the checks.

