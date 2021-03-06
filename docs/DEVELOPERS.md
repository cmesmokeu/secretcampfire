## `secret campfire` handshake requirements
To participate and play in the `secret campfire` network, your instance must implement the following endpoints:
  - `/feed`
    
    `/feed/<offset>`
    
    - feed JSON schema:
      ```
        {
          "name": "Feed Name",
          "description": "",
          "avatar_url": "",
          "header_url": "",
          "blog_url": "http://instance",
          "style_url": "http://instance/stylesheets/feed.css",
          "nsfw": false,
          "posts": [
            {
              "id": "5c5d40a0e96ba00004b9cde9",
              "title": "Title",
              "date": "2012-04-23T18:25:43.511Z",
              "thumbs": [],
              "urls": [],
              "text": "markdown",
              "tags": [],
              "post_url": "/post/id",
              "re_url": "http://reblogged_from_instance/post/id"
            }
          ]
        }
      ```
    - the `style_url` field in the feed provides custom CSS to render:
      - infinite-scroll viewer for entire feed
      - single-post page
  - `/post/<id>`
    - returns JSON of post from DB
    
    - post JSON schema:
    ```
      {
          "name": "Feed Name",
          "description": "",
          "avatar_url": "",
          "header_url": "",
          "blog_url": "http://instance",
          "style_url": "http://instance/stylesheets/feed.css",
          "nsfw": false,
          "post":
            {
              "id": "5c5d40a0e96ba00004b9cde9",
              "title": "Title",
              "date": "2012-04-23T18:25:43.511Z",
              "thumbs": [],
              "urls": [],
              "text": "markdown",
              "tags": [],
              "post_url": "/post/id",
              "re_url": "http://reblogged_from_instance/post/id"
            }
       }
    ```
  - `/render/<feed>` and `/render/<post>`
    - pulls `feed` JSON and renders infinite-scroll viewer
    - pulls `post` JSON and renders single-post page
  - `/dashboard` 
  
    `/dashboard/<offset>`
    
    - (private)
    - for owner to view live stream of followed blogs
    - for owner to add/manage posts

## Design philosophy
 
- Separate code from platform (user is free to run code on any platform).
- Separate platform from database (user is free to plug and play any database).
- Separate platform from media -- don't host media (user is free to use any existing platform to host images and videos). 
- Database only stores user's text data and links to external media.
- For security, all user's actions must be redirected to execute on the user's own Dashboard (e.g., Post, Reblog, Follow, Unfollow). 
- Don't reinvent the wheel. Use off-the-shelf components whenever possible.
- Less is more and more is lazy.

## Recommended tech
  - MVC: Node.js + Express + Bootstrap + MongoDB
  - hosting: Heroku, Google Cloud Platform
  - media hosting: Gfycat, Imgur, ImageBam, YouTube, etc

The architecture ingredients above are recommendations. Feel free to use your favorite technology to meet the `handshake requirements` above.
