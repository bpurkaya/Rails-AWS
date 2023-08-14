# Rails-AWS
### Install asdf and ruby 

- sudo apt install curl git
- git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.8.1
- echo '. $HOME/.asdf/asdf.sh' >> ~/.bashrc
- echo '. $HOME/.asdf/completions/asdf.bash' >> ~/.bashrc
- source ~/.bashrc

### Install llibrary dependencies & ruby 
- sudo apt-get install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev gcc
- asdf plugin add ruby
- asdf plugin-update ruby
- asdf install ruby latest
- asdf global ruby 3.0.2 
- ruby -v

### Install postgreSQL 
apt install postgresql postgresql-contrib libpq-dev
sudo -u postgres createuser -s ubuntu -P
- sudo -u postgres psql
- \password ubuntu 

- echo 'export SHOP2HERO_DATABASE_PASSWORD=“YourPassword” >> ~/.bashrc
- source ~/.bashrc


### Install rails and bundler 
- gem install rails 
- gem install bundler 
- gem update --system


### Install Nodejs & yarn 
- curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
- sudo apt-get install -y nodejs

- curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
- echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
- sudo apt-get update
- sudo apt-get install yarn

### Create a new rails app with react frontend and postgresql database 

- rails new my_first_rails_app -d=postgresql -T --webpack=react 
- cd my_first_rails_app
- bundle install 
- yarn install


### Start server 


- rails s -p 3003 -b 0.0.0.0
