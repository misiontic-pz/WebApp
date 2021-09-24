###First time
npm install

###Run App
npm run serve

###Deployment
- heroku login
- heroku create 'appName'
- heroku container:login
- heroku container:push web --app misiontic-100polas
- heroku container:release web --app misiontic-100polas