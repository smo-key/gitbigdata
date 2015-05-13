![Git Big Data logo](https://raw.githubusercontent.com/smo-key/gitbigdata/master/img/gitbigdata-extended-gh.png)

Displays every public metric possible about Github, its users, its organizations, its repos, and its impact on the global community.

**Call to developers and idea-makers:** see below to [help support this project](https://github.com/smo-key/gitbigdata#support-this-project)

## How it started
GitBigData started when I browsed the network graph of Github's largest project I know of - the linux kernel.  After finding the graph unavailable (and for good reason, it's huge!), I decided to try to make an app to create these large, unavailable network graphs.  From that moment, the idea evolved into a project dedicated with indexing the entirety of public Github and to mine these nodes of data into useful analytics for the common Github user.

## How it works
GitBigData is an app written in NodeJS to scan Github's public users, repositories, and organizations and collect this data into comprehensible statistics.

The app itself consists of four main parts: the database, the request balancer, the Github API and social media scraper, the parser, and finally the web interface.

- **Overview: Balancer -> Scrapers -> Parsers -> Web interface**
- Database: MongoDB - stores the nodes of data downloaded by scrapers and the human-friendly results from the parsers
- Balancer / Allocator: Distributes API requests by the scraper equally from users' rate limits to scrapers
- Scraper: constantly downloads data from the Github API - only indexes nodes requested by the parsers
  - Live Scraper: constantly indexes new nodes
  - Initialize Scraper: re-searches all nodes for a new data point
  - Custom Scraper: rescrapes a node whenever a user requests it
- Parser: reads metric JS files that search the massive data retrieved from the scraper and create properties
  - Initialize Parser: immediately when the parse is created, this thread works on brand new metrics
  - Live Parser: constantly reads all available metrics files for new data
  - Clean Parser: removes parts of nodes created by the scraper when they are deemed unused by future parsers
- Live Web interface: displays all data from the parser to the user and gets new data from the server every few seconds

## Stages of Development
- [ ] Stage 1: Get data by the repo or user, no live or initialize scraper
- [ ] Stage 1.1: Web interface for repo and user sections
- [ ] Stage 2.0: Begin campaign to ask users to donate a portion of their API time to the app (suggested by Github staff)
- [ ] Stage 2.1: Scrape for every repository possible (starting with Linux or continuous list), wait a while
- [ ] Stage 3: Scrape these repositories for additional metrics, one or two at a time
- [ ] Stage 4: Social media scraping (to find Github's impact on global code community)
- [ ] Stage 5: Additional research into topics such as global code climate, database API, etc.

## Code Philisophy
- The top priority is creating userful or empowering analytics for the Github community
- The app runs on seperate servers dedicated to their task - servers share the relational database
- Asynchronous threading is controlled and rate limited so as to not pose a threat to Github's servers
- Parsers are modular, taking in data metric files (javascript with a few required and special functions) and parsing the data into data points displayed to the user
- Compression algorithms value storage space over computation speed but are prepared for a migration to a more rapid but space-intensive algorithm (I'm not working with very large storage servers here yet, but have significant processing power)
- The less requests, the better - find the optimal path toward least API calls to Github's servers and use resorces such as https://www.githubarchive.org/, http://ghtorrent.org/, and https://libgit2.github.com/ to gather more data, faster, without the need to go through GitHub's servers.
- User engagement is important, as well as full database visibility and code transparency (all open source, clean, and documented)

## Potential Data Points
Data points are separated into four sections in the UI: the Github Overview (which shows points about all data collected) and data by Organization, User, and Repo.

Please feel free to fork and add to this list!

### Github Overview
- Users
  - Most active users (user with most contributions - contributions to larger repositories are weighted more)
  - Linus number distribution chart
  - Rising stars (new developers with high weighted contributions)
  - Just Joined (brand new users - live)
- Repos
  - Count of all repos
  - Largest developer communities (includes not just commits, but contributions)
  - Most active repositories (most commits in the last few days)
  - Hidden gems (active repos with lower contributions)
  - Largest wikis
- Organizations
  - Most active organizations
  - Most repositories
  - Most public users
  - Most influence (forks)

### Organization
- Users' activity
- Number of repositories
- Languages of repositories
- Influence ranking (count of forks)
- Active
- Private information (if logged it and part of org)
  - All of above, plus specification by team

### User
- Your Linus Number (distance to someone that committed to the Linux repository)
- Location
  - Other basic details
- Total contributions
- Number of repos owned
- Number of repos contributed to
- Contributions / year
- Timing of contributions (morning, day, night, etc.)
- Contribution ratio (yours / others)
- Language graph (most frequent programming languages used)

### Repo
- Entire network graph
- Entire contributors list


## Support this Project
This project **currently runs on your stars and feedback**.  GitBigData encourages you to fork or clone this repository with the objective to return data back into the project.  My personal email, for any feedback to, interest in, or advise for this project, is pachachura.arthur@gmail.com.

Thank you for your interest in this project!

---
smo-key (:bear:) and contributors
