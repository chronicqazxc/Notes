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
## Gem install pg for Rails
* [ERROR:  Error installing pg: ERROR: Failed to build gem native extension.](https://stackoverflow.com/a/39301829)
## Components
* [sortable-lists](http://railscasts.com/episodes/147-sortable-lists-revised?view=asciicast)
* [https://gorails.com/episodes/sortable-drag-and-drop](https://gorails.com/episodes/sortable-drag-and-drop)
* [https://stackoverflow.com/a/17830722](https://stackoverflow.com/a/17830722)
## Sortable list format
* Example1:
```html
<ul id="sortlist">
        <li id="#<%= 'city_Vancouver' + catalog.id.to_s %>">Vancouver</li>
        <li id="#<%= 'city_Toronto' + catalog.id.to_s %>">Toronto</li>
        <li id="#<%= 'city_Montreal' + catalog.id.to_s %>">Montreal</li>
        <li id="#<%= 'city_Ottawa' + catalog.id.to_s %>">Ottawa</li>
        <li id="#<%= 'city_Calgary' + catalog.id.to_s %>">Calgary</li>
        <li id="#<%= 'city_Edmonton' + catalog.id.to_s %>">Edmonton</li>
        <li id="#<%= 'city_Winnipeg' + catalog.id.to_s %>">Winnipeg</li>
</ul>
```
* Example2:
```html
<div id="links" data-update-url="<%= sort_links_url %>" class="list-group list-group-justified">
          <% catalog.links.order("position").each do |link| %>
            <%= link_to link.title, modal_catalogs_link_path(catalog, link), remote: true, title: link.content, 'id' => "link_"+link.id.to_s, 'class' => 'list-group-item', 'data-toggle' => 'tooltip', 'data-placement' => 'top' %>
          <% end %>
</div>
```
