# Ruby - Command Line Interface Project

## READ BEFORE STARTING

**Use a cloud based service or a local IDE**<br>

**Create a GitHub Repository/commit frequently**<br>

You've gone through Ruby syntax and most importantly programming fundamentals. That should be enough to create an awesome Ruby CLI, a command line interface.

We will create a gem to do just this.

Here are some examples of project themes and features

- Project Theme examples but not limited to the following:
  - text adventure game
  - music albums
  - social media 
  - movies 
  - games 
  - books 
  - language interpreter 
  - secret language interpreter
- scrape data from a webpage/display, here are some example sites:
    - https://www.scrapethissite.com/pages/
    - http://toscrape.com/
    - https://webscraper.io/test-sites
-  Use the faraday gem to send requests to an API!

## Setup

`bundle gem project_name` to create a gem. Use the directory/file structure to your advantage to organize files.

### bin/run

Under bin, create a file called `run`. Use the shebang line `#!/usr/bin/env ruby ` at the top of your file. Now if you enter `bin/run` in the terminal, it should execute `run` as a ruby file.

In case you get a `permission denied` error, run `chmod +x bin/*`.

or you can execute the run file with `ruby bin/run` if you are have any issues

### README.md

Create a `README.md` file in the root directory of the project.

Copy and paste:

```
# TODO: Enter project name

# TODO: Add project summary

# TODO: CLI Feature 1
# TODO: CLI Feature 2
# TODO: CLI Feature 3
```

Fulfill each todo.

#### Optional

- Scrape data using Nokogiri/open-uri
- Incorporate a login/logout system using BCrypt
- Send requests to an API to capture data using Faraday

---
