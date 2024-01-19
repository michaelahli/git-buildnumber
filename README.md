# About git-buildnumber

`git-buildnumber` produces versions strings for Git repositories in a `W.X.Y.Z`
format, such that:

```txt
W - Number of years since the start of the repo
X - Month of year of a git commit
Y - Day of the month of a git commit
Z - Order (the number) of the git commit that day
```

By default, `git-buildnumber` calculates `W` as the number of calendar years
since the repo's initial commit, but can be changed via a command-line option
(see below).

### Use-case

`git-buildnumber` produces standardized version strings in a human-readable
form for use with rolling release cycles, or when a lexicographically-ordered
build number is desirable. Version strings generated by `git-buildnumber` are not
meant as a replacement for standard short/long Git commit hashes.

## Installing

Install in the usual [Go][go-project] way:

```sh
$ go install github.com/michaelahli/git-buildnumber@latest
```

## Using

The following examples are for the `HEAD` of a Git repo created in 2014, and
where the latest commit (ie, the 0th) was made on March 3rd, 2015:

```sh
# general (from within the git worktree)
$ cd /path/to/repo
$ git-buildnumber
v1.2.3.0

# specify path to repo
$ git-buildnumber /path/to/repo
v1.2.3.0

# short form (trims last ".0")
$ git-buildnumber -short
v1.2.3

# use 2000 as year offset
$ git-buildnumber -year 2000
v15.2.3.0

# use 2015 as year offset
$ git-buildnumber -year 2015
v0.2.3.0

# short form and 2000 as year offset
$ git-buildnumber -short -year 2000
v15.2.3

# short form and 0 as year offset
$ git-buildnumber -short -year 0
v2015.2.3

# inverse
$ git-buildnumber -inverse v1.2.3.0
a3efd74543d3402b62184081ed93bfdf2c65421d
```

### Command-line parameters

```sh
Usage of git-buildnumber:
  -inverse string
    	string to inverse
  -prefix string
    	prefix (default "v")
  -rev string
    	git revision (default "HEAD")
  -sep string
    	field separator (default ".")
  -short
    	trim last "<sep>0" from version
  -year string
    	start year offset
```

**Note**: when `-year` is not specified, then an attempt is made to use the
year of the first commit in the repository. If the year cannot be determined,
then no offset calculation will be performed.

[go-project]: https://golang.org/project/
