## Create a new React app:
```
npx create-react-app my-react-app
```
## Navigate to your project:
```
cd my-react-app
```
## Local Run the development server:
```
npm start
```
Runs the app in the development mode.
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

## Dockerize
Create `Dockerfile` in root directore. 
```
FROM node:14

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

#EXPOSE 3000

CMD [ "npm", "start" ]
```
## Build and Run Docker
```
docker build -t my-react-app:001 .
docker run -p 3000:3000 my-react-app:001

```

## Network Configuration:
Ensure that your Docker container is running in the same network context as your host machine. Docker containers typically use bridge networking by default, so they should be accessible on `localhost` or `127.0.0.1` from the host machine.

## Check Browser URL:
If your app is running but not automatically opening in the browser, try manually navigating to the URL. By default, the app should be accessible at `http://localhost:3000` if the React app is configured to use port 3000.

#  `With Project details click` [Here](https://github.com/Ashadozzaman/docker-images/tree/main/my-react-app)