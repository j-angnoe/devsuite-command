# Devsuite command

## Installation
npm install -g devsuite-command

A small utility that lets you easily switch to different projects via your terminal.

Enter a project directory and run `devsuite bookmark` to bookmark the project.
It will register the directory and a name in $HOME/.devsuites.json

Now you can access the project quickly by running `devsuite enter [name]`.
(This will open the default $SHELL in the project directory)

To run any command against the project directory run `devsuite [somecommand] [...args]`
for instance, a file listing: `devsuite ls`

devsuite will check if the command is in your path, otherwise, it will interpret as
`devsuite npm run [somecommand]`

# Why
The reasons this utility comes in handy:
- Commands like docker-compose require you to run it in the directory containing the 
  docker-compose.yml. This can be inconvenient when you are deep inside a subfolder and need
  to restart a docker-service. Now with the devsuite command at hand you can always run a 
  command against the project root from any subfolder. Now i can run `devsuite docker-compose restart` instead of traveling to project-directory and running it. 
- I often need to switch to different projects and start the application(s) by running 
docker-compose up. I find any open idle terminal and run devsuite enter [project] and get
going.

# How it works
There are basically two mechanisms:

- Find the nearest project root directory: This directory is detected because it will
  have a '.devsuiterc' file in it.

- Resolve a project name and open a shell with the project directory as working directory.
  This information is stored inside '.devsuites.json' in your $HOME folder. Entries to this
  file are added whenever you run `devsuite bookmark` inside a project root directory. `devsuite bookmark` will also create a '.devsuiterc' file when none exist in the directory.

- Run commands against project root:
    - First it will check if the command exists inside your $PATH and run it. It will 
    pass the existing environment and will use the project root directory as working directory.
    - If the command does not exist it will try to interpret it as an npm script. (scripts
    that are defined in a package.json). 







