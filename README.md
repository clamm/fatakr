This repo is an exemplary data repository (place where the posts are stored) for the Airbnb knowledge repo: https://github.com/airbnb/knowledge-repo


# Test of Knowledge Repo

## Quickstart 
(copied from https://github.com/airbnb/knowledge-repo)

1. Install the knowledge-repo tooling (incl. support for all project types)
  
  ```
  git clone https://github.com/airbnb/knowledge-repo.git
  cd knowledge-repo
  pip install ".[all]"
  ```

2. Initialize a knowledge repository - your posts will get added here

  ```
  knowledge_repo --repo ./example_repo init
  ```

3. Create a post template

  ```
  knowledge_repo --repo ./example_repo create ipynb example_post.ipynb
  ```

4. Edit the notebook file example_post.ipynb as you normally would.

5. Add your post to the repo with path project/example

  ```
  knowledge_repo --repo ./example_repo add example_post.ipynb -p project/example
  ```

6. Preview the added post

  ```
  knowledge_repo --repo ./example_repo preview project/example
  ```


## Run Knowledge Repo web server on multiple data repositories

1. Setup a second data repo

  ```
  cd ~/Development/knowledge-repo
  knowledge_repo --repo ~/Desktop/my_k_repo init
  ```

2. Put a post into this second data repo

  ```
  knowledge_repo --repo ~/Desktop/my_k_repo add example_post.ipynb -p project/example
  ```

3. Start the web server sourcing both data repos

  ```
  knowledge_repo --repo "{Desktop}~/Desktop/my_k_repo" --repo "{dev}./example_repo" runserver
  ```

4. Checkout http://localhost:7000/feed


## Test markdown posts with images

1. Initialize template for markdown report

  ```
  cd ~/Development/knowledge-repo
  knowledge_repo --repo ./example_repo create md example_post.md
  ```

2. Put images into the template

  ```
  cp ~/Pictures/karaoke.png ~/Development/knowledge-repo
  <edit the markdown file to contain the following line
  ![karaoke pic](karaoke.png)
  >
  ```

3. Put the markdown post into the data repo (in a separate project because of naming conflict)

  ```
  knowledge_repo --repo ./example_repo add example_post.md -p project/markdown
  ```

4. Start the web server and verify that images are displayed

  ```
  knowledge_repo --repo "{Desktop}~/Desktop/my_k_repo" --repo "{dev}./example_repo" runserver
  ```

5. Checkout http://localhost:7000/feed


## Test adding knowledge posts to a GitHub hosted data repo

1. Create a repo on GitHub and clone it

  ```
  cd ~/Development
  git clone https://github.com/clamm/my_posts.git
  cd my_posts
  ```

2. Initialise the knowledge_repo in this git repo:

  ```
  knowledge_repo --repo ~/Development/my_posts init
  ```

3. Put the markdown post into that data repo (in a separate project because of naming conflict)

  ```
  knowledge_repo --repo ~/Development/my_posts add example_post.md -p project/markdown
  ```

4. Preview the post

  ```
  knowledge_repo --repo ~/Development/my_posts preview project/markdown
  ```

5. Submit the post

  ```
  knowledge_repo --repo ~/Development/my_posts submit project/markdown
  ```

6. Open a PR on https://github.com/clamm/my_posts

7. Review the PR

8. Do changes

  ```
  knowledge_repo --repo ~/Development/my_posts add example_post.md -p project/markdown --update
  knowledge_repo --repo ~/Development/my_posts preview project/markdown
  knowledge_repo --repo ~/Development/my_posts submit project/markdown
  ```

7. Merge the PR


## Test running the web server on a VM to host a GitHub data repo

:hand: WORK IN PROGRESS - need to read about the webserver deployment

1. Install knowledge_repo tooling on VM

  See https://github.com/clamm/marry_vagrant_and_ansible to create a Vagrant VM with the knowledge repo tooling installed.

2. Clone the data repo on the VM

  ```
  cd /tmp
  git clone https://github.com/clamm/my_posts.git
  ```

3. Start the web server and verify that posts are visible

  ```
  knowledge_repo --repo "/tmp/my_k_repo" run server --port 4567
  ```

4. Checkout http://localhost:4567/feed

