## Setup
* [https://gorails.com/setup/osx/10.11-el-capitan](https://gorails.com/setup/osx/10.11-el-capitan)
## Docker-compose Deployment instructions
1. rails new shdr-portal --database=postgresql
2. Add Cartfile
3. Add docker-compose.yml
4. ```docker-compose build```
5. Modify config/database.yml
6. ```docker-compose up```
7. ```docker-compose run web rake db:create```
8. ```docker-compose run web rake db:migrate```
9. ```docker-compose run down```
10. ```docker-compose run web bundle install```
11. ```docker-compose up --build```
## Components
* [sortable-lists](http://railscasts.com/episodes/147-sortable-lists-revised?view=asciicast)
* [https://gorails.com/episodes/sortable-drag-and-drop](https://gorails.com/episodes/sortable-drag-and-drop)
* [https://stackoverflow.com/a/17830722](https://stackoverflow.com/a/17830722)
