# API CATATAN Abraham Yusuf

strapi application API For [Catatan Abraham Yusuf](https://github.com/abraham-yusuf/catatan-abraham-yusuf)

## Features

- 4 Content types: Article, Category, Contributor, Pages.
- Publication system (draft & published).
- Preview unpublished content: Articles, pages.
- Slug system
- 2 Contributor types: Featured, default.
- SEO and social media friendly
- Role based access controls

## API Routes

- `/articles`
- `/categories`
- `/contributors`
- `/pages`

## Getting started

Create your own copy of this project by clone this repository.

### Running locally

Create a folder and `git clone` from your own repository.

Install the dependencies and start the dev server.

```bash
    yarn install
    yarn develop
```

The strapi server will run on [http://localhost:1337](http://localhost:1337)

Go to the admin panel [(http://localhost:1337/admin)](http://localhost:1337), create an account and start adding sample content.

### Deployment to Production

First, you'll need a [Cloudinary](https://cloudinary.com) and a [Heroku](https://www.heroku.com/) account.

Don't Forget to add some package
```bash
    yarn add strapi-provider-upload-cloudinary 
    && yarn add pg
    yarn build && yarn develop
```

1. From your copy of the repo "Deploy to Heroku"
2. Fill the Cloudinary ENV variables. // see in .env.example
3. Deploy
4. Once is deployed, go to the admin panel e.g. `https://yourherokudomain.com/admin` and create an account.
5. Last, go to "Setting" > "Users & permissions plugins" > "Public" > "Permissions" and check `find` on Article, Category, Contributor and Pages.
6. in folder config, let's create folder then add database.js eg: /env/production/database.js
fill this to database.js
```bash
    module.exports = ({ env }) => ({
  defaultConnection: "default",
  connections: {
    default: {
      connector: "bookshelf",
      settings: {
        client: "postgres",
        host: env("DATABASE_HOST", "localhost"),
        port: env.int("DATABASE_PORT", 5432),
        database: env("DATABASE_NAME", "strapi"),
        username: env("DATABASE_USERNAME", "strapi"),
        password: env("DATABASE_PASSWORD", "strapi"),
        schema: "public",
        ssl: { rejectUnauthorized: false },
      },
      options: {},
    },
  },
});
```
7. and let's create plugins.js in /config/env/production/
fill this
```bash
    //file in /config/env/production/plugins.js

    module.exports = ({ env }) => ({
  upload: {
    provider: "cloudinary",
    providerOptions: {
      cloud_name: env("CLOUDINARY_NAME"),
      api_key: env("CLOUDINARY_KEY"),
      api_secret: env("CLOUDINARY_SECRET"),
    },
  },
});
```
### Adding Content

The recommended flow for adding new content is:

- Add contributor
- Add category
- Add article or page

### Preview Content

Once you have your frontend deployed go to "Settings" > "Preview Content"

Fill it with your info, the URL should look like this.
`https://<yoursite.com>/api/:contentType-preview?secret=<your-secret>&id=:id`

Now, go to any article or page and click on "Preview".

## License

[MIT License](https://github.com/abraham-yusuf/api-catatan-abraham-yusuf/blob/main/LICENSE).
